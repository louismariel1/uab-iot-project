# XIV. IMPLEMENTATION OPTIONS AND SELECTION RATIONALE

This chapter compares implementation alternatives for the SSP wearable, edge gateway, cloud back-end, and user interface. Selections are based on functional performance, energy efficiency, reliability, security, integration complexity, component availability, and cost. The wearable circuit architecture and energy budget are presented in Chapter XIII.

## XIV.1. Wearable Hardware

The SSP wearable integrates low-power motion sensing, GNSS positioning, BLE communication, tamper detection, haptic feedback, local event buffering, and rechargeable power management.

Two implementation approaches are considered: integration of commercially available electronic components and modules, or custom PCB design and professional manufacturing. A hybrid approach is preferred, using commercial modules for functional validation followed by integration onto a compact custom PCB.

### XIV.1.1. Commercial Wearable Component Alternatives

Three candidate component configurations are compared:

- **Configuration A — Preferred SSP:** Components selected in the Chapter XIII hardware architecture.
- **Configuration B — Alternative SSP:** Commercial alternatives providing comparable core functions.
- **Configuration C — Alternative SSP:** Additional component alternatives with different integration, performance, and cost characteristics.

**Table XIV-I. Commercial Component Alternatives for the SSP Wearable**

| Hardware function       | Configuration A         | Configuration B            | Configuration C        |
| ----------------------- | ----------------------- | -------------------------- | ---------------------- |
| MCU + BLE               | Raytac MDBT50Q-1MV2     | Raytac MDBT50Q-1MEN        | nRF5340-based module   |
| 6-axis IMU              | Bosch BMI270            | ST LSM6DSOX                | TDK ICM-42688-P        |
| GNSS positioning        | u-blox MAX-M10S         | u-blox SAM-M10Q            | Quectel L76K           |
| Tamper detection        | TI DRV5032              | Allegro A3213              | Magnetic reed switch   |
| Haptic actuator         | Coin-type ERM motor     | LRA actuator               | Piezoelectric actuator |
| Battery charging / PMIC | TI BQ25120A             | TI BQ24074                 | Microchip MCP73831     |
| Nonvolatile storage     | nRF52840 internal flash | Winbond W25Q16JV           | MB85RC256V FRAM        |
| Rechargeable battery    | 3.7 V, 500 mAh LiPo     | 3.7 V, 400 mAh LiPo        | 3.7 V, 600 mAh LiPo    |
| GNSS antenna            | Ceramic GNSS antenna    | Integrated in SAM-M10Q     | Active GNSS antenna    |
| Haptic driver           | Logic-level N-MOSFET    | TI DRV2605L                | TI DRV2604L            |
| Charging interface      | Sealed USB-C            | Magnetic charging contacts | Inductive charging     |

The three configurations represent candidate component combinations rather than electrically interchangeable assemblies. Differences in supply voltage, logic levels, charging circuits, actuator drivers, antenna requirements, and firmware interfaces must be considered during integration.

All configurations retain the same SSP functional architecture, with deterministic processing on the wearable and AI inference at the Edge and Cloud layers.

### XIV.1.2. Comparative Component Cost Estimation

Table XIV-II presents indicative small-quantity component purchase costs for the three configurations. Values are expressed in euros per wearable and exclude VAT, shipping, PCB fabrication, enclosure manufacturing, assembly, and testing.

**Table XIV-II. Estimated Component Costs for Three SSP Wearable Configurations**

| Hardware function      | A (€)     | B (€)     | C (€)     |
| ---------------------- | --------- | --------- | --------- |
| MCU + BLE              | 5.40      | 6.50      | 10.00     |
| 6-axis IMU             | 3.62      | 4.00      | 5.00      |
| GNSS receiver          | 9.78      | 11.77     | 9.00      |
| Tamper sensor          | 0.80      | 1.00      | 0.50      |
| Haptic actuator        | 2.50      | 4.00      | 3.00      |
| Charging / PMIC        | 3.50      | 2.50      | 1.00      |
| Nonvolatile storage    | 0.00      | 1.20      | 3.50      |
| LiPo battery           | 7.00      | 6.00      | 8.00      |
| GNSS antenna           | 2.00      | 0.00      | 5.00      |
| Haptic driver          | 0.30      | 2.50      | 2.50      |
| Charging interface     | 1.00      | 2.00      | 5.00      |
| **Estimated subtotal** | **35.90** | **41.47** | **52.50** |

The component subtotal is calculated as:

$$\
C\_{\mathrm{BOM}}=\sum\_{i=1}^{n}q_i p_i\
$$

where $q_i$ is the quantity of component $i$ and $p_i$ is its unit purchase price.

The values are preliminary engineering allowances based on candidate commercial components, not complete supplier quotations. Exact prices depend on manufacturer part numbers, procurement quantities, distributor availability, and component specifications.

