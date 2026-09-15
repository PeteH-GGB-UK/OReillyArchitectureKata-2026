| So let's split his requirements into different groupings and then we can review each group separately to delve deeper into the requirements. Something they might need from an architectural perspective, both lines and boxes, but also what sort of hardware things you might need. As an example, identifying queues and guiding visitors: how would they identify queues? There are a number of ways. Sam did talk about using MQTT quite a bit, so we could use those sort of things. Same with monitoring other animals. |
| --- |

Here’s a useful first-cut split. I’d treat “visitor experience” as customer-facing, and the other three as estate operations—connected by an event backbone such as MQTT.

| **Group** | **Business requirements** | **Likely physical/hardware needs** | **Architectural direction** |
| --- | --- | --- | --- |
| Visitor journey & growth | Ticket sales, family passes, repeat visits, referrals, understand visitor preferences | Website/mobile access; optionally ticket kiosks, barcode/QR scanners and turnstiles | Ticketing, customer accounts, CRM/marketing consent and campaign services |
| Crowd & site operations | Identify popular areas, queues and congestion; guide guests to quieter or relevant locations | Turnstile counts, infrared/thermal people counters, queue cameras with edge analytics, WiFi/Bluetooth presence sensors, staff tablets, digital signs | Real-time occupancy/queue service; notification/signage service; privacy-preserving analytics |
| Ride operations | Understand ride popularity; detect recurring maintenance problems; enable proactive maintenance | Ride telemetry sensors where feasible, inspections via maintenance tablets, spare-parts scanning, perhaps vibration/temperature/current sensors | Asset register, maintenance-work-order system, ride telemetry ingestion and predictive-maintenance analytics |
| Animal care & welfare | Track feeding, health, sickness and animal populations; monitor aquatic and land exhibits | Keeper tablets, feed scales, RFID tags where appropriate, enclosure temperature/humidity sensors, water-quality sensors, cameras, automated counters | Animal records, feeding/health workflows, sensor ingestion, alerts and audit trail |
| Shared estate platform | Operate efficiently and profitably; correlate attraction demand, queues, maintenance and animal care | Site network, resilient gateways, local edge devices, WiFi/ethernet, power/UPS for critical kit | Identity/access control, operational reporting, data platform, alerting, integrations and security |

For queue identification, I’d start with reliable, low-intrusion methods:

Turnstile or entrance/exit counters establish ride throughput.

Overhead people-counting cameras or infrared sensors measure the queue length/zone occupancy.

An edge gateway publishes readings such as park/ride/rollercoaster/queue/occupancy over MQTT.

A queue service converts those readings into estimated wait times.

The visitor app and nearby signs recommend alternatives when a queue crosses a threshold.

The same pattern works for animal monitoring: sensors and keeper-entered observations publish events through MQTT, while the animal-care service owns the authoritative health, feeding, and population records. The important architectural boundary is that MQTT carries telemetry/events—it should not become the system of record.

| Sam did mention that the Wi-Fi capability on this date was quite patchy, so we would need to ensure that any MQTT device, if it used Wi-Fi, had some form of store and forward capability.We would also need to decide whether we want store and forward for each individual device or whether some type of hard-wired connection to one or more locations which would store and fold from there. This may only be useful in parts of the estate if we're monitoring the animals themselves. If they have the MQTT device, you would probably also need Wi-Fi close to them. Hardwire that tomorrow at a central location somewhere. You probably still need more than one, and then either something like a line-of-sight between specified locations on the estate to a central hub where the main work was done, or something similar. |
| --- |

Yes—a hybrid edge design fits the estate well. I would avoid making every sensor depend on a continuously available WiFi connection to a central broker.

The design principle would be:

Put resilient, mains-powered edge gateways in a few local estate zones—especially around animal enclosures.

Let nearby devices communicate over short, strong links. These might be local WiFi, wired Ethernet for fixed equipment, or a lower-power sensor network where battery life/range matters.

Give each gateway durable store-and-forward storage: it queues MQTT messages during a backhaul outage and forwards them once connectivity returns.

Give individual devices a small buffer only for readings that cannot safely be lost, such as water quality, enclosure temperature, feed events, or ride safety/maintenance alerts. This protects against the short outage between device and gateway.

Backhaul gateways to the central estate platform primarily over wired fibre/Ethernet where practical. For remote estate sections, use redundant line-of-sight point-to-point wireless links.

Keep WiFi local to the enclosure or operational zone; do not attempt blanket WiFi coverage just for sensors.

For animal monitoring, I’d also distinguish normal telemetry from urgent welfare events:

Normal readings can be stored and forwarded.

Critical thresholds should trigger a local alarm at the gateway and notify staff by whatever path is available; they should not wait for the central platform or an internet connection.

This gives the estate a sensible hierarchy: sensor → local gateway → resilient backhaul → central MQTT/platform. It reduces WiFi coverage demands while preserving data and operational safety during outages.
