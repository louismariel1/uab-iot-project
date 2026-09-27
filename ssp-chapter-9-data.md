## Chapter 9 plan

 The chapter will follow the frozen structure:

 1. **9.1 Data sources** — identify every meaningful source of SSP data.
2. **9.2 Raw sensor data** — define the signals produced by the device.
3. **9.3 Device-level processing** — explain filtering, state estimation, compression and local event generation.
4. **9.4 Edge/mobile processing** — explain fusion, geofence/proximity evaluation, contextual interpretation and local decisions.
5. **9.5 Cloud processing** — explain centralized event processing, historical analysis, fleet-level information and long-term processing.
6. **9.6 AI-generated data** — distinguish sensor data from predictions, confidence values and model outputs.
7. **9.7 Alerts/events** — define the structured event model used throughout SSP.
8. **9.8 Data transmission** — explain what crosses each system boundary and why.
9. **9.9 Data storage** — distinguish temporary, operational and long-term data.
10. **9.10 Data visualization** — show how processed information becomes operator-facing information.
11. **9.11 Data lifecycle** — establish the complete generated → acquired → processed → transmitted → stored → analyzed → presented → acted-upon chain.
12. **9.12 Data privacy** — connect the data architecture to Chapter 3 privacy requirements and Chapter 4 context.

 A key principle will be:

 > **SSP does not treat all sensor data as equally valuable or equally necessary to transmit.**

 The data architecture therefore follows the same principle established by the previous chapters:

 **Sense → Filter → Interpret → Assess → Transmit selectively → Store appropriately → Analyze → Present → Act**

 The chapter will also explicitly distinguish **raw measurements**, **derived data**, **events**, **AI outputs**, **operational alerts**, and **historical records**. This distinction will become important later for Chapter 10 AI, Chapter 11 performance/energy, Chapter 12 cloud architecture, and Chapter 15 validation.

---

 # 9\. Data Flow

 # 9\. Data Flow

 ## 9.1 Data Flow Architecture

 The SSP data architecture defines how information moves through the complete IoT system from physical sensing to operational response.

 Chapter 5 established the principal system architecture:

 **Device → Edge/Mobile → Cloud → User**

 Chapters 6–8 subsequently defined the principal hardware, communication and software mechanisms supporting this architecture.

 Chapter 9 now defines the information flowing through those components.

 The purpose of this chapter is not simply to describe data transmission. It establishes the complete transformation of information through SSP:

 > **Generated → Acquired → Processed → Interpreted → Transmitted → Stored → Analyzed → Presented → Acted upon**

 The architecture is designed so that information is processed at the layer where processing provides the greatest operational benefit while respecting:

 - latency;
- energy consumption;
- communication availability;
- privacy;
- computational resources;
- security;
- scalability.

 This means that raw sensor information does not automatically need to be transmitted to the Cloud.

 Instead, SSP uses a hierarchical data-processing model:

 **Raw sensing → Device-derived information → Edge/contextual information → Cloud/system information → Operational information**

 The resulting data architecture is therefore closely coupled to the distributed Device–Edge/Mobile–Cloud architecture.

---

 ## 9.2 Data Sources

 SSP receives information from several categories of sources.

 ### 9.2.1 Device sensor data

 The monitored device provides physical and contextual measurements such as:

 - position information;
- positioning quality or confidence;
- acceleration;
- angular motion;
- device orientation where available;
- movement state;
- proximity information;
- battery state;
- device temperature where available;
- device integrity or tamper state;
- communication status.

 These measurements constitute the lowest-level operational data available to SSP.

 ### 9.2.2 Device configuration data

 The device also receives configuration information from authorized system components.

 Examples include:

 - device identity;
- operating configuration;
- sensing parameters;
- sampling configuration;
- monitoring mode;
- communication parameters;
- applicable policy identifiers;
- software and firmware version information.

 Configuration data is distinct from sensor data because it describes **how the device is expected to operate**, rather than what the physical environment is currently reporting.

 ### 9.2.3 Edge/Mobile data

 The Edge/Mobile layer can generate additional information by combining device information with local contextual information.

 Examples include:

 - current geofence status;
- proximity status;
- movement classification;
- trajectory estimate;
- local event status;
- communication state;
- local risk indicators;
- confidence-adjusted interpretations.

 ### 9.2.4 Cloud and system-level data

 The Cloud can contribute information that is not available to an individual device.

 Examples include:

 - historical device activity;