The zero-cost storage entry in Configuration A reflects the use of MCU-integrated flash rather than a separate memory component. Configuration B uses a GNSS receiver with an integrated antenna, avoiding a separate antenna purchase.

The estimated subtotals exclude supporting electronic components, voltage regulators where additionally required, PCB fabrication, connectors, enclosure, sealing, assembly, testing, and production overhead. They therefore do not represent complete manufacturing costs.

### XIV.1.3. Preferred Configuration and Implementation Strategy

**Configuration A is selected as the SSP wearable baseline**, consistent with the circuit architecture and energy model in Chapter XIII.

The principal selection rationale is:

- **MCU and BLE:** Raytac MDBT50Q-1MV2, based on the Nordic nRF52840, provides integrated BLE, low-power operation, 1 MB flash, 256 KB RAM, and suitable peripheral interfaces.
- **Motion sensing:** Bosch BMI270 supports configurable six-axis sensing and interrupt-based operation for adaptive monitoring.
- **Positioning:** u-blox MAX-M10S provides compact GNSS functionality with configurable acquisition and power-management behaviour.
- **Tamper detection:** TI DRV5032 enables low-power magnetic detection without mechanical contacts.
- **Haptic feedback:** A coin-type ERM motor provides simple tactile alerts using controlled switching.
- **Local memory:** Internal MCU flash supports configuration storage and limited event buffering without an additional memory device.
- **Power management:** TI BQ25120A combines rechargeable-battery charging, power-path management, and voltage regulation.
- **Battery:** A protected 3.7 V, 500 mAh LiPo battery supports rechargeable operation within the selected wearable architecture.

Configuration A has the lowest estimated component subtotal at €35.90. However, the final selection also depends on electrical compatibility, energy consumption, component availability, enclosure integration, and reliability.

The preferred implementation strategy is hybrid: commercial development boards and breakout modules support functional validation, followed by integration onto a compact custom PCB.

The final hardware design requires verification of GNSS supply and logic compatibility, haptic motor voltage and driver requirements, charging and battery protection, antenna performance, PCB dimensions, and environmental protection.

The selected wearable targets a minimum seven-day battery autonomy, with a fourteen-day engineering objective, as evaluated in Section XIII.4. It also supports the SSP retail-price objective of €80–€120, subject to complete manufacturing-cost estimation.

## XIV.2. Edge Gateway Hardware and Connectivity

The selected edge architecture uses an externally powered Linux-capable ARM gateway for sensor-data fusion, contextual AI inference, predictive geofencing, event validation, and local buffering.

- **Processing platform:** A Raspberry Pi-class Linux ARM single-board computer is the reference implementation, selected for software support, flexibility, and cost. Industrial Linux gateways and x86 mini-PCs are alternatives where robustness, lifecycle, or processing requirements justify them.
- **AI processing:** CPU-based inference is preferred for contextual AI workloads. An NPU or GPU accelerator may be considered if measured inference latency or processing demand requires additional acceleration.
- **Local storage:** Industrial microSD is preferred for the reference gateway. eMMC and SSD alternatives provide different trade-offs in write endurance, reliability, capacity, and cost.
- **Wearable connectivity:** BLE is selected to communicate with the SSP wearable, matching the device hardware and communication architecture.
- **Primary backhaul:** Ethernet is preferred for stable wired communication with the cloud. Wi-Fi is an alternative where cabling is impractical.
- **Failover connectivity:** Cellular 4G/5G is an optional backup connection, using link monitoring and automatic switching where supported.
- **Satellite backhaul:** Satellite remains an optional alternative for locations without suitable terrestrial coverage, subject to equipment, service, latency, and operating costs.
- **Resilience:** Automatic connectivity monitoring, local buffering, and reconnection procedures are preferred over manual recovery.

The edge gateway performs contextual AI processing and event handling independently of cloud availability. Multiple gateways support the distributed SSP deployment, with local processing and buffering capacity assessed against the requirements in Table 2.

## XIV.3. Cloud Back-End Technologies

The preferred cloud architecture uses managed public-cloud services for telemetry ingestion, storage, analytics, alert management, and scalability.

- **Cloud deployment:** Managed public cloud is selected for scalability and reduced infrastructure maintenance. Self-managed virtual machines and container platforms are alternatives offering greater deployment control.
- **Message ingestion:** A managed MQTT broker over TLS is preferred for secure telemetry and event ingestion. Self-hosted MQTT brokers and HTTPS-based ingestion are alternatives.
- **Time-series storage:** Managed time-series storage is preferred for sensor telemetry and time-based queries. PostgreSQL with a time-series extension is an alternative.
- **Structured data:** Managed relational storage is preferred for devices, users, configuration, events, and audit records. Self-managed PostgreSQL is an alternative.
- **Historical archives:** Object storage is selected for scalable long-term data retention.
- **Analytics and AI:** Managed analytics and AI services are preferred for historical analysis, multi-device correlation, and model management. Containerized workloads offer greater customization and portability.
- **Identity and access:** Managed identity with role-based access control (RBAC) is preferred for authentication, authorization, and auditing.
- **Monitoring and scaling:** Managed monitoring, autoscaling, and distributed processing are preferred to support increasing device and message volumes.

