 # SSP — Smart Safety & Protection IoT System

 ## D2 — Functional and Performance Specifications

 **Academic Year:** 2026/2027\
 **Course:** IoT Design Project\
 **Deliverable:** D2 — Functional & Performance Specifications\
 **Acronym:** SSP\
 **Authors:** _\[Insert group members\]_

---

 ## Abstract

 This paper defines the functional and performance specifications of the proposed Smart Safety & Protection (SSP) IoT system. SSP is a distributed IoT solution designed to monitor the location, movement, proximity and operational state of a protected person or asset and to provide relevant information and alerts to authorized users.

 The target system consists of five principal layers: sensing and device processing, edge processing, communication, cloud services and user interface (UI). The specification defines the functions assigned to each layer and establishes measurable performance requirements for computational processing, communication, energy consumption, mechanical characteristics, cloud infrastructure, UI performance and system cost.

 A central objective of this D2 is to explicitly separate **functional requirements**, which describe what the system shall do, from **performance requirements**, which describe how well those functions shall operate. The document also defines the data generated, processed and transmitted at each node, including data types, formats, packet sizes, update rates and storage requirements.

 The proposed requirements are design targets rather than experimentally validated results. Their feasibility will be evaluated during subsequent deliveries through component selection, implementation, measurements and validation. Market context is included only to establish the relevance of the selected functions and constraints; the detailed market research is considered completed as part of the preceding project work.

 **Index Terms—** Internet of Things, IoT, wearable device, safety monitoring, edge computing, cloud computing, positioning, motion sensing, event detection, energy management.

---

 # I. INTRODUCTION

 ## A. Motivation

 Many safety-monitoring applications require information about the location, movement and operational condition of a person or protected asset. A useful monitoring system must not only collect sensor measurements but also transform those measurements into reliable information and actionable events.

 The proposed Smart Safety & Protection (SSP) system addresses this requirement through a distributed IoT architecture combining sensing, local processing, edge computing, communication, cloud services and an authorized user interface.

 The design is intended to support applications in which:

 - the current or recent location of a monitored entity is relevant;
- movement or inactivity may provide useful contextual information;
- proximity information can contribute to event detection;
- device status and battery condition must be monitored;
- communication may temporarily become unavailable;
- events should continue to be detected during degraded connectivity;
- sensitive location and movement data require controlled access; and
- the system should remain portable and energy efficient.

 The purpose of this D2 is to establish the requirements that will guide the later architecture, hardware selection, implementation, AI development and validation stages.

 The specification intentionally does not prescribe a final microcontroller, sensor, communication protocol, cloud provider or AI model. Those implementation decisions belong to subsequent deliveries.

---

 # II. SYSTEM SCOPE AND TARGET ARCHITECTURE

 ## A. Target System

 The target SSP system is defined as:

 **Sensors → Device Processing → Edge → Wide-Area Communication → Cloud → Analytics → UI**

 The five principal system layers are:

 1. **Device:** sensing, local preprocessing, event detection, energy management and temporary storage.
2. **Edge:** data reception, validation, aggregation, local processing, temporary storage and communication management.
3. **Communication:** bidirectional transfer of measurements, events, configuration and status.
4. **Cloud:** centralized ingestion, storage, analytics, device management, user management and APIs.
5. **UI:** presentation of current status, position, events, historical information and authorized configuration.

 The laboratory prototype may implement only a subset of the complete target system. For example, a smartphone or development computer may temporarily perform functions that would ultimately belong to a dedicated edge or cloud component.

 The requirements in this document nevertheless describe the **target SSP solution**, not merely the laboratory prototype.

 ## B. Device-to-Edge-to-Cloud Data Flow

 The principal data flow is:

 **Physical environment → Sensors → Device → Edge → Cloud → UI**

 Control and configuration information follows the reverse direction:

 **UI → Cloud → Edge → Device**

 The architecture shall also support local operation when one or more communication links are unavailable.

---

 # III. MARKET CONTEXT AND DESIGN CONSTRAINTS

 The detailed market research and brainstorming were completed before D2. They are treated as project background. This section retains only the market observations that directly justify the requirements defined in this document.

 Commercial safety and tracking products already provide several functions that SSP also requires. For example, T-Mobile's SyncUP KIDS Watch provides real-time GPS location tracking, virtual boundary alerts and emergency functionality through an application. T-Mobile's SyncUP TRACKER provides near-real-time location tracking, geofencing, location history and motion alerts.  T-Mobile+1

 AngelSense similarly provides continuous monitoring, real-time location, geofencing, notifications and historical activity information. Its documented location-update behavior also demonstrates that commercial systems adapt update frequency to activity and context rather than necessarily transmitting at a constant maximum rate.  AngelSense+2

 These observations establish that location tracking, event notification, historical information and mobile monitoring are established market expectations rather than unique SSP functions.

 Consequently, SSP's D2 requirements focus on the intended combination of:

 - multi-source sensing;
- local and edge processing;
- adaptive sensing and communication;
- operation during temporary connectivity loss;
- explicit energy management;
- event-oriented processing;
- controlled access to sensitive data;
- scalable cloud architecture; and
- optional AI-assisted interpretation.

 The D2 does **not** claim that SSP is already commercially superior to existing products. Commercial competitiveness must be evaluated later using implemented performance, measured battery life, reliability, total cost and comparison with actual competing products.

 The market observations also influence the following requirements:

 - useful location updates must be available without continuously transmitting maximum-rate raw sensor data;