- previously generated events;
- fleet-level information;
- configured geographical policies;
- user and role information;
- device-management information;
- model versions;
- operational rules;
- historical analytical results.

 The Cloud therefore provides the system-wide context required for functions that cannot be performed reliably using only local information.

 ### 9.2.5 User-generated information

 Authorized operators and administrators can also generate data through the SSP user interfaces.

 Examples include:

 - configuration changes;
- policy changes;
- acknowledgement of alerts;
- operator annotations;
- administrative actions;
- device-management commands;
- investigation records.

 User-generated information therefore becomes part of the system's operational history.

---

 ## 9.3 Raw Sensor Data

 Raw sensor data represents measurements as they are acquired from physical sensing or positioning subsystems before significant interpretation has taken place.

 Typical raw or near-raw information may include:

 | Source | Example data | Typical purpose |
| --- | --- | --- |
| Positioning subsystem | Latitude, longitude, timestamp | Position estimation |
| Positioning subsystem | Accuracy/confidence information | Position-quality assessment |
| Accelerometer | X/Y/Z acceleration | Motion analysis |
| Gyroscope | X/Y/Z angular velocity | Orientation/motion analysis |
| Proximity subsystem | Presence/distance indication | Local proximity assessment |
| Battery subsystem | Voltage/state estimate | Energy management |
| Device integrity subsystem | Tamper/state indicators | Security monitoring |
| Communication subsystem | Link/status information | Connectivity management |

Raw data is normally associated with a timestamp and device identity.

 Where appropriate, it may also include:

 - measurement quality;
- sensor status;
- sequence number;
- acquisition mode;
- firmware/software version;
- synchronization information.

 The timestamp is particularly important because SSP must correlate information from sensors that do not necessarily produce measurements at exactly the same time.

 Raw data should therefore be considered a **measurement record**, not automatically an operational event.

 For example:

 > An accelerometer measurement of increased acceleration is not by itself equivalent to an abnormal movement event.

 Additional processing may be required before an operational interpretation is justified.

---

 ## 9.4 Device-Level Processing

 The device performs initial processing before information is transmitted to higher layers.

 This processing serves four principal purposes:

 1. reduce unnecessary data;
2. identify immediately relevant local conditions;
3. reduce communication and energy requirements;
4. provide continued functionality during communication disruption.

 ### 9.4.1 Signal conditioning

 Where appropriate, raw sensor measurements may undergo local conditioning such as:

 - filtering;
- range checking;
- outlier detection;
- timestamp validation;
- sensor-status checking;
- basic calibration compensation.

 The objective is to prevent obviously invalid measurements from being treated as valid operational information.

 ### 9.4.2 Local feature extraction

 The device may calculate compact features rather than continuously transmitting raw samples.

 Examples include:

 - acceleration magnitude;
- movement intensity;
- stationary/moving state;
- orientation change;
- local motion statistics;
- battery trend;
- communication quality indicators.

 This can substantially reduce the amount of information that must cross the device communication boundary.

 ### 9.4.3 Local state estimation

 The device may maintain a local operational state such as:

 - stationary;
- normal movement;
- elevated movement;
- communication degraded;
- low battery;
- tamper suspected;
- monitoring active;
- monitoring reduced.

 These states can influence subsequent sensing and communication behavior.

 ### 9.4.4 Local event pre-processing

 Where sufficiently clear conditions exist, the device can generate preliminary events.

 Examples include:

 - device tamper indication;
- abnormal sensor condition;
- low battery;
- communication degradation;
- device fault;
- locally detected movement transition.

 The device-generated information does not necessarily constitute a final operational decision.

 Instead, the device can provide a structured observation to the Edge/Mobile or Cloud layer.

 ### 9.4.5 Local data buffering

 The device shall support temporary buffering of relevant information when communication is unavailable or degraded, subject to the available memory and configured retention policy.

 This supports the Chapter 3 requirements for:

 - communication-loss operation;
- event preservation;
- graceful degradation;
- recovery.

 The buffering strategy should prioritize operationally important information rather than treating every measurement equally.

---

 ## 9.5 Edge/Mobile Processing

 The Edge/Mobile layer provides an intermediate processing environment between the constrained device and the Cloud.

 Depending on the deployment configuration, this layer may be implemented by a mobile device, gateway or another authorized edge-processing platform.

 Its primary purpose is to combine information that can be processed locally without requiring continuous Cloud interaction.

 ### 9.5.1 Data aggregation

 The Edge/Mobile layer can collect information from one or more device sources and organize it into a consistent local data stream.

 This may include:

 - position;