The SSP architecture targets **100,000 active wearable devices** distributed across multiple edge gateways.

Assuming one telemetry message per device every ten seconds, the corresponding cloud ingestion requirement is:

$$\
R\_{\mathrm{telemetry}}=\frac{100,000}{10}\
\=10,000\ \mathrm{messages/s}\
$$

The cloud therefore targets at least 10,000 telemetry messages/s under this operating assumption. Event-processing capacity must additionally account for event frequency, simultaneous alerts, and burst conditions.

Horizontal scaling of message ingestion, processing, and storage supports the target deployment size. Actual throughput, latency, availability, and scalability require verification against the performance requirements in Table 2.

Recurring cloud costs depend on message volume, data retention, storage, processing, network traffic, and service configuration.

## XIV.4. User Interface and API Technologies

The SSP user interface supports authorized monitoring, alerts, historical reporting, and system configuration.

- **Web front-end:** React is selected for its component-based architecture, maintainability, and development ecosystem. Angular and Vue are alternatives.
- **Mobile application:** Flutter is preferred if a dedicated cross-platform mobile application is implemented. React Native and native Android/iOS development are alternatives.
- **Application API:** HTTPS REST is selected for authenticated queries and configuration. GraphQL is an alternative for more flexible client queries.
- **Real-time updates:** WebSockets are preferred for live dashboard updates. HTTPS polling is a simpler alternative but can introduce additional requests and update delays.
- **Mobile alerts:** Push notifications are preferred for timely operator alerts, with periodic polling as an alternative.
- **Visualization:** Web-mapping and charting libraries support geofence monitoring, device locations, and historical analysis.
- **Authentication:** Managed identity with RBAC is selected to separate operator and administrator permissions and support access auditing.

React, HTTPS REST, WebSockets, and managed identity form the selected web-interface baseline, consistent with the cloud architecture described in Chapter XII.

## XIV.5. Selected Baseline and Selection Rationale

The selected SSP implementation combines the following technologies across the four system layers:

- **Device:** Configuration A, comprising the nRF52840 BLE MCU, BMI270 IMU, MAX-M10S GNSS receiver, DRV5032 tamper sensor, ERM haptic motor, BQ25120A power management, and 500 mAh LiPo battery. This combination prioritizes low-power operation, compact integration, deterministic event processing, and cost control.
- **Edge:** Linux-capable ARM gateway with CPU-based contextual AI, BLE communication, local buffering, and Ethernet backhaul. Wi-Fi and cellular provide alternative connectivity options.
- **Cloud:** Managed MQTT ingestion, time-series and relational storage, historical analytics, cloud AI, managed identity, monitoring, and horizontal scaling toward 100,000 active devices.
- **User Interface:** React web application, HTTPS REST APIs, WebSocket updates, and RBAC. Flutter remains the preferred option for a dedicated mobile application.
- **Communication:** BLE between wearable and edge, MQTT over TLS between edge and cloud, and HTTPS REST for authenticated application access. Ethernet is the preferred gateway backhaul, with Wi-Fi, cellular, and optional satellite alternatives.

The wearable performs adaptive sensing and deterministic event processing, the Edge executes contextual AI and predictive geofencing, and the Cloud provides historical analytics and centralized services.

The comparative component analysis identifies Configuration A as the preferred wearable design, with an estimated component subtotal of €35.90. Configurations B and C remain alternative candidate assemblies, subject to electrical, mechanical, energy, and cost verification.

The SSP economic model targets a device retail price of €80–€120 and a proposed subscription of €9.99 per device per month. Complete hardware costs include electronic components, PCB fabrication, assembly, battery, enclosure, and testing. Deployment and operating costs additionally include edge hardware, connectivity, and cloud services.

Overall, the selected architecture balances functional performance, energy efficiency, implementation complexity, reliability, scalability, and cost against the requirements specified in Table 2.

### Integration notes

The chapter now has two new tables and three subsections under XIV.1, without changing the remaining chapter numbering.

Two points should be addressed before final report submission:

1. Table 2 consistency: Update the cloud scalability and telemetry-ingestion requirements to 100,000 active devices and 10,000 messages/s at a ten-second reporting interval. The existing 20 events/s requirement also needs an explicit scope or revised burst-load assumption.
2. Component verification: The cost comparison is an engineering estimate, not a fully quoted manufacturing BOM. Exact manufacturer part numbers and supplier prices remain to be confirmed for generic components, particularly batteries, actuators, antennas, and charging interfaces.

The preferred architecture, Chapter XIII component selections, and existing Edge/Cloud/UI technology choices remain unchanged.