- event alerts require low latency;
- the system should provide historical information;
- the device must remain portable;
- battery autonomy must be compatible with practical deployment;
- the UI must support map-based and event-based monitoring; and
- communication loss must not automatically terminate local monitoring.

---

 # IV. FUNCTIONAL SPECIFICATIONS

 Functional specifications describe **what SSP shall do**. Numerical performance requirements are specified separately in Section VI.

 ## A. Device Functions

 The device shall provide the following functions.

 **F-D01 — Motion sensing:**\
 The device shall acquire motion information using inertial sensors suitable for detecting movement, inactivity, acceleration patterns and other relevant motion states.

 **F-D02 — Position determination:**\
 The device shall acquire positioning information when a positioning source is available.

 **F-D03 — Proximity detection:**\
 The device shall detect the presence, absence or state of relevant nearby devices or proximity references.

 **F-D04 — Device-state monitoring:**\
 The device shall monitor battery state, communication state, sensor state and relevant internal health indicators.

 **F-D05 — Local preprocessing:**\
 The device shall filter, validate, transform and/or aggregate sensor information before transmission when this reduces communication or energy requirements.

 **F-D06 — Local event detection:**\
 The device shall evaluate deterministic rules and/or lightweight inference to identify events requiring further processing or immediate communication.

 **F-D07 — Temporary storage:**\
 The device shall buffer relevant measurements, status records and events when communication is temporarily unavailable.

 **F-D08 — Local status generation:**\
 The device shall generate information describing its operational state.

 **F-D09 — Energy management:**\
 The device shall adapt its operating state according to monitoring requirements, detected activity and available battery energy.

 **F-D10 — Configuration reception:**\
 The device shall receive authorized configuration parameters such as sampling rates, monitoring modes and communication settings.

 **F-D11 — Device identification:**\
 The device shall maintain a unique identity used for data association and authenticated communication.

 **F-D12 — Secure firmware lifecycle:**\
 The target product shall support authenticated firmware updates.

---

 ## B. Edge Functions

 The edge layer shall provide:

 **F-E01 — Data reception:** receive data from one or more devices.

 **F-E02 — Message validation:** verify message structure, identity, sequence information and data validity.

 **F-E03 — Timestamping:** assign or verify timestamps and preserve the relationship between measurement time and reception time.

 **F-E04 — Data ordering:** use sequence numbers and timestamps to identify out-of-order messages.

 **F-E05 — Aggregation:** combine measurements and events into structured edge records.

 **F-E06 — Local filtering:** remove invalid, redundant or irrelevant information according to configured rules.

 **F-E07 — Feature extraction:** calculate selected features from incoming sensor information.

 **F-E08 — Event evaluation:** execute local event rules.

 **F-E09 — Low-latency inference:** execute selected inference functions where local processing provides a latency or connectivity advantage.

 **F-E10 — Offline buffering:** temporarily store information when cloud connectivity is unavailable.

 **F-E11 — Synchronization:** transmit buffered information after connectivity is restored.

 **F-E12 — Duplicate handling:** detect duplicate messages using identifiers and sequence numbers.

 **F-E13 — Cloud forwarding:** transmit relevant records and events to the cloud.

 **F-E14 — Configuration forwarding:** forward authorized configuration information to the appropriate devices.

 **F-E15 — Local operational continuity:** continue selected monitoring and event-processing functions while the cloud is unavailable.

---

 ## C. Communication Functions

 The communication subsystem shall:

 **F-C01:** provide device-to-edge communication.

 **F-C02:** provide edge-to-cloud communication.

 **F-C03:** support bidirectional communication.

 **F-C04:** transmit telemetry data.

 **F-C05:** transmit event data with appropriate priority.

 **F-C06:** transmit device and communication status.

 **F-C07:** transmit authorized configuration information.

 **F-C08:** support retry and synchronization mechanisms.

 **F-C09:** protect message integrity.

 **F-C10:** authenticate communicating devices.

 **F-C11:** detect communication failures.

 **F-C12:** support temporary offline operation.

 The final communication technologies shall be selected during subsequent architecture and hardware evaluation.

---

 ## D. Cloud Functions

 The cloud subsystem shall:

 **F-CL01:** register devices.

 **F-CL02:** authenticate devices.

 **F-CL03:** authenticate users.

 **F-CL04:** receive telemetry.

 **F-CL05:** receive events.

 **F-CL06:** validate incoming data.

 **F-CL07:** store historical telemetry and event information.

 **F-CL08:** maintain current device state.

 **F-CL09:** process events.

 **F-CL10:** execute cloud-level analytics.

 **F-CL11:** support AI model management where applicable.

 **F-CL12:** manage users and roles.

 **F-CL13:** enforce access permissions.

 **F-CL14:** maintain audit information.

 **F-CL15:** provide APIs to authorized applications.

 **F-CL16:** support device/fleet management.

 **F-CL17:** support configurable retention and deletion.

 **F-CL18:** generate authorized notifications.

 **F-CL19:** provide historical data queries.