- movement;
- proximity;
- device state;
- communication state;
- timestamps;
- device confidence information.

 ### 9.5.2 Sensor and context fusion

 The Edge/Mobile layer can combine multiple information sources.

 For example:

 **Position + motion + proximity + position confidence**

 may provide a more informative representation of a situation than any individual measurement.

 This supports the requirement established in Chapter 3 that uncertain positioning should not automatically be treated as equivalent to high-confidence positioning.

 ### 9.5.3 Geographical rule evaluation

 The Edge/Mobile layer can evaluate configured geographical rules when local processing provides an operational benefit.

 These rules may include:

 - inclusion zones;
- exclusion zones;
- permitted areas;
- restricted areas;
- boundary conditions;
- proximity-related geographical rules.

 The output is not necessarily a final alert.

 For example:

 > **Geofence boundary crossed**

 is an event condition.

 Its operational significance may depend on:

 - movement direction;
- speed;
- position confidence;
- proximity;
- persistence of the condition;
- configured policy.

 ### 9.5.4 Local contextual interpretation

 The Edge/Mobile layer can combine multiple observations into a contextual state.

 For example:

 **Position outside permitted zone**

 - **high position confidence**
- **movement toward restricted area**
- **relevant proximity condition**

 may produce a more significant event than a low-confidence isolated boundary observation.

 This is one of the principal reasons for maintaining an Edge/Mobile processing layer.

 ### 9.5.5 Local decision capability

 Where defined by the operational policy, the Edge/Mobile layer can generate or escalate an event without waiting for Cloud processing.

 This can reduce:

 - end-to-end latency;
- dependence on wide-area connectivity;
- unnecessary communication;
- exposure of raw sensitive information.

 The exact decision logic and AI functions are developed further in Chapter 10.

---

 ## 9.6 Cloud Processing

 The Cloud provides centralized processing and system-wide information management.

 The Cloud is not intended to receive every raw sensor sample by default.

 Instead, it primarily receives information required for:

 - operational monitoring;
- centralized event management;
- historical analysis;
- fleet management;
- long-term storage;
- reporting;
- model management;
- system-wide analytics;
- integration with authorized external systems.

 ### 9.6.1 Event correlation

 The Cloud can correlate information across time and across devices.

 For example, it may combine:

 - current event;
- historical events;
- device state;
- policy configuration;
- previous communication status;
- relevant operational records.

 ### 9.6.2 Historical analysis

 Historical information allows SSP to analyze patterns that cannot be identified reliably from a single observation.

 Potential applications include:

 - recurring boundary events;
- communication reliability;
- device health;
- battery behavior;
- repeated anomalies;
- fleet-level performance;
- system utilization.

 ### 9.6.3 Fleet-level processing

 The Cloud can aggregate information from multiple deployed devices.

 This supports:

 - fleet health monitoring;
- device comparison;
- configuration management;
- operational reporting;
- model monitoring;
- maintenance planning.

 ### 9.6.4 Policy management

 The Cloud provides a centralized location for authorized policies such as:

 - geographical rules;
- notification policies;
- device configurations;
- retention policies;
- user permissions;
- monitoring modes.

 Policies can subsequently be distributed to the appropriate system layers.

 ### 9.6.5 Model and analytics management

 Where AI is used, the Cloud can manage:

 - training datasets;
- model versions;
- model evaluation results;
- deployment configurations;
- model performance;
- rollback information.

 Detailed AI data flows are defined in Chapter 10.

---

 ## 9.7 AI-Generated Data

 AI-generated information is treated as **derived information**, not as a replacement for the underlying measurements.

 Potential AI outputs include:

 - movement classification;
- predicted trajectory;
- predicted boundary crossing;
- anomaly score;
- risk indicator;
- event classification;
- confidence score;
- uncertainty estimate.

 For example:

 **Raw data**

 → position sequence + motion data

 **Derived features**

 → speed + direction + acceleration characteristics

 **AI output**

 → predicted trajectory

 **AI confidence**

 → confidence/uncertainty associated with prediction

 **Operational interpretation**

 → predicted approach to restricted area

 This distinction is important because an AI prediction should not automatically be treated as an established fact.

 Where an AI model produces low-confidence results, SSP shall apply the confidence information according to the applicable decision policy.

 The data model should therefore preserve, where applicable:

 - model identifier;