---

 ## E. User Interface Functions

 The UI shall provide authorized users with:

 **F-U01:** current device status.

 **F-U02:** current or most recent position.

 **F-U03:** event notifications.

 **F-U04:** event history.

 **F-U05:** map-based visualization.

 **F-U06:** battery information.

 **F-U07:** communication status.

 **F-U08:** historical sensor/event summaries.

 **F-U09:** device management according to authorization.

 **F-U10:** user management according to authorization.

 **F-U11:** permitted configuration functions.

 **F-U12:** event acknowledgement where applicable.

 **F-U13:** audit information for authorized administrative users.

 The UI shall not display information for which the authenticated user does not have permission.

---

 # V. DATA SPECIFICATIONS

 The data specification defines what information exists at each node and how much information is transferred.

 ## A. Data Representation Strategy

 The system shall use two logical representation levels:

 1. **Compact device-level representation**, optimized for bandwidth and energy efficiency.
2. **Structured edge/cloud representation**, optimized for interoperability, processing and maintainability.

 Binary, CBOR, Protocol Buffers or an equivalent compact representation may be used for device communication. JSON or an equivalent structured representation may be used for cloud APIs.

 The exact encoding will be selected during later implementation.

---

 ## B. Device Sensor Data

 | Data | Type | Unit | Typical Size | Maximum Size | Source |
| --- | --- | --- | --- | --- | --- |
| Device ID | UUID/binary identifier | — | 16 B | 16 B | Device |
| Timestamp | 64-bit integer | ms | 8 B | 8 B | Device |
| Accelerometer X/Y/Z | 16-bit integer or float | g | 6–12 B | 12 B | IMU |
| Gyroscope X/Y/Z | 16-bit integer or float | °/s | 6–12 B | 12 B | IMU |
| Latitude | 32-bit float | degrees | 4 B | 4 B | Positioning |
| Longitude | 32-bit float | degrees | 4 B | 4 B | Positioning |
| Position confidence | 32-bit float | m | 4 B | 4 B | Positioning |
| Proximity state | integer/enum | state | 1 B | 1 B | Proximity sensor |
| Battery level | unsigned integer | % | 1 B | 1 B | Device |
| Device state | enum | state | 1 B | 1 B | Device |
| Communication state | enum | state | 1 B | 1 B | Communication |
| Event flag | enum/bit field | state | 1 B | 1 B | Device |
| Sequence number | unsigned integer | — | 4 B | 4 B | Device |

The values in this table describe the logical data representation. Actual binary encoding may introduce headers, checksums, timestamps or protocol metadata.

---

 ## C. Device Sampling Requirements

 The target device shall support adaptive sampling.

 | Measurement | Normal Mode | Event/High-Activity Mode |
| --- | --- | --- |
| Accelerometer | up to 50 Hz | up to 100 Hz |
| Gyroscope | up to 50 Hz | up to 100 Hz |
| Position | 0.1–1 Hz | dynamically increased when required |
| Proximity | event/state dependent | event/state dependent |
| Battery/status | approximately every 60 s | approximately every 10–60 s |
| Aggregated telemetry | every 10–60 s | event dependent |

The device shall not continuously transmit every raw inertial sample during normal operation unless a diagnostic or specific monitoring mode requires it.

---

 ## D. Device-to-Edge Packets

 The principal device-to-edge application packets shall be:

 ### 1\. Normal telemetry packet

 Target maximum payload:

 **≤128 bytes**

 The packet shall contain, as applicable:

 - device ID;
- timestamp;
- sequence number;
- summarized motion information;
- position;
- position confidence;
- battery state;
- communication/device state;
- event state.

 ### 2\. Event packet

 Target maximum application payload:

 **≤512 bytes**

 The event packet shall contain:

 - device ID;
- event ID;
- event type;
- event timestamp;
- event severity;
- relevant measurements/features;
- confidence/quality;
- sequence number;
- current device state.

 Lower-layer protocol overhead is excluded from these application payload limits.

---

 ## E. Device Data Volume

 The device shall be designed around **application traffic rather than continuous raw sensor transmission**.

 The target normal application traffic is:

 **≤10 kbit/s per device average.**

 The device-to-edge communication link shall nevertheless provide a substantially higher capacity:

 **≥100 kbit/s application-level link capacity target.**

 The difference between these values provides headroom for event bursts, retransmission and protocol overhead.

---

 ## F. Edge Data

 The edge shall transform incoming device information into structured records containing at least:

 - device ID;
- measurement timestamp;
- edge reception timestamp;
- sequence number;
- sensor/feature values;
- position;
- position confidence;
- battery state;
- communication state;
- event state;
- processing status;
- source identifier.

 Target edge record size:

 **≤1 kB per structured record.**

 Normal aggregated telemetry shall be forwarded to the cloud approximately every 10–60 s.

 Event information shall be forwarded immediately when connectivity is available.

---

 ## G. Edge-to-Cloud Data

 Edge-to-cloud messages shall use a structured representation.

 A telemetry record shall contain:

 - device ID;
- timestamp;
- data type;
- measurement;
- unit;
- quality/confidence;
- source;
- sequence number.

 An event record shall additionally contain:

 - event ID;
- event type;
- severity;
- confidence;
- triggering inputs;
- event timestamp;
- processing status;
- acknowledgement status where applicable.

 Target maximum application record size:

 **≤1 kB for normal telemetry/event records.**

 Larger historical responses shall use pagination.

---

 ## H. Cloud Data

 The cloud shall maintain at least four logical data classes:

 1. **Telemetry data**