- model version;
- input-data reference;
- prediction;
- confidence;
- uncertainty;
- timestamp;
- processing location.

 This enables later analysis of both successful and unsuccessful predictions.

---

 ## 9.8 Events and Alerts

 SSP distinguishes between a **measurement**, an **event**, and an **alert**.

 ### Measurement

 A measurement is an observation produced by a sensor or subsystem.

 Example:

 > Position = defined coordinate at time T.

 ### Event

 An event is a structured interpretation of one or more observations.

 Example:

 > Device entered exclusion zone.

 ### Alert

 An alert is an operational notification generated when an event satisfies a configured operational condition.

 Example:

 > High-priority alert: device entering restricted area with high-confidence position and relevant proximity condition.

 This distinction prevents the system from treating every measurement as an operational incident.

 ### 9.8.1 Event structure

 A general SSP event should contain, where applicable:

 - event identifier;
- device identifier;
- timestamp;
- event type;
- event severity;
- event status;
- location;
- position confidence;
- relevant movement information;
- proximity information;
- source layer;
- supporting observations;
- AI output where applicable;
- AI confidence where applicable;
- policy/rule identifier;
- communication state;
- processing timestamp.

 ### 9.8.2 Event lifecycle

 An event can progress through states such as:

 **Detected → Assessed → Reported → Acknowledged → Resolved/Closed**

 The exact state model depends on the operational application.

 ### 9.8.3 Alert prioritization

 Alerts should be prioritized according to operational significance.

 A conceptual hierarchy is:

 **Routine → Elevated → Critical**

 This does not imply that every system deployment must use exactly three levels. The actual classification shall be configurable according to the operational scenario.

---

 ## 9.9 Data Transmission

 Data transmission occurs across several system boundaries.

 The principal communication paths are:

 **Device ↔ Edge/Mobile**

 **Edge/Mobile ↔ Cloud**

 **Cloud ↔ Authorized User**

 Each boundary should carry only information required by the receiving layer.

 ### 9.9.1 Device to Edge/Mobile

 The Device may transmit:

 - current or recent position;
- position confidence;
- selected motion information;
- proximity status;
- device state;
- battery status;
- locally detected events;
- health information.

 Raw high-frequency sensor streams should not be transmitted continuously unless required for a defined function.

 ### 9.9.2 Edge/Mobile to Cloud

 The Edge/Mobile layer may transmit:

 - contextual state;
- structured events;
- alerts;
- selected measurements;
- summarized sensor information;
- device health information;
- buffered events;
- synchronization information.

 The objective is to transmit information that provides system-wide value rather than simply forwarding everything received from the device.

 ### 9.9.3 Cloud to User

 The Cloud provides authorized users with:

 - current device status;
- event information;
- alerts;
- location information where authorized;
- historical information;
- system health;
- configuration status;
- operational analytics.

 ### 9.9.4 Cloud to Device/Edge

 Feedback and control information can flow in the opposite direction.

 Examples include:

 - configuration updates;
- geographical policies;
- monitoring-mode changes;
- notification policies;
- software/firmware update instructions;
- time synchronization;
- operational commands.

 Thus the complete architecture is not a one-way pipeline.

 It is better represented as:

 **Device ⇄ Edge/Mobile ⇄ Cloud ⇄ User**

 with control and configuration information flowing in the reverse direction.

---

 ## 9.10 Data Storage

 SSP uses multiple levels of data persistence.

 ### 9.10.1 Temporary device storage

 The device may temporarily retain:

 - recent measurements;
- important events;
- communication-failure records;
- device-state information.

 This storage exists primarily to support continuity and recovery.

 ### 9.10.2 Edge/Mobile storage

 The Edge/Mobile layer may temporarily retain:

 - recent event history;
- locally generated events;
- buffered information;
- synchronization state;
- temporary processing data.

 The duration should be limited according to operational requirements.

 ### 9.10.3 Cloud operational storage

 The Cloud provides persistent storage for information required for normal system operation.

 Examples include:

 - device registry;
- current device state;
- active events;
- alert records;
- configuration;
- users and roles;
- operational metadata.

 ### 9.10.4 Historical storage

 Longer-term storage can support:

 - historical event analysis;