2. **Event data**
3. **Device-management data**
4. **User/audit data**

 Cloud records shall be stored in a form that permits:

 - chronological queries;
- device-based queries;
- event-based queries;
- aggregation;
- analytics;
- retention control;
- deletion;
- auditing.

---

 ## I. UI/API Data

 The UI shall normally request processed and summarized information rather than continuously retrieving raw sensor streams.

 Normal UI/API responses shall contain:

 - current device state;
- current/recent position;
- recent events;
- battery state;
- communication state;
- historical summaries;
- requested configuration information.

 Target normal response payload:

 **≤100 kB per request/page.**

 Historical information larger than this shall be paginated.

---

 # VI. PERFORMANCE SPECIFICATIONS

 Functional specifications define what SSP shall do. The following requirements define measurable limits describing how well the system shall perform.

 ## A. Computational Performance

 ### 1\. Device

 | Parameter | Requirement |
| --- | --- |
| Sensor acquisition latency | ≤20 ms |
| Local preprocessing latency | ≤100 ms |
| Local event-rule evaluation | ≤200 ms |
| Event decision generation | ≤500 ms |
| Local buffer write latency | ≤100 ms |
| Average local processing duty cycle | ≤20% |

The device shall continue essential monitoring without requiring continuous cloud availability.

 ### 2\. Device-to-Edge

 | Parameter | Target |
| --- | --- |
| Application latency | ≤2 s nominal |
| Normal telemetry interval | 10–60 s |
| Normal application traffic | ≤10 kbit/s/device |
| Required link capacity | ≥100 kbit/s/device |
| Event burst capacity | ≥50 kbit/s/device |
| Application packet loss after retry | \<1% target |
| Offline buffer | ≥24 h |

---

 # VII. COMMUNICATION PERFORMANCE

 ## A. Device-to-Edge Communication

 The device-to-edge link shall be:

 - wireless;
- short range;
- low power;
- bidirectional;
- suitable for periodic telemetry;
- suitable for event transmission.

 Target requirements:

 | Parameter | Target |
| --- | --- |
| Nominal range | ≥10 m |
| Minimum practical range | ≥5 m |
| Application throughput capability | ≥100 kbit/s |
| Typical latency | ≤500 ms |
| Event delivery latency | ≤2 s |
| Communication direction | Bidirectional |

The final technology shall be selected after comparison of candidate technologies.

 ## B. Edge-to-Cloud Communication

 The wide-area connection shall provide:

 | Parameter | Target |
| --- | --- |
| Connectivity | Wireless wide-area |
| Minimum application capacity | ≥50 kbit/s/device |
| Typical event latency | ≤5 s |
| Availability | ≥99% when network coverage exists |
| Offline operation | Required |
| Synchronization after recovery | Required |

The design shall not assume continuous availability of an external network.

---

 # VIII. COMMUNICATION RESILIENCE

 The system shall continue useful operation during communication loss.

 When cloud connectivity is unavailable:

 1. the device shall continue local monitoring;
2. relevant events shall be buffered;
3. the edge shall continue local processing where available;
4. buffered records shall be synchronized after reconnection;
5. sequence numbers shall identify missing or duplicated information;
6. duplicate messages shall be detected;
7. critical events shall not be silently discarded solely because the cloud is unavailable.

 Target minimum buffering:

 **24 hours of event/status information.**

---

 # IX. ENERGY PERFORMANCE

 Energy consumption is a primary constraint because the SSP device is intended to be wearable or portable.

 ## A. Device Power Targets

 | Operating State | Maximum/Target Average Power |
| --- | --- |
| Deep sleep | ≤1 mW |
| Normal monitoring | ≤50 mW |
| Active sensing | ≤150 mW |
| Communication burst | ≤500 mW peak |
| Positioning active | ≤300 mW peak |

These values are design targets and shall be validated after component selection.

 ## B. Battery Autonomy

 The target minimum battery autonomy shall be:

 **≥7 days**

 The engineering objective shall be:

 **≥14 days under nominal monitoring conditions.**

 The final battery capacity shall be calculated during the hardware-design stage using measured or manufacturer-specified component consumption.

 ## C. Energy Duty Cycle

 The design shall consider:

 - sleep;
- sensing;
- local computation;
- positioning;
- wireless transmission;
- wireless reception;
- event processing.

 Target nominal duty cycle:

 | State | Target Duty Cycle |
| --- | --- |
| Sleep/low power | 80–90% |
| Normal sensing | 8–15% |
| Positioning | 1–5% |
| Communication | \<2% |
| High-intensity event mode | Event dependent |

The percentages are engineering targets rather than simultaneous mandatory percentages. The final energy model shall be based on actual operating-mode measurements.

---

 # X. MECHANICAL AND ENVIRONMENTAL PERFORMANCE

 ## A. Device Mechanical Requirements

 | Parameter | Requirement |
| --- | --- |
| Maximum volume | ≤100 cm³ |
| Maximum mass | ≤100 g |
| Form factor | Wearable/portable |
| Operating temperature | −10 to +50 °C |
| Storage temperature | −20 to +60 °C |
| Ingress protection | Target IP65 or better |
| Drop resistance | ≥1 m target |
| Continuous operation | Required |

The enclosure shall protect the electronics during ordinary wearable/mobile operation.

 ## B. Edge Mechanical Requirements

 If a dedicated physical edge gateway is used, its design target shall be:

 | Parameter | Target |
| --- | --- |
| Maximum mass | ≤500 g |
| Maximum volume | ≤2 L |
| Continuous operation | Required |
| Cooling | Passive preferred |
| External power | Permitted |
| Portable operation | Preferred where deployment requires it |

If the edge is implemented by an existing smartphone, computer or gateway, these dedicated edge mechanical constraints may instead be treated as interface and deployment constraints.

 ## C. Environmental Requirements

 The system shall tolerate:

 - normal outdoor operation;
- normal indoor operation;
- rain/splash exposure consistent with the specified IP rating;
- ordinary dust;
- vibration associated with normal movement;
- temperature variations within the specified operating range.

---

 # XI. CLOUD PERFORMANCE SPECIFICATIONS

 ## A. Capacity and Scalability

 The initial cloud architecture shall support:

 **100 active devices.**

 The architecture shall have a scalability objective of:

 **≥10,000 devices.**

 This does not imply that 10,000 devices must be deployed during the project.

 ## B. Cloud Performance Targets

 | Parameter | Target |
| --- | --- |
| Initial fleet | 100 devices |
| Scalable fleet | ≥10,000 devices |
| Telemetry ingestion | ≥100 messages/s initial capacity |
| Event ingestion | ≥20 events/s burst |
| API p95 latency | ≤1 s for normal queries |
| Event processing p95 | ≤2 s |
| Service availability | ≥99.5% |
| Historical retention | ≥12 months |
| Device metadata | Lifecycle duration |
| Backup | Required |
| Audit logging | Required |

---

 # XII. CLOUD STORAGE REQUIREMENTS

 For a planning calculation, assume:

 - average telemetry record = 200 bytes;
- one record every 30 s;
- 86,400 s/day.

 For one device:

 $$
200 \times \frac{86400}{30}
=576,000\text{ bytes/day}
$$

 This corresponds to approximately:

 **0.576 MB/device/day**

 For 1,000 devices:

 **576 MB/day**

 For one year:

 **approximately 210 GB/year**

 For 10,000 devices:

 **approximately 2.1 TB/year**

 These calculations represent raw application data before database indexes, replication, metadata, backups and other infrastructure overhead.

 Therefore, the initial cloud deployment shall provide:

 **≥500 GB usable application storage**

 while the production architecture shall support scalable expansion beyond this capacity.

 The 500 GB target is therefore an **initial deployment requirement**, not the storage limit for the 10,000-device scalability objective.

---

 # XIII. USER INTERFACE PERFORMANCE

 | Function | Target |
| --- | --- |
| Login response | ≤2 s |
| Dashboard load | ≤3 s |
| Current status refresh | ≤5 s |
| Event display after cloud ingestion | ≤5 s |
| Historical query p95 | ≤2 s |
| Map display | ≤3 s |
| Normal API response | ≤100 kB |

The UI shall remain usable on desktop and mobile-class displays.

 The UI shall prioritize:

 - current state;
- current/recent position;
- significant events;
- battery state;
- communication state;
- historical summaries.

---

 # XIV. END-TO-END EVENT PERFORMANCE

 Operationally significant events may be generated by the device, edge or cloud.

 Each event shall contain:

 - event type;
- timestamp;
- source;
- severity;
- confidence/quality;
- relevant triggering information.

 The target event path is:

 **Sensor → Device/Edge → Cloud → UI ≤10 s**

 For high-priority events, the target is:

 **≤5 s**

 under nominal connectivity conditions.

 These targets are not guarantees under unavailable external networks.

---

 # XV. SECURITY REQUIREMENTS

 Security shall be incorporated into the system from the beginning.

 The system shall provide:

 - unique device identities;
- authenticated device communication;
- authenticated user access;
- role-based authorization;
- encrypted communication;
- protected credential storage;
- secure update mechanisms;
- audit logging;
- session management;
- protection against replay or duplicate messages where required.

 The final cryptographic algorithms and key-management implementation shall be selected during subsequent engineering stages.

---

 # XVI. PRIVACY REQUIREMENTS

 The system processes potentially sensitive location and movement information.

 Therefore:

 - only necessary information shall be collected;
- raw data shall not automatically be transmitted when derived information is sufficient;
- access shall be role-based;
- sensitive information shall be encrypted in transit and at rest;
- retention periods shall be configurable;
- deletion policies shall be supported;
- administrative access shall be auditable.

 The final implementation shall comply with the applicable privacy and data-protection requirements for its intended deployment.

---

 # XVII. AI FUNCTIONAL AND PERFORMANCE SCOPE

 AI is considered an optional intelligence layer rather than a prerequisite for all SSP functions.

 Potential AI functions include:

 - movement classification;
- activity recognition;
- anomaly detection;
- contextual event classification;
- false-event reduction;
- predictive maintenance.

 Deterministic rules shall remain available for functions that do not require machine learning.

 The detailed AI architecture belongs to a later delivery.

 ## AI Target Requirements

 | Metric | Initial Target |
| --- | --- |
| Classification accuracy | ≥90% on representative validation data |
| Event recall | ≥90% |
| False-positive rate | ≤5% target |
| Edge inference latency | ≤200 ms |
| Model update mechanism | Required |
| Model monitoring | Required |