- reporting;
- system performance analysis;
- maintenance;
- AI development where appropriately authorized;
- auditability.

 Historical retention shall be governed by the applicable policy and regulatory requirements.

 ### 9.10.5 Storage principle

 SSP should not retain all generated information indefinitely.

 The storage architecture should distinguish:

 **Operational necessity**

 from

 **historical usefulness**

 from

 **regulatory/audit requirement**

 from

 **unnecessary data retention**

 This supports the data-minimization and retention requirements defined in Chapter 3.

---

 ## 9.11 Data Visualization

 Processed information is ultimately presented to authorized users through the SSP user/interface layer.

 The objective is not to expose all available technical data.

 Instead, the interface should present information appropriate to the user's operational role.

 ### 9.11.1 Operational dashboard

 An operational dashboard may present:

 - active devices;
- device status;
- current alerts;
- event locations;
- severity;
- communication status;
- battery status;
- relevant contextual information.

 ### 9.11.2 Event view

 An operator investigating an event may require:

 - event type;
- event time;
- location;
- position confidence;
- movement information;
- proximity information;
- relevant historical events;
- event status;
- supporting evidence.

 ### 9.11.3 Historical visualization

 Historical information may be represented through:

 - event timelines;
- geographical tracks;
- event frequency;
- communication history;
- battery trends;
- device-health indicators.

 ### 9.11.4 Role-based presentation

 Different users may receive different information.

 For example:

 **Operator → Operational events and alerts**

 **Administrator → Configuration and fleet information**

 **Technical administrator → Diagnostics and device health**

 **Authorized analyst → Historical and aggregated information**

 This implements the role-based access principle established in Chapters 3 and 4.

---

 ## 9.12 Complete SSP Data Lifecycle

 The complete SSP data lifecycle can be represented as:

 **Generated**

 Physical sensors and system components generate measurements.

 ↓

 **Acquired**

 The device acquires and timestamps the measurements.

 ↓

 **Processed**

 Filtering, validation and local feature extraction are performed.

 ↓

 **Interpreted**

 Device and Edge/Mobile processing convert measurements into contextual information.

 ↓

 **Assessed**

 Rules, contextual logic and, where justified, AI determine the significance of the information.

 ↓

 **Transmitted**

 Only information required by the next system layer is communicated.

 ↓

 **Stored**

 Operationally and historically relevant information is stored according to policy.

 ↓

 **Analyzed**

 The Cloud performs centralized and historical analysis.

 ↓

 **Presented**

 Relevant information is presented to authorized users.

 ↓

 **Acted upon**

 Operators or authorized systems respond to the resulting event or alert.

 ↓

 **Feedback**

 Configuration, policy and operational decisions can influence subsequent device and system behavior.

 The complete conceptual flow is therefore:

 > **Generated → Acquired → Processed → Interpreted → Assessed → Transmitted → Stored → Analyzed → Presented → Acted upon → Feedback**

 This is the central data-flow model for SSP.

---

 ## 9.13 Data Prioritization

 Not all information has the same operational importance.

 SSP therefore applies a conceptual hierarchy to data transmission and processing.

 | Information type | Typical priority | Processing objective |
| --- | --- | --- |
| Critical event | Immediate | Operational response |
| High-severity contextual event | High | Rapid assessment |
| Device fault | High | Reliability/maintenance |
| Low-battery warning | Medium/High | Resource management |
| Routine status | Normal | Monitoring |
| Historical raw data | Low/conditional | Analysis when required |

This prioritization supports the communication and energy requirements established in Chapter 3.

 For example, a critical event may justify immediate transmission even when communication is energy-intensive, whereas routine measurements may be aggregated or transmitted less frequently.

 The precise prioritization policy will be defined in conjunction with the communication and operational policies.

---

 ## 9.14 Data Reduction and Aggregation

 One of the principal advantages of the distributed SSP architecture is that data can be reduced before transmission.

 A conceptual example is:

 **100 raw sensor samples**

 ↓

 **Local filtering**

 ↓

 **10 derived features**

 ↓

 **1 contextual state**

 ↓

 **1 operational event if required**

 This does not mean that raw information is always discarded.

 Where raw information is required for:

 - diagnostics;
- model development;
- validation;
- forensic analysis;
- troubleshooting;

 it may be retained or transmitted according to an explicit policy.

 The important principle is that **raw data availability and raw data transmission are separate decisions**.

 This distinction contributes to:

 - lower communication energy;
- lower bandwidth requirements;
- reduced Cloud processing;
- reduced storage;
- improved privacy.

---

 ## 9.15 Data Synchronization

 Because SSP is distributed across Device, Edge/Mobile and Cloud, the system must maintain sufficient synchronization to correctly interpret events.

 Relevant synchronization information includes:

 - timestamps;
- sequence numbers;
- device identifiers;
- event identifiers;
- processing timestamps;
- synchronization state.

 When communication is temporarily unavailable, information generated locally may be transmitted later.

 The receiving layer must therefore be capable of distinguishing:

 **event occurrence time**

 from

 **event transmission time**

 from

 **event processing time**

 For example:

 > Event occurred at 14:02:15.

 > Communication restored at 14:03:10.

 > Event received by Cloud at 14:03:11.

 These timestamps describe different stages of the same event and should not be treated as interchangeable.

---

 ## 9.16 Data Integrity and Provenance

 SSP data should retain sufficient metadata to establish where and how important information was generated.

 Where appropriate, data records should identify:

 - source device;
- source subsystem;
- timestamp;
- processing layer;
- software/model version;
- configuration or policy version;
- event identifier;
- confidence information.

 This supports:

 - troubleshooting;
- validation;
- security investigation;
- auditability;
- AI model evaluation;
- requirements verification.

 For example, an AI-generated prediction should be traceable to the model version and relevant input information that produced it.

 Similarly, an operational alert should be traceable to the event and policy condition that caused it.

---

 ## 9.17 Data Privacy

 Privacy is integrated into the SSP data-flow architecture rather than added only after data has reached the Cloud.

 The fundamental principle is:

 > **Collect and transmit only the information required for the authorized function.**

 ### 9.17.1 Data minimization

 Where a derived result is sufficient for an operational function, transmitting raw information may be unnecessary.

 For example:

 **Raw accelerometer stream**

 may not need to be transmitted if:

 **Movement state = stationary**

 is sufficient for the receiving layer.

 ### 9.17.2 Local processing

 Sensitive information should, where practical and operationally appropriate, be processed as close to the source as possible.

 This can reduce unnecessary exposure of:

 - precise location;
- movement history;
- proximity information;
- raw sensor information.

 ### 9.17.3 Context-dependent transmission

 The amount of information transmitted can vary according to operational state.

 A conceptual policy is:

 **Normal state**

 → minimal status information

 **Elevated state**

 → additional contextual information

 **Critical state**

 → information required for authorized operational response

 This implements the privacy-aware communication principle established in Chapters 3 and 4.

 ### 9.17.4 Access control

 Data should be accessible according to:

 - user identity;
- role;
- operational responsibility;
- data sensitivity;
- applicable policy.

 ### 9.17.5 Retention

 Data retention shall be explicitly defined.

 Information should not be retained indefinitely merely because storage capacity is available.

 Retention periods shall instead be determined according to:

 - operational requirements;
- security requirements;
- audit requirements;
- applicable legal/regulatory requirements;
- legitimate analytical requirements.

---

 ## 9.18 Data Security

 Data security applies throughout the complete lifecycle.

 Protection is required:

 **At generation**

 → trusted device identity and protected sensing/processing environment

 **During transmission**

 → authentication, integrity and confidentiality mechanisms

 **During storage**

 → access control and appropriate data protection

 **During processing**

 → controlled execution and authorization

 **During presentation**

 → role-based access and secure interfaces

 **During deletion/retention**

 → controlled lifecycle management

 The data architecture therefore reinforces the Chapter 3 security requirements rather than treating security as a separate Cloud function.

---

 ## 9.19 Data Flow During Communication Failure

 Communication failure is treated as an expected engineering condition.

 ### Device-to-Edge failure

 The device should:

 - detect the communication problem;
- continue appropriate local monitoring;
- buffer important information;
- attempt recovery according to the communication policy.

 ### Edge-to-Cloud failure

 The Edge/Mobile layer should:

 - continue local processing where required;
- retain important events;
- avoid unnecessary loss of information;
- forward buffered information when connectivity returns.

 ### Cloud-to-User disruption

 The Cloud should retain operational information even if an individual user interface is temporarily unavailable.

 Where required by the application, local or alternative notification mechanisms may be used.

 The objective is therefore:

 > **Communication failure should reduce functionality only to the extent that the failed communication path actually prevents the affected function from operating.**

 This is consistent with the graceful-degradation principle established in Chapter 3.