These values are development targets and shall not be interpreted as achieved performance.

 The metrics shall be refined after the dataset, classes and validation methodology have been defined.

---

 # XVIII. ECONOMIC PERFORMANCE REQUIREMENTS

 The economic requirements are intended to prevent the technical architecture from becoming impractical for the intended deployment.

 ## A. Device Cost

 Target production-oriented hardware cost:

 **≤€150/device** for an initial low-volume design.

 Engineering objective for larger-scale production:

 **≤€100/device**

 These values exclude development, personnel, certification and other non-recurring costs.

 ## B. Recurring Cost

 Target communication and cloud operating cost:

 **≤€10/device/month**

 under normal operating conditions.

 This value is a design target and shall be refined after communication technology and cloud architecture are selected.

 ## C. Global Deployment Cost

 For an initial deployment of 100 devices, the D2 system-level economic ceiling shall be:

 **≤€25,000 for the first-year operational deployment target**, excluding personnel salaries and academic project-development labor.

 This target includes, where applicable:

 - 100 device hardware units;
- batteries and accessories;
- edge infrastructure;
- communication;
- cloud services;
- initial deployment software/services;
- expected maintenance/replacement allowance.

 Development, certification and organizational costs shall be separately identified in the later economic analysis.

 The purpose of this requirement is to establish a measurable upper boundary for the complete deployment rather than evaluating only the unit device price.

---

 # XIX. FUNCTIONAL–PERFORMANCE SEPARATION

 The following examples demonstrate the distinction between functional and performance requirements.

 ### Example 1 — Positioning

 **Functional requirement:**\
 The device shall determine its position.

 **Performance requirements:**\
 The position update rate shall be configurable between approximately 0.1 and 1 Hz under normal operation, with more frequent updates permitted during high-activity conditions.

 ### Example 2 — Event detection

 **Functional requirement:**\
 The device and/or edge shall detect relevant events.

 **Performance requirement:**\
 Local event decision generation shall be ≤500 ms.

 ### Example 3 — Communication

 **Functional requirement:**\
 The device shall transmit telemetry and events to the edge.

 **Performance requirement:**\
 The device-to-edge link shall provide ≥100 kbit/s application capacity, with nominal application latency ≤2 s.

 ### Example 4 — Cloud storage

 **Functional requirement:**\
 The cloud shall store historical telemetry and events.

 **Performance requirement:**\
 The initial deployment shall provide ≥500 GB usable application storage and ≥12 months historical retention.

 ### Example 5 — UI

 **Functional requirement:**\
 The UI shall display current device status and events.

 **Performance requirement:**\
 Dashboard loading shall be ≤3 s and normal API responses shall be ≤100 kB.

 This separation shall be maintained throughout subsequent project deliveries.

---

 # XX. REQUIREMENT TRACEABILITY

 | Requirement Area | D2 Requirement | Later Verification |
| --- | --- | --- |
| Device functions | F-D01–F-D12 | D3/D4 |
| Edge functions | F-E01–F-E15 | D3/D4 |
| Communication functions | F-C01–F-C12 | D3/D4 |
| Cloud functions | F-CL01–F-CL19 | D3/D4 |
| UI functions | F-U01–F-U13 | D3/D4 |
| Sensor data | Defined by data tables | D3/D4 |
| Data format | Compact + structured representation | D3 |
| Packet volume | 128 B normal / 512 B event | D3/D4 |
| Device throughput | ≤10 kbit/s normal | D4 |
| Link capacity | ≥100 kbit/s device-edge | D3/D4 |
| Device-edge latency | ≤2 s | D4 |
| Communication range | ≥10 m target | D4 |
| Offline buffering | ≥24 h | D4 |
| Energy | Power-mode limits defined | D4 |
| Battery autonomy | ≥7 days; ≥14 days objective | D4 |
| Device mechanics | ≤100 cm³ / ≤100 g | D4 |
| Edge mechanics | ≤2 L / ≤500 g if dedicated | D4 |
| Environmental | −10 to +50 °C; IP65 target | D4 |
| Cloud capacity | ≥100 devices initially | D3/D4 |
| Cloud scalability | ≥10,000 devices | D3/D4 |
| Cloud storage | ≥500 GB initial | D3/D4 |
| Cloud retention | ≥12 months | D3/D4 |
| UI latency | ≤3 s dashboard target | D3/D4 |
| End-to-end event | ≤10 s target | D4/D6 |
| High-priority event | ≤5 s target | D4/D6 |
| AI | Initial targets defined | D5 |
| Device cost | ≤€150 initial target | D4/D6 |
| Scaled device cost | ≤€100 objective | D6 |
| Recurring cost | ≤€10/device/month target | D6 |
| Global deployment | ≤€25,000 first-year target | D6 |

---

 # XXI. CONSISTENCY WITH MARKET REQUIREMENTS

 The D2 requirements are consistent with the functions already established in commercial safety and tracking systems.

 Real-time or near-real-time location, geofencing, event notifications, historical location information and application-based monitoring are established market functions. T-Mobile documents these capabilities for both SyncUP KIDS Watch and SyncUP TRACKER, while AngelSense documents continuous monitoring, real-time tracking, geofencing, notifications and historical activity.  T-Mobile+2

 Therefore, SSP does not define basic location tracking as its sole differentiation.

 The D2 design instead emphasizes a system architecture combining:

   **F-C12:** support temporary offline operation.

 The final communication technologies shall be selected during subsequent architecture and hardware evaluation.

---

 ## D. Cloud Functions

            **F-CL11:** support AI model management where applicable.

    **F-CL15:** provide APIs to authorized applications.

    **F-CL19:** provide historical data queries.

---

 ## E. User Interface Functions

 The UI shall provide authorized users with:

 **F-U01:** current device status.

 **F-U02:** current or most recent position.

       **F-U09:** device management according to authorization.

 **F-U10:** user management according to authorization.

 **F-U11:** permitted configuration functions.

 **F-U12:** event acknowledgement where applicable.

 **F-U13:** audit information for authorized administrative users.

---

 # V. DATA SPECIFICATIONS

 The data specification defines what information exists at each node and how much information is transferred.

 ## A. Data Representation Strategy

 The system shall use two logical representation levels:

 1. **Compact device-level representation**, optimized for bandwidth and energy efficiency.
2. **Structured edge/cloud representation**, optimized for interoperability, processing and maintainability.

 Binary, CBOR, Protocol Buffers or an equivalent compact representation may be used for device communication. JSON or an equivalent structured representation may be used for cloud APIs.

  1. **multi-source sensing;**
2. **adaptive monitoring;**
3. **local event processing;**
4. **edge processing;**
5. **communication-resilient operation;**
6. **explicit energy management;**
7. **privacy-aware data reduction;**
8. **cloud-based historical and fleet management;**
9. **role-based access; and**
10. **optional AI-assisted interpretation.**

 The requirements are therefore intended to make SSP technically comparable with established market expectations while leaving room for architectural differentiation.

 A definitive statement about commercial competitiveness is outside the scope of D2 because competitiveness requires measured implementation results, verified costs, reliability data and comparison against specific competing products.

---

 # XXII. KEY ENGINEERING TRADE-OFFS

 ## A. Monitoring Rate Versus Energy

 Increasing sensor and positioning rates improves temporal resolution but increases power consumption.

 Therefore:

 **Monitoring intensity ↔ responsiveness ↔ battery autonomy**

 The adaptive-sampling requirement is intended to balance these constraints.

 ## B. Local Processing Versus Communication

 Local preprocessing can reduce transmitted data and communication energy but requires additional computation.

 Therefore:

 **Local computation ↔ communication volume ↔ energy**

 ## C. Raw Data Versus Privacy

 Transmitting all raw sensor information provides greater analytical flexibility but increases bandwidth, storage and privacy exposure.

 Therefore:

 **Raw information ↔ analytical flexibility ↔ bandwidth ↔ privacy**

 ## D. AI Complexity Versus Latency

 More complex AI models may provide additional classification capability but require more computational resources.

 Therefore:

 **Model complexity ↔ analytical performance ↔ latency ↔ energy**

 ## E. Connectivity Versus Cost

 Greater communication availability may improve operational continuity but may increase recurring communication costs.

 Therefore:

 **Connectivity ↔ resilience ↔ operational cost**

---

 # XXIII. D2 COMPLIANCE CHECKLIST

 The D2 requirements can be directly mapped to the official questions as follows.

 | Official Question | D2 Coverage |
| --- | --- |
| Are all possible functions at device, edge, cloud and UI well defined? | Sections IV-A to IV-E define 12 device, 15 edge, 12 communication, 19 cloud and 13 UI functions. |
| Is the data well described at every node? | Section V defines device, device-edge, edge, edge-cloud, cloud and UI data. |
| Are data types and formats specified? | Section V defines logical types, units, sizes and representation strategy. |
| Is volume per packet specified? | Device telemetry ≤128 B; event packet ≤512 B; edge records ≤1 kB; UI/API response ≤100 kB. |
| Are functional and performance specifications separated? | Sections IV and VI-XVIII explicitly separate the two categories. |
| Are computational requirements specified? | Section VI defines acquisition, processing, event latency, duty cycle and throughput. |
| Are communication requirements specified? | Section VII defines wireless operation, range, latency, throughput and resilience. |
| Are energy requirements specified? | Section IX defines power limits, duty cycle and battery autonomy. |
| Are mechanical requirements specified? | Section X defines volume, mass, environmental limits and edge constraints. |
| Are cloud requirements specified? | Sections XI-XII define capacity, scalability, storage, latency, availability and retention. |
| Are UI requirements specified? | Section XIII defines UI functions and response-time targets. |
| Are economic requirements specified? | Section XVIII defines device, recurring and global deployment cost targets. |
| Are requirements consistent with the market? | Sections III and XXI relate D2 requirements to established market functions. |
| Is competitiveness claimed without evidence? | No. D2 explicitly treats competitiveness as requiring later measured validation. |

---

 # XXIV. RELATIONSHIP TO FUTURE DELIVERIES

 This D2 document establishes requirements before final implementation choices.

 **D3 — Architecture:**\
 The architecture and communication technologies shall be evaluated against the requirements defined here.

 **D4 — Hardware and Implementation:**\
 Concrete sensors, processors, communication components, battery and physical components shall be selected and evaluated against the D2 performance limits.

 **D5 — AI and Edge AI:**\
 The AI functions and performance targets shall be implemented and validated.

 **D6 — Validation and Economics:**\
 The final system performance, lifecycle economics, deployment cost and comparison with the requirements shall be evaluated.

 This sequence is intended to prevent the design from being driven solely by an initially selected development board or communication technology.