---

 ## 9.20 Data Flow for a Representative Event

 A representative perimeter event can illustrate the complete architecture.

 ### Step 1 — Physical observation

 The device acquires:

 - position;
- position confidence;
- motion information;
- proximity information.

 ### Step 2 — Device processing

 The device validates measurements and derives relevant local movement information.

 ### Step 3 — Edge processing

 The Edge/Mobile layer combines:

 **Position + confidence + movement + proximity + geographical policy**

 ### Step 4 — Contextual assessment

 The system determines that the device is approaching a restricted condition.

 ### Step 5 — Event generation

 A structured event is generated containing:

 - event type;
- timestamp;
- location;
- confidence;
- movement state;
- relevant context.

 ### Step 6 — Severity assessment

 The system determines the operational significance according to configured rules and, where applicable, AI-supported assessment.

 ### Step 7 — Selective transmission

 The relevant event and supporting information are transmitted to the Cloud.

 Unnecessary raw sensor streams are not automatically transmitted.

 ### Step 8 — Cloud processing

 The Cloud records the event, correlates it with historical and system-wide information, and makes it available to authorized users.

 ### Step 9 — Alert

 If the configured conditions are satisfied, an operational alert is generated.

 ### Step 10 — User response

 The authorized operator receives the alert and accesses the contextual information required for the operational response.

 ### Step 11 — Historical record

 The event and its relevant lifecycle information are retained according to the applicable policy.

 This example demonstrates how SSP transforms raw measurements into an operationally meaningful result.

---

 ## 9.21 Data Flow and the Device–Edge–Cloud Allocation

 The data architecture reinforces the following functional allocation:

 | Function | Device | Edge/Mobile | Cloud |
| --- | --- | --- | --- |
| Sensor acquisition | Primary | — | — |
| Basic filtering | Primary | Secondary | — |
| Local state estimation | Primary | Primary | — |
| Geofence evaluation | Possible | Primary | Secondary |
| Proximity interpretation | Primary | Primary | Secondary |
| Event pre-processing | Primary | Primary | — |
| Contextual assessment | Limited | Primary | Primary |
| Historical analysis | — | Limited | Primary |
| Fleet analytics | — | — | Primary |
| Long-term storage | Temporary | Temporary | Primary |
| Model management | — | — | Primary |
| Low-latency decisions | Primary/limited | Primary | Secondary |
| System-wide decisions | — | — | Primary |
| User visualization | — | Possible | Primary |
| Configuration management | Receives | Applies/forwards | Primary |

The table is not intended to imply that a function can exist at only one layer.

 Instead, it identifies the **preferred architectural location** based on the principles established in Chapters 3–5.

---

 ## 9.22 Data Flow and Energy Management

 The data architecture directly influences energy consumption.

 A simplified relationship is:

 > **More sensing → more processing → more communication → greater energy consumption**

 SSP therefore seeks to reduce unnecessary data movement.

 Examples include:

 - reducing sensor sampling when high-rate sensing is unnecessary;
- extracting local features instead of transmitting raw samples;
- aggregating routine information;
- transmitting events immediately when operationally necessary;
- reducing communication frequency during low-risk states;
- preserving high-intensity operation for conditions where it provides measurable value.

 This supports the Chapter 3 energy principle:

 **Risk/context → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

 The quantitative evaluation of this relationship is deferred to Chapter 11.

---

 ## 9.23 Data Flow and AI

 The data architecture establishes the inputs and outputs required by Chapter 10.

 The general AI data path is:

 **Sensor data**

 → **pre-processing**

 → **features**

 → **AI model**

 → **prediction/classification**

 → **confidence/uncertainty**

 → **contextual decision**

 → **event/alert**

 The model should not be considered independently from the data pipeline.

 AI performance depends on:

 - data quality;
- sampling;
- feature quality;
- synchronization;
- labeling;
- environmental conditions;
- model version;
- confidence interpretation.

 Chapter 10 will therefore build upon the data structures established here rather than defining an independent data path.

---

 ## 9.24 Data Flow and Cloud Architecture

 The information identified in this chapter establishes the principal inputs to Chapter 12.

 The Cloud must ultimately provide appropriate mechanisms for:

 - device registration;
- event ingestion;
- operational state management;
- historical storage;
- event processing;
- user access;
- configuration;
- analytics;
- AI/model management;
- auditability.

 Chapter 12 will therefore refine the logical data flows described here into concrete backend services, APIs, databases and storage mechanisms.