---

 # XXV. D2 REQUIREMENT SUMMARY

 | Domain | Target |
| --- | --- |
| Device sensing | Motion + positioning + proximity + device health |
| Normal inertial sampling | Up to 50 Hz |
| Event inertial sampling | Up to 100 Hz |
| Position update | 0.1–1 Hz adaptive |
| Normal telemetry packet | ≤128 B |
| Event packet | ≤512 B |
| Normal application traffic | ≤10 kbit/s/device |
| Device-edge link capacity | ≥100 kbit/s |
| Event burst capacity | ≥50 kbit/s |
| Device-edge latency | ≤2 s |
| Local event processing | ≤500 ms |
| Local wireless range | ≥10 m target |
| Offline buffering | ≥24 h |
| Deep sleep | ≤1 mW |
| Normal monitoring | ≤50 mW |
| Active sensing | ≤150 mW |
| Communication peak | ≤500 mW |
| Minimum battery autonomy | ≥7 days |
| Target battery autonomy | ≥14 days |
| Device mass | ≤100 g |
| Device volume | ≤100 cm³ |
| Operating temperature | −10 to +50 °C |
| Ingress protection | Target IP65+ |
| Edge mass, if dedicated | ≤500 g |
| Edge volume, if dedicated | ≤2 L |
| Initial cloud fleet | 100 devices |
| Scalable fleet | ≥10,000 devices |
| Cloud ingestion | ≥100 messages/s initial |
| Cloud availability | ≥99.5% |
| Cloud API p95 | ≤1 s |
| Historical retention | ≥12 months |
| Initial usable cloud storage | ≥500 GB |
| UI dashboard | ≤3 s |
| Normal UI/API payload | ≤100 kB |
| End-to-end event | ≤10 s |
| High-priority event | ≤5 s |
| AI edge inference | ≤200 ms target |
| AI validation accuracy | ≥90% initial target |
| Initial device cost | ≤€150 |
| Scaled device cost | ≤€100 objective |
| Recurring cloud/communication | ≤€10/device/month |
| Initial 100-device deployment | ≤€25,000 first-year target |

---

 # XXVI. CONCLUSION

 This D2 document establishes the functional and performance requirements for the Smart Safety & Protection IoT system.

 The target architecture consists of:

 **Device → Edge → Communication → Cloud → UI**

 The specification defines the functions of each layer and explicitly identifies the data generated, processed and exchanged between the layers.

 The document separates functional requirements from measurable performance requirements and establishes targets for:

 - computational latency;
- processing duty cycle;
- application throughput;
- communication capacity;
- communication range;
- communication latency;
- communication resilience;
- energy consumption;
- battery autonomy;
- mechanical dimensions and mass;
- environmental operation;
- cloud capacity;
- cloud storage;
- cloud availability;
- UI response time;
- event latency;
- security;
- privacy;
- AI performance;
- device cost;
- recurring operating cost; and
- global deployment cost.

 The requirements are design targets and have not yet been presented as achieved results. Their feasibility will be evaluated in subsequent project deliveries.

 The market context confirms that location tracking, geofencing, alerts, historical information and application-based monitoring are established expectations in existing commercial systems.  T-Mobile+2  SSP therefore focuses its intended differentiation on the integration of multi-source sensing, adaptive monitoring, local and edge processing, communication resilience, energy management, privacy-aware data processing and optional AI.

  The resulting requirements provide a measurable basis for the architecture, hardware selection, implementation, AI development, validation and economic evaluation of the SSP system.

---

 # REFERENCES

 \[1\] IEEE Author Center, “IEEE Article Templates,” IEEE.  IEEE Article Templates

 \[2\] IEEE Author Center, “Authoring Tools and Templates,” IEEE.  IEEE Authoring Tools and Templates

 \[3\] T-Mobile, “SyncUP KIDS Watch,” T-Mobile.  T-Mobile SyncUP KIDS Watch

 \[4\] T-Mobile, “SyncUP TRACKER,” T-Mobile Support.  T-Mobile SyncUP TRACKER

 \[5\] AngelSense, “Safeguard GPS Location Tracker,” AngelSense.  AngelSense GPS Location Tracker

 \[6\] AngelSense, “Device Specifications,” AngelSense.  AngelSense Device Specifications

 \[7\] AngelSense, “Location Update Frequency,” AngelSense Help Center.  AngelSense Location Update Frequency

 \[8\] AngelSense, “The Unique Capabilities of AngelSense,” AngelSense.  AngelSense Product Capabilities

---

 **Document status:** D2 submission version\
 **Requirement status:** Design targets to be verified in subsequent deliveries\
 **Next major activity:** D3 — Architecture and technology selection

 ### Submission note

 This version is the one I would use as the **D2 source document**. When transferring it into the official IEEE template, keep the two-column IEEE layout, add your actual author names/affiliations, and convert the section/table formatting to the template's styles. IEEE provides official Word and LaTeX templates for this purpose.  IEEE Author Center Journals+1

 The important change from the earlier D2 is that the instructor can now check the official questions almost mechanically: **every system layer has functions, every layer has defined data, functional and performance requirements are separated, every requested performance category has numerical targets, and market consistency is explicitly addressed without claiming unverified commercial superiority.**