---

 ## 9.25 Data Flow and Validation

 The data architecture also provides a direct basis for testing.

 Important validation questions include:

 - Is sensor information acquired correctly?
- Are timestamps preserved?
- Are invalid measurements detected?
- Are events generated correctly?
- Is position confidence propagated?
- Is unnecessary raw data transmitted?
- Are critical events transmitted within the required latency?
- Are events preserved during communication loss?
- Is stored information complete and consistent?
- Can an alert be traced back to its originating observations?
- Are unauthorized users prevented from accessing sensitive information?
- Are retention and deletion policies correctly applied?

 These questions will be converted into measurable tests in Chapter 15.

---

 ## 9.26 Preliminary Data Model

 At the logical level, SSP can distinguish the following principal information entities:

 | Entity | Purpose |
| --- | --- |
| Device | Represents the monitored physical device |
| Measurement | Represents a sensor or subsystem observation |
| Position record | Represents a location observation and its confidence |
| Device state | Represents the current operational state |
| Event | Represents a meaningful interpreted condition |
| Alert | Represents an operational notification |
| Policy | Defines applicable monitoring or decision rules |
| User | Represents an authorized system user |
| Configuration | Represents device/system configuration |
| AI prediction | Represents an AI-generated output |
| Model | Identifies the AI model/version |
| Audit record | Represents significant security/operational actions |

The final physical database schema will be developed in Chapter 12.

---

 ## 9.27 Summary of the SSP Data Strategy

 The SSP data architecture is based on six principal principles.

 ### 1\. Process information progressively

 Raw measurements should be transformed into increasingly meaningful information as they move through the system.

 ### 2\. Process locally when beneficial

 Information should be processed at the Device or Edge/Mobile layer when this provides measurable benefits in latency, energy, resilience or privacy.

 ### 3. Transmit selectively

 The system should not transmit information merely because it is available.

 ### 4\. Preserve context and confidence

 Important decisions should retain information about measurement quality, processing conditions and AI confidence where applicable.

 ### 5\. Store according to purpose

 Temporary, operational and historical data should be treated differently.

 ### 6\. Protect information throughout its lifecycle

 Security and privacy should apply from data generation through transmission, processing, storage, visualization and eventual deletion.

 The resulting SSP data-flow concept is:

 > **Physical sensing → Local processing → Contextual interpretation → Event/risk assessment → Selective communication → Cloud/system processing → Authorized visualization → Operational action**

---

 ## 9.28 Chapter 9 Conclusion

 Chapter 9 establishes the information architecture of SSP.

 The principal conclusion is that SSP should not be designed as a simple pipeline in which all sensor information is continuously transmitted to a central server.

 Instead, the system uses a hierarchical data-flow model:

 **Device → Edge/Mobile → Cloud → User**

 with processing and feedback distributed according to operational requirements.

 At the Device level, SSP acquires and preprocesses physical information.

 At the Edge/Mobile level, it combines sensor information, contextual information, geographical rules and local state to produce more meaningful interpretations.

 At the Cloud level, it provides centralized storage, historical analysis, fleet-level processing, policy management and system-wide intelligence.

 At the User level, it presents only the information required for the authorized operational role.

 The complete information lifecycle can therefore be summarized as:

 > **Generated → Acquired → Processed → Interpreted → Assessed → Transmitted → Stored → Analyzed → Presented → Acted upon → Feedback**

 This architecture also establishes an important distinction between:

 **measurement → derived information → event → alert → operational action**

 which prevents raw sensor observations from automatically being treated as security incidents.

 The data architecture further supports the central SSP principles established in earlier chapters:

 - distributed intelligence;
- adaptive monitoring;
- contextual event interpretation;
- communication resilience;
- energy-aware operation;
- privacy-aware information flow;
- security throughout the data lifecycle;
- scalable Cloud processing.

 The chapter also establishes the information structures required by the subsequent engineering work.

 Chapter 10 will build on this foundation to define **which SSP functions genuinely require AI, what data they consume, what outputs they produce, where the models execute, and how confidence and failure are handled**.

 Chapter 11 will then quantify the relationship between the data-flow strategy, communication activity, processing load, latency and energy consumption.

 Chapter 12 will translate the Cloud-side data requirements into the concrete backend, API, database, storage and service architecture.

 The resulting progression is:

 **Requirements → Architecture → Hardware → Communication → Software → Data Flow → AI → Energy/Performance → Cloud → PoC → Business/Costs → Validation**
