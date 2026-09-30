 ## TD1 — Update plan

 The final D2 will use the improved logical progression we established:

 **Chapter 1 → SSP concept, motivation and objectives**\
 **Chapter 2 → Users, use cases and operational scenarios**\
 **Chapter 3 → SSP functional and performance requirements**\
 **Chapter 4 → Existing solutions, comparison context and improvement opportunities**

 The useful content from the previous D2 will be integrated as follows:

 - **Previous functional requirements** → Chapter 3, but reorganized so they are derived from the Chapter 2 scenarios rather than presented as an isolated catalogue.
- **Previous data specifications** → Chapter 3, including data types, logical representations, packet sizes, sampling, traffic volumes and storage requirements.
- **Previous quantitative performance targets** → Chapter 3.
- **Energy requirements** → Chapter 3, linked explicitly to adaptive monitoring.
- **Communication resilience** → Chapter 2 as an operational scenario and Chapter 3 as formal requirements.
- **Security and privacy** → Chapter 3 as cross-cutting requirements.
- **AI scope and targets** → Chapter 3, without prescribing the future AI architecture.
- **Economic requirements** → Chapter 3.
- **Functional/performance separation** → explicitly maintained throughout Chapter 3.
- **Engineering trade-offs** → incorporated where they help justify requirements, using formal relationships such as `monitoring intensity ↔ responsiveness ↔ energy consumption`.
- **Requirement traceability** → incorporated at the end of Chapter 3, linking scenarios to requirements and later verification.
- **Market observations** → Chapter 4, retaining only information that helps establish the state of existing solutions and justify improvement opportunities.
- **Market competitiveness claims** → removed unless supported by later measured evidence.
- **Architecture descriptions** → removed from D2. Chapter 2 may show conceptual operational flows, but **no Device–Edge–Cloud architecture design** will be specified.
- **Future deliverables** → a short closing section will state that D3 addresses architecture, D4 implementation/hardware, etc., without incorporating those designs into D2.

 The resulting scientific progression will therefore be:

 **SSP problem and objectives → operational use → requirements → existing solutions and improvement opportunities**

 rather than:

 **SSP → architecture → functions → market.**

---

 # TD2 — Final Updated D2

 # SSP — Smart Safety & Protection IoT System

 ## D2 — Functional and Performance Specifications

 **Academic Year:** 2026/2027\
 **Course:** UAB 105075 — IoT Design Project\
 **Deliverable:** D2 — Functional and Performance Specifications\
 **Acronym:** SSP\
 **IoT Group 14:** Louis-Marie Loe, Cheong Travis

---

 # Abstract

 This document defines the functional and performance specifications of the proposed Smart Safety & Protection (SSP) IoT system. SSP is conceived as a distributed safety-monitoring system intended to provide authorized users with relevant information concerning the location, movement, proximity, risk-related events and operational state of a monitored person or protected entity.

 The purpose of D2 is to establish a scientifically structured and measurable requirements baseline before the detailed system architecture and implementation are designed. The document therefore distinguishes the motivation and objectives of SSP from the operational scenarios through which the system is expected to be used, and from the functional and performance requirements derived from those scenarios.

 The specification considers sensing, local processing, communication, edge processing, cloud services and user interaction as system capabilities without defining their final architectural implementation. Detailed architecture and technology selection are outside the scope of D2 and will be addressed in the subsequent architecture deliverable.

 Particular attention is given to adaptive monitoring, distributed processing, energy-efficient operation, communication resilience, privacy-aware information processing, contextual event interpretation, security, scalability and optional AI-assisted processing. These characteristics are formulated as engineering requirements and measurable targets rather than as claims of already-achieved performance.

 The requirements established in this document will provide the basis for subsequent architecture, implementation, AI development, validation and economic evaluation activities.

 **Index Terms—** Internet of Things, IoT, safety monitoring, protection system, wearable device, location monitoring, motion sensing, edge computing, cloud computing, adaptive monitoring, privacy-aware processing, event detection, energy efficiency.

---

 # 1\. Introduction, Motivation and SSP Objectives

 ## 1.1 Motivation

 Safety-monitoring applications may require continuous or periodic information concerning the location, movement, proximity and operational condition of a monitored person or protected entity. However, the usefulness of such a system does not depend solely on the acquisition of sensor measurements. Sensor information must be transformed into relevant operational information, abnormal conditions must be identified, and appropriate information must be made available to authorized users with sufficient timeliness and reliability.

 A conventional monitoring system may treat sensing and communication primarily as a data-collection problem. SSP instead considers monitoring as an adaptive and context-dependent process in which the intensity of sensing, processing and communication can vary according to the current operational situation.

 The resulting conceptual progression is:

 **Physical situation → sensing → information processing → event interpretation → authorized information → operational response**

 This progression establishes the fundamental motivation for SSP.

 ## 1.2 SSP Concept

 The Smart Safety & Protection system is conceived as an IoT-based monitoring solution capable of observing relevant physical and operational conditions and transforming them into information that can support safety-related decisions.

 The system is intended to support situations in which location information is relevant, movement or inactivity may provide contextual information, proximity may contribute to event detection, device status must be monitored, communication may temporarily become unavailable, and sensitive information must be appropriately protected.

 SSP is therefore not defined merely as a location-tracking device. Its intended functionality includes sensing, local processing, adaptive monitoring, event detection, resilient information handling, controlled information access and centralized management.

 ## 1.3 Purpose of D2

 The purpose of D2 is to translate the SSP concept into a formal requirements specification.

 The document establishes:

 **SSP objectives → operational scenarios → functional requirements → performance requirements → verification targets**

 The requirements are intended to guide subsequent engineering work while avoiding premature commitment to particular hardware components, communication technologies, cloud services or machine-learning models.

 Architecture design is outside the scope of D2. The architecture will be developed in the subsequent D3 deliverable using the requirements established here.

 ## 1.4 Scope

 The D2 specification covers the expected behaviour and measurable requirements of the SSP system, including sensing, monitoring, event detection, information processing, communication, resilience, energy consumption, security, privacy, cloud services, user interaction, AI-related capabilities and economic constraints.

 The specification describes the target system rather than limiting itself to a particular laboratory prototype. A prototype implementation may temporarily realize some functions using development boards, smartphones, computers or other available equipment. Such implementation choices do not redefine the target requirements.

 ## 1.5 SSP Improvement Objectives

 SSP is intended as an improved IoT safety and protection system building on functions already established in existing monitoring and tracking solutions. The objective of D2 is not to claim that these improvements have already been achieved, but to translate the intended improvements into measurable engineering requirements that can be evaluated during subsequent project deliveries.

 The intended improvements concern several complementary aspects of system operation.

 At the device level, SSP shall support local preprocessing, adaptive sensing, selected event detection, device-state monitoring, temporary buffering and energy-aware operation. The purpose is to reduce unnecessary communication and energy consumption while maintaining useful monitoring during temporary connectivity interruptions.

 At the edge level, SSP shall support functions beyond simple data forwarding. Relevant information may be validated, filtered, aggregated, interpreted and temporarily stored before being transmitted to centralized services. This is intended to reduce unnecessary cloud traffic and support low-latency operation.

 At the cloud level, SSP shall provide centralized historical information, event processing, fleet management, controlled access, auditing, scalable data ingestion and authorized interfaces. The cloud environment shall support deployment across geographically distributed use cases without requiring each deployment to maintain its own physical cloud infrastructure.

 Privacy is treated as a system-level requirement. Where a required function can be achieved using processed, summarized or event-oriented information rather than continuously transmitting raw sensor data, the lower-data approach shall be preferred, subject to functional requirements.

 AI is considered a distributed capability that may be used at different processing stages according to computational resources, latency, energy, connectivity, privacy and model-complexity constraints. D2 therefore specifies AI capabilities and measurable targets without prescribing a final machine-learning model or architecture.

 Energy efficiency is treated as a system-level design objective. Adaptive sensing, local processing, low-power operation and event-driven communication shall be considered together when defining the energy requirements of the system.

 The intended improvements are consequently evaluated through measurable engineering outcomes rather than through unsupported claims of superiority.

---

 # 2\. Target Users, Use Cases and Operational Scenarios

 ## 2.1 SSP Actors and Users

 The principal actors provide the vocabulary required to describe SSP operation.

 The **protected person** is the person for whom a protection perimeter or safety-related monitoring service is provided.

 The **monitored person** is the person or entity whose location, movement or operational state is subject to an authorized monitoring rule.

 The **protection operator** monitors the system, reviews alerts and performs the operational actions associated with detected events.

 The **system administrator** manages users, devices, policies and system configuration according to the authorization model.

 The **authorized organization** is the institution responsible for deploying and operating SSP.

 The **technical or service operator** maintains the devices, communication services, cloud services and supporting infrastructure.

 These actors may correspond to different physical persons or organizations depending on the deployment context.

 ## 2.2 Conceptual SSP Use-Case Model

 At the operational level, SSP can be represented as:

 **Protected environment → SSP monitoring → location/status/risk information → alert → authorized user → operational action**

 The monitoring process involves the acquisition and interpretation of information concerning the monitored person or protected entity. The resulting information is made available to authorized users according to the operational context and applicable access policies.

 This representation is deliberately conceptual. It describes how SSP is used rather than defining its technical architecture.

 ## 2.3 Use Case 1 — Normal Monitoring

 Normal monitoring represents the baseline operating condition in which no critical event is currently detected.

 The operational sequence is:

 **Device activated → positioning and motion information acquired → local processing evaluates current state → relevant information transmitted according to policy → monitored status updated → authorized operator observes current status → adaptive monitoring continues**

 Normal operation does not necessarily require continuous transmission of all raw sensor information. The system may process and summarize information locally and transmit only information required by the current monitoring policy.

 This scenario establishes the basis for adaptive sensing, event-oriented communication and energy-aware operation.

 ## 2.4 Use Case 2 — Approach to a Protected Perimeter

 When a monitored person approaches a protected perimeter, the monitoring process may become more intensive.

 The operational sequence is:

 **Movement detected → position and motion evaluated → trajectory or proximity assessed → approach condition identified → risk level increases → monitoring and communication policy adapts → predictive assessment performed → warning generated when threshold is reached → authorized user notified → operational response**

 This scenario illustrates that SSP is intended to support context-dependent monitoring rather than treating every operating condition identically.

 ## 2.5 Use Case 3 — High-Risk or Critical Event

 A high-risk event may arise from abnormal movement, a perimeter violation or another condition defined by the monitoring policy.

 The operational sequence is:

 **Abnormal condition detected → local event assessment → high-risk condition identified → priority communication → further event evaluation → critical event confirmed → immediate notification → authorized user reviews event → operational response**

 The scenario establishes the requirement for differentiated event priority and low-latency processing.

 ## 2.6 Use Case 4 — Temporary Connectivity Loss

 Connectivity may become unavailable during normal operation.

 The operational sequence is:

 **Normal monitoring → connectivity disruption → communication failure detected → local monitoring continues → relevant information buffered → selected event processing continues → connectivity restored → buffered information synchronized → normal operation resumes**

 Loss of connectivity shall therefore not automatically imply loss of all monitoring functionality.

 ## 2.7 Use Case 5 — Device Tampering or Abnormal Device State

 The device may experience tampering or an abnormal internal condition.

 The operational sequence is:

 **Normal device operation → abnormal device condition detected → local validation → condition classified → priority communication attempted → event processed → authorized operator notified → operational response**

 This scenario connects physical device state with the broader safety and security requirements of SSP.

 ## 2.8 Use Case 6 — Privacy-Aware Monitoring

 Sensor information may contain information that is not required for every operational function.

 The intended information flow is:

 **Sensor information generated → local processing → information classified → required information identified → necessary information transmitted according to policy → unnecessary raw information retained locally, aggregated or discarded where appropriate → monitoring continues**

 This scenario establishes data minimization as an operational principle without prescribing the detailed technical implementation.

 ## 2.9 Use Case 7 — Operator Workflow

 From the perspective of the protection operator, the operational sequence is:

 **Operator authentication → monitored devices displayed → status/location/risk/battery/connectivity/events reviewed → monitoring continues when no critical event exists → alert received → event information reviewed → operational procedure applied → event acknowledged or closed → relevant record retained**

 The interface shall therefore provide information that supports operational decision-making rather than merely displaying raw sensor data.

 ## 2.10 End-to-End SSP Operational Storyboard

 The complete operational process can be summarized as:

 **Physical environment → sensing → local information processing → contextual/event processing → centralized information management → authorized user → operational response**

 Operational feedback then produces:

 **Operational response → policy/configuration → subsequent monitoring behaviour**

 This feedback relationship emphasizes that SSP is an operational monitoring system rather than simply a collection of sensing devices.

 ## 2.11 Stakeholder Interaction Summary

 The principal interactions are summarized below.

 | Actor | Interaction with SSP | Main information consumed or generated |
| --- | --- | --- |
| Protected person | Receives relevant protection information | Alerts, protection status |
| Monitored person | Uses or carries the monitored device | Position, movement, device status |
| Protection operator | Monitors events and performs operational actions | Location, risk, alerts, device status |
| System administrator | Configures users, devices and policies | Configuration and management information |
| Authorized organization | Deploys and manages SSP | Operational and management information |
| Technical/service operator | Maintains technical services | Device, connectivity and system-health information |

## 2.12 Chapter 2 to Chapter 3 Transition

 The use cases presented in this chapter define how SSP is expected to operate from the perspective of its users and operational environment. They identify the principal interactions, events, decisions and responses that the system must support.

 These scenarios provide the basis for translating expected behaviour into measurable functional, data, performance, security, privacy, reliability, scalability and economic requirements.

 The resulting progression is:

 **Operational scenarios → required system capabilities → measurable engineering requirements**

---

 # 3\. SSP Functional and Performance Requirements

 ## 3.1 Requirement Structure

 The requirements in this chapter distinguish between functional requirements and performance requirements.

 A **functional requirement** specifies what SSP shall do.

 A **performance requirement** specifies a measurable characteristic describing how well the required function shall operate.

 The distinction is maintained throughout D2 so that subsequent validation can determine independently whether a function exists and whether its implementation satisfies the associated quantitative target.

 ## 3.2 Device Functional Requirements

 The SSP device shall acquire motion information using inertial sensing suitable for detecting movement, inactivity, acceleration patterns and other relevant motion states.

 The device shall acquire positioning information when a positioning source is available.

 The device shall detect relevant proximity states when a suitable proximity mechanism is available.

 The device shall monitor battery state, communication state, sensor state and relevant internal health indicators.

 The device shall preprocess, filter, validate, transform or aggregate sensor information when local processing can reduce unnecessary communication or energy consumption.

 The device shall evaluate deterministic rules and/or lightweight inference for selected events that require local detection.

 The device shall temporarily buffer relevant measurements, status records and events when communication is unavailable.

 The device shall generate information describing its operational state.

 The device shall adapt its operating state according to monitoring requirements, detected activity and available battery energy.

 The device shall receive authorized configuration parameters, including monitoring rates, operating modes and communication parameters.

 The device shall maintain a unique identity for data association and authenticated communication.

 The target product shall support an authenticated firmware-update mechanism.

 These functions correspond to the following requirement set:

 **F-D01 → motion sensing**\
 **F-D02 → positioning**\
 **F-D03 → proximity detection**\
 **F-D04 → device-state monitoring**\
 **F-D05 → local preprocessing**\
 **F-D06 → local event detection**\
 **F-D07 → temporary storage**\
 **F-D08 → local status generation**\
 **F-D09 → energy management**\
 **F-D10 → configuration reception**\
 **F-D11 → device identification**\
 **F-D12 → secure firmware lifecycle**

 ## 3.3 Edge Functional Requirements

 The SSP system shall support reception of information from monitored devices.

 Received information shall be validated with respect to message structure, identity, sequence information and data validity.

 The system shall preserve or establish timestamps and distinguish measurement time from reception time where necessary.

 Sequence numbers and timestamps shall be used to identify out-of-order information.

 Incoming information shall be aggregated into structured records when appropriate.

 Invalid, redundant or irrelevant information shall be filtered according to configured policies.

 Selected features shall be extracted from incoming sensor information.

 Selected event-processing rules shall be executable at the edge.

 Selected inference functions shall be executable at the edge when this provides a latency, connectivity or privacy advantage.

 The system shall temporarily buffer relevant information when centralized connectivity is unavailable.

 Buffered information shall be synchronized following connectivity recovery.

 Duplicate information shall be detectable using message identifiers, sequence numbers or equivalent mechanisms.

 Relevant information shall be forwarded to centralized services when connectivity is available.

 Authorized configuration information shall be transferable toward the monitored devices.

 Selected monitoring and event-processing functions shall continue during temporary centralized-service unavailability.

 These functions correspond to:

 **F-E01 → F-E15**

 ## 3.4 Communication Functional Requirements

 The communication subsystem shall provide bidirectional transfer of telemetry, events, status and authorized configuration information.

 The communication subsystem shall support device-to-intermediate processing communication and communication between intermediate processing and centralized services, while the specific technologies remain subject to subsequent architecture evaluation.

 The communication subsystem shall support retry, synchronization, message-integrity protection, device authentication and communication-failure detection.

 Temporary offline operation shall be supported.

 The corresponding functional requirements are:

 **F-C01 → device-to-intermediate communication**\
 **F-C02 → intermediate-to-centralized communication**\
 **F-C03 → bidirectional communication**\
 **F-C04 → telemetry transfer**\
 **F-C05 → prioritized event transfer**\
 **F-C06 → status transfer**\
 **F-C07 → authorized configuration transfer**\
 **F-C08 → retry and synchronization**\
 **F-C09 → message integrity**\
 **F-C10 → communication authentication**\
 **F-C11 → communication-failure detection**\
 **F-C12 → temporary offline operation**

 ## 3.5 Cloud Functional Requirements

 Centralized services shall support device registration and authentication, user authentication, telemetry and event reception, incoming-data validation and historical data storage.

 The centralized service shall maintain current device state, process events, execute centralized analytics and support AI model management where applicable.

 It shall manage users and roles, enforce access permissions, maintain audit information, provide authorized APIs and support fleet management.

 It shall provide configurable data retention and deletion and support authorized notifications and historical data queries.

 The corresponding requirements are:

 **F-CL01 → F-CL19**

 ## 3.6 User Interface Functional Requirements

 The user interface shall provide authorized users with current device status, current or most recent position, event notifications, event history, map-based visualization, battery information, communication status and historical summaries.

 Authorized administrative users shall be provided with device, user and configuration management functions according to their permissions.

 The interface shall support event acknowledgement where applicable and shall not display information for which the authenticated user has insufficient authorization.

 The corresponding requirements are:

 **F-U01 → F-U13**

 ## 3.7 Data Requirements

 SSP shall distinguish between compact device-level data and structured information used for higher-level processing and interfaces.

 The device-level representation shall be optimized for bandwidth and energy efficiency. The structured representation shall support interoperability, processing, maintainability and historical storage.

 A compact binary representation such as binary encoding, CBOR, Protocol Buffers or an equivalent technology may be used for constrained communication. A structured representation such as JSON or an equivalent representation may be used for application interfaces. The final encoding shall be selected during subsequent engineering work.

 ### 3.7.1 Principal Device Data

 The device shall be capable of generating information including device identity, timestamps, sequence numbers, acceleration, angular velocity, position, position confidence, proximity state, battery state, device state, communication state and event state.

 Logical data representation shall permit at least:

 **Device identifier → timestamp → sequence information → sensor information → position → device state → event information**

 The precise binary encoding and protocol overhead shall be determined during implementation.

 ### 3.7.2 Adaptive Sampling

 The device shall support adaptive sampling.

 As initial engineering targets, normal operation shall support inertial sampling up to approximately 50 Hz, while high-activity or event conditions shall permit sampling up to approximately 100 Hz.

 Position updates shall support approximately 0.1–1 Hz under normal operation, with dynamically increased update frequency when required by the monitoring context.

 Battery and device-status information shall normally be updated approximately every 10–60 s or according to the operational state.

 The device shall avoid continuous transmission of every raw inertial sample during normal operation unless explicitly required by a diagnostic or specialized monitoring mode.

 ### 3.7.3 Packet and Record Sizes

 A normal device telemetry packet shall have a target maximum application payload of **128 bytes**.

 An event packet shall have a target maximum application payload of **512 bytes**.

 An edge or centralized structured telemetry/event record shall have a target maximum size of **1 kB** under normal operation.

 Normal user-interface/API responses shall have a target maximum size of **100 kB per request or page**, with larger historical information returned through pagination.

 These limits refer to application data and exclude lower-layer protocol overhead unless otherwise specified.

 ## 3.8 Communication and Data-Volume Requirements

 The target normal application traffic generated by one device shall not exceed approximately **10 kbit/s average**.

 The device communication subsystem shall target a latency of no more than shall provide a target application-level capacity of at least **100 kbit/s per device**, providing headroom for bursts, retransmission and protocol overhead.

 Event communication shall support bursts of at least approximately **50 kbit/s per device** at the application level.

 Normal aggregated telemetry shall normally be transmitted at approximately 10–60 s intervals, while significant events shall be transmitted as soon as practical when connectivity is available.

 ## 3.9 Computational Performance Requirements

 The device shall target sensor acquisition latency of no more than **20 ms**.

 Local preprocessing shall target a latency of no more than **100 ms**.

 Local event-rule evaluation shall target a latency of no more than **200 ms**.

 Local event-decision generation shall target a maximum of approximately **500 ms**.

 Local buffer-write latency shall target no more than **100 ms**.

 Average local processing duty cycle shall target no more than approximately **20%** under nominal monitoring conditions.

 The intermediate processing stage shall support a nominal application latency of approximately **2 s or less** for device-to-intermediate information transfer.

 ## 3.10 Communication Performance

 The selected short-range communication solution shall target a nominal practical range of at least **10 m**, with **5 m** considered a minimum practical target for constrained deployment scenarios.

 The communication subsystem shall target application-level throughput of at least **100 kbit/s** for device-to-intermediate communication.

 Nominal communication latency shall target approximately **500 ms** for ordinary messages, while significant event delivery shall target approximately **2 s** under nominal connectivity.

 After applicable retry mechanisms, application-level packet loss shall target less than **1%** under nominal conditions.

 Wide-area communication shall provide a target application capacity of at least **50 kbit/s per device**, subject to available external network coverage.

 ## 3.11 Communication Resilience

 The system shall continue useful monitoring during temporary communication loss.

 The minimum target buffering capacity for event and status information shall be **24 hours**.

 During connectivity loss, local monitoring and selected event-processing functions shall continue.

 After connectivity recovery, relevant buffered information shall be synchronized.

 Sequence numbers and identifiers shall allow missing or duplicated information to be detected.

 Critical events shall not be silently discarded solely because centralized connectivity is unavailable.

 The operational sequence is therefore:

 **Connectivity loss → local monitoring → event detection → buffering → connectivity recovery → synchronization**

 ## 3.12 Energy Requirements

 Energy efficiency shall be treated as a system-level requirement involving sensing, processing, positioning and communication.

 Initial device power targets are:

 | Operating state | Target |
| --- | --- |
| Deep sleep | ≤1 mW |
| Normal monitoring | ≤50 mW |
| Active sensing | ≤150 mW |
| Communication burst | ≤500 mW peak |
| Positioning active | ≤300 mW peak |

The minimum target battery autonomy shall be **7 days** under the defined nominal operating conditions.

 The engineering objective shall be **14 days or more** under nominal monitoring conditions.

 The system shall consider the relationship:

 **Monitoring intensity ↔ responsiveness ↔ energy consumption**

 Adaptive sensing and event-driven communication shall be used where appropriate to manage this trade-off.

 The final battery capacity and energy model shall be established using selected components and measured operating characteristics during later implementation.

 ## 3.13 Mechanical and Environmental Requirements

 The target device shall be wearable or portable.

 Initial engineering targets are:

 | Parameter | Target |
| --- | --- |
| Maximum volume | ≤100 cm³ |
| Maximum mass | ≤100 g |
| Operating temperature | −10 to +50 °C |
| Storage temperature | −20 to +60 °C |
| Ingress protection | IP65 or better target |
| Drop resistance | ≥1 m target |

The device shall support ordinary indoor and outdoor operation within the defined environmental range.

 Where a dedicated intermediate gateway is required, its initial target dimensions are approximately **≤2 L** and **≤500 g**. These constraints apply only where a dedicated physical gateway is used and do not prescribe the final architecture.

 ## 3.14 Cloud Capacity and Storage Requirements

 The initial centralized service deployment shall support at least **100 active devices**.

 The scalable deployment target shall be at least **10,000 devices**.

 The initial ingestion capacity shall target at least **100 messages/s**, with a target burst capacity of approximately **20 events/s**.

 Normal API requests shall target a p95 response latency of no more than **1 s**.

 Event processing shall target a p95 latency of no more than **2 s**.

 The service availability target shall be at least **99.5%** under the applicable service conditions.

 Historical information shall be retained for at least **12 months**, subject to applicable privacy and retention policies.

 An initial deployment shall provide at least **500 GB of usable application storage**, while the overall system shall support expansion beyond this value.

 For planning purposes, assuming a 200-byte telemetry record generated every 30 s gives:

 **200 bytes × 86,400 s/day ÷ 30 s ≈ 576,000 bytes/day/device**

 or approximately **0.576 MB/device/day** before infrastructure overhead.

 For 1,000 devices this corresponds to approximately **576 MB/day**, and for one year approximately **210 GB** of raw application data.

 For 10,000 devices the equivalent raw annual volume is approximately **2.1 TB**, before indexes, replication, backups and infrastructure metadata.

 These calculations justify scalable storage rather than treating 500 GB as a long-term upper limit.

 ## 3.15 User Interface Performance

 The user interface shall target the following response characteristics:

 | Function | Target |
| --- | --- |
| Login response | ≤2 s |
| Dashboard loading | ≤3 s |
| Current-status refresh | ≤5 s |
| Event display after centralized ingestion | ≤5 s |
| Historical query p95 | ≤2 s |
| Map display | ≤3 s |
| Normal API response | ≤100 kB |

The interface shall prioritize current state, significant events, current or recent position, battery condition, connectivity and historical summaries.

 ## 3.16 End-to-End Event Performance

 Operationally significant events may originate from local, intermediate or centralized processing.

 Each event shall include an event type, timestamp, source, severity and confidence or quality information, together with relevant triggering information where available.

 Under nominal connectivity, the target end-to-end event path is:

 **Sensor → processing → centralized service → UI ≤10 s**

 For high-priority events, the target shall be:

 **High-priority event → authorized user notification ≤5 s**

 These targets do not constitute guarantees during external network outages or other conditions outside SSP's control.

 ## 3.17 Security Requirements

 SSP shall incorporate security throughout the system lifecycle information necessary important reference for defining SSP requirements. The purpose of this chapter is not to reproduce the detailed market research conducted during the earlier project work, but to retain the observations that are relevant to the engineering specification.

 The system shall provide unique device identities, authenticated device communication, authenticated user access, role-based authorization, encrypted communication, protected credential storage, secure update mechanisms, audit logging and appropriate session management.

 The communication system shall provide mechanisms for message-integrity verification and protection against replay or duplicated messages where required.

 The final cryptographic algorithms and key-management mechanisms shall be selected during subsequent engineering activities.

 ## 3.18 Privacy Requirements

 SSP may process sensitive location, movement and event information.

 The system shall therefore apply data minimization throughout its operation.

 Only information necessary for an intended function shall be collected or transmitted where technically and operationally feasible.

 Raw sensor information shall not automatically be transmitted when processed, aggregated or event-oriented information is sufficient to fulfil the required function.

 Access to sensitive information shall be controlled according to user authorization.

 Sensitive information shall be protected in transit and at rest.

 Retention periods shall be configurable and deletion shall be supported.

 Administrative access shall be auditable.

 The fundamental information-flow principle is:

 **Raw information → local processing → necessary information → controlled transmission → authorized use**

 The final implementation shall comply with applicable data-protection requirements for the intended deployment.

 ## 3.19 AI Functional and Performance Scope

 AI is considered an optional intelligence capability rather than a prerequisite for every SSP function.

 Potential AI-assisted functions include movement classification, activity recognition, anomaly detection, contextual event classification, false-event reduction and predictive maintenance.

 Deterministic rules shall remain available for functions for which machine learning is unnecessary or undesirable.

 AI processing may subsequently be considered at different processing stages according to:

 **Model complexity ↔ computational resources ↔ latency ↔ energy ↔ privacy ↔ connectivity**

 Initial engineering targets include classification accuracy of at least **90%** on representative validation data, event recall of at least **90%**, a false-positive rate target of no more than **5%**, and inference latency of approximately **200 ms or less** for selected edge-processing functions.

 These values are development targets and shall not be interpreted as achieved results. The final metrics shall be refined once datasets, event classes and validation methodologies have been established.

 ## 3.20 Economic Requirements

 Economic requirements shall prevent the technical solution from becoming impractical for the intended deployment.

 The initial production-oriented hardware cost target shall be no more than approximately **€150 per device** for low-volume implementation.

 The engineering objective for larger-scale production shall be approximately **€100 per device** or less.

 The target recurring communication and centralized-service cost shall be no more than approximately **€10 per device per month** under nominal operating conditions.

 For an initial deployment of 100 devices, the first-year operational deployment target shall be no more than approximately **€25,000**, excluding personnel salaries and academic development labour.

 The deployment target may include device hardware, batteries and accessories, intermediate infrastructure, communication services, centralized services and reasonable maintenance or replacement allowances.

 Development, certification and organizational costs shall be identified separately during subsequent economic analysis.

 ## 3.21 Engineering Trade-Offs

 The SSP requirements involve several interdependent engineering variables.

 Monitoring intensity affects both responsiveness and energy consumption:

 **Monitoring intensity ↔ responsiveness ↔ battery autonomy**

 Local processing may reduce communication but increases computational requirements:

 **Local computation ↔ communication volume ↔ energy consumption**

 Raw information provides analytical flexibility but increases bandwidth, storage and privacy exposure:

 **Raw information ↔ analytical flexibility ↔ bandwidth ↔ privacy**

 AI complexity may improve analytical capability while increasing computational requirements:

 **Model complexity ↔ analytical capability ↔ latency ↔ energy**

 Communication availability can improve resilience while increasing recurring cost:

 **Connectivity ↔ resilience ↔ operational cost**

 These relationships explain why the requirements are specified as a system of interacting constraints rather than as independent numerical targets.

 ## 3.22 Requirement Traceability

 The requirements shall be traceable to the operational scenarios introduced in Chapter 2.

 | Operational scenario | Principal requirement areas | Later verification |
| --- | --- | --- |
| Normal monitoring | Sensing, adaptive sampling, local processing, telemetry, UI | D3/D4 |
| Protected-perimeter approach | Positioning, contextual processing, event detection, latency | D3/D4/D5 |
| High-risk event | Event detection, priority communication, end-to-end latency | D4/D5/D6 |
| Connectivity loss | Local operation, buffering, synchronization, resilience | D4 |
| Device tampering | Device-state monitoring, event generation, security | D4/D5 |
| Privacy-aware monitoring | Data minimization, access control, retention, deletion | D3/D4/D6 |
| Operator workflow | UI, authentication, authorization, event handling | D3/D4 |
| End-to-end operation | Integrated sensing, processing, communication and user notification | D4/D6 |

This traceability establishes:

 **Use case → functional requirement → performance requirement → implementation → validation**

 ## 3.23 D2 Requirements Summary

 The principal quantitative targets established by D2 are summarized below.

 | Requirement domain | Initial target |
| --- | --- |
| Normal inertial sampling | Up to 50 Hz |
| Event/high-activity inertial sampling | Up to 100 Hz |
| Position update | Approximately 0.1–1 Hz adaptive |
| Normal telemetry packet | ≤128 B |
| Event packet | ≤512 B |
| Structured record | ≤1 kB |
| Normal application traffic | ≤10 kbit/s/device |
| Device communication capacity | ≥100 kbit/s |
| Event burst capacity | ≥50 kbit/s |
| Local event decision | ≤500 ms |
| Device-to-intermediate nominal latency | ≤2 s |
| Communication range target | ≥10 m |
| Offline buffering | ≥24 h |
| Deep sleep | ≤1 mW |
| Normal monitoring | ≤50 mW |
| Active sensing | ≤150 mW |
| Communication peak | ≤500 mW |
| Minimum battery autonomy | ≥7 days |
| Engineering battery objective | ≥14 days |
| Device mass | ≤100 g |
| Device volume | ≤100 cm³ |
| Operating temperature | −10 to +50 °C |
| Ingress protection | IP65 target |
| Initial centralized fleet | 100 devices |
| Scalability objective | ≥10,000 devices |
| Initial ingestion capacity | ≥100 messages/s |
| Centralized-service availability | ≥99.5% |
| Centralized API p95 | ≤1 s |
| Historical retention | ≥12 months |
| Initial usable storage | ≥500 GB |
| Dashboard loading | ≤3 s |
| Normal API response | ≤100 kB |
| End-to-end event | ≤10 s |
| High-priority event | ≤5 s |
| Edge AI inference target | ≤200 ms |
| Initial AI accuracy target | ≥90% |
| Initial device cost | ≤€150 |
| Scaled device cost objective | ≤€100 |
| Recurring cost | ≤€10/device/month |
| Initial 100-device deployment | ≤€25,000 first-year target |

---

 # 4\. Existing Solutions and Requirements Context

 ## 4.1 Purpose of the Existing-Solutions Analysis

 Existing monitoring and tracking solutions provide an important reference for defining SSP requirements. The purpose of this chapter is not to reproduce the detailed market research conducted during the earlier project work, but to retain the observations that are relevant to the engineering specification.

 The analysis establishes which capabilities are already present in existing solutions and identifies areas in which SSP may investigate alternative or improved approaches.

 The logical relationship is:

 **Existing solutions → established capabilities and constraints → opportunities for improvement → SSP requirements**

 ## 4.2 Established Monitoring Capabilities

 Commercial monitoring and tracking systems demonstrate that several capabilities considered by SSP are established functions in the application domain. These include location tracking, geofencing or virtual-boundary monitoring, event notifications, historical location information and application-based monitoring.

 Consequently, SSP shall not treat basic location tracking or notification as sufficient evidence of innovation by itself.

 The existence of these capabilities establishes a baseline against which SSP requirements can be formulated.

 ## 4.3 Existing interface through which authorized users can interpret the observations reinforce the relevance of the demonstrated advantages at distributing selected processing functions across constrained and local monitoring, temporary buffering, selected local or intermediate event products lack all corresponding capabilities. Rather, it identifies the combination of characteristics that SSP will investigate and quantify-Solution Perspective

 Existing solutions also illustrate the practical importance of several system-level constraints.

 A monitoring system must provide sufficiently current information to support operational decisions.

 It must provide event notifications when relevant conditions occur.

 It must maintain historical information where required.

 It must provide a user interface through which authorized users can interpret the current and historical state of monitored entities.

 It must operate within practical constraints concerning device size, energy consumption, communication availability and operating cost.

 These observations reinforce the relevance of the requirements established in Chapter 3.

 ## 4.4 SSP Improvement Opportunities

 The analysis identifies opportunities for improvement using **distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation**.

 These opportunities are not presented as experimentally demonstrated advantages at the D2 stage.

 Instead, they define areas in which the SSP engineering design shall investigate measurable improvements.

 ### 4.4.1 Distributed Processing

 Existing monitoring systems establish the usefulness of centralized monitoring and analysis. SSP additionally investigates distributing selected processing functions across constrained and less constrained computational environments.

 The intended progression is:

 **Sensor information → local preprocessing → intermediate processing → centralized analytics**

 The objective is to reduce unnecessary data transmission, support low-latency decisions and maintain selected functions during connectivity interruptions.

 ### 4.4.2 Adaptive Monitoring

 A fixed monitoring intensity may be inefficient when operational conditions vary.

 SSP therefore specifies adaptive monitoring in which sensing and communication intensity can respond to activity, proximity, risk or other contextual information.

 The intended progression is:

 **Normal condition → moderate monitoring → increased activity/risk → intensified monitoring → event resolution → return to normal monitoring**

 This objective is reflected in the adaptive sampling and energy requirements of Chapter 3.

 ### 4.4.3 Energy-Aware Operation

 Portable safety-monitoring devices are constrained by available battery energy.

 SSP therefore considers sensing, processing, positioning and communication as components of a common energy budget.

 The intended relationship is:

 **Low activity → low-power operation → increased activity → intensified sensing/processing → event resolution → low-power operation**

 The quantitative energy targets in Chapter 3 establish measurable criteria for subsequent validation.

 ### 4.4.4 Privacy-Aware Information Flow

 Location and movement information may be sensitive.

 SSP therefore investigates whether required functions can be performed using derived or aggregated information rather than continuous transmission of raw measurements.

 The intended principle is:

 **Raw sensor information → local processing → relevant information → controlled transmission → authorized use**

 This approach is intended to reduce unnecessary data exposure while preserving required system functionality.

 ### 4.4.5 Contextual Event Interpretation

 A simple threshold-based monitoring approach may not fully represent the context in which a movement or position change occurs.

 SSP therefore includes requirements for contextual event processing and optional AI-assisted interpretation.

 The intended progression is:

 **Sensor measurements → features/context → event interpretation → risk assessment → operational notification**

 The purpose of D2 is to define the capability and performance targets; the specific algorithms and models remain subject to later development and validation.

 ### 4.4.6 Resilient Operation

 Connectivity interruptions are a normal possibility in distributed IoT deployments.

 SSP therefore specifies local monitoring, temporary buffering, selected local or intermediate event processing and post-recovery synchronization.

 The intended operational sequence is:

 **Connectivity available → normal operation → connectivity loss → local operation and buffering → connectivity recovery → synchronization → normal operation**

 This provides a measurable resilience objective rather than assuming permanent network availability.

 ## 4.5 Relationship Between Existing Capabilities and SSP Requirements

 The existing-solutions analysis supports the following distinction.

 Established market functions include:

 **location monitoring → proximity/geofencing → event notification → historical information → application-based monitoring**

 SSP requirements additionally emphasize:

 **adaptive monitoring → distributed processing → energy-aware operation → privacy-aware information flow → contextual event interpretation → resilient operation**

 The second group should not be interpreted as an assertion that existing commercial products lack all corresponding capabilities. Rather, it identifies the combination of characteristics that SSP will investigate and quantify.

 ## 4.6 Requirements Versus Demonstrated Improvements

 D2 defines **intended engineering improvements**, not validated product superiority.

 The distinction is essential:

 **D2 → defines targets**

 **D3/D4/D5 → develops the system**

 **D4/D5/D6 → measures and validates performance**

 Only after implementation and measurement can SSP determine whether the proposed targets have actually been achieved and commercial competitiveness, superiority or comparative performance are therefore outside the scope of the present specification and AI models will be selected and evaluated against the D2 requirements rather than being assumed in advance 1 establishes the problem addressed by SSP and defines the intended system-level improvement objectives. Chapter 2 describes how SSP is expected to be used through operational scenarios involving normal monitoring, perimeter approach, high-risk events, connectivity loss, device abnormalities, privacy-aware monitoring and operator interaction. Chapter 3 translates these scenarios into measurable functional, data, performance, energy, communication, resilience, security, privacy, AI and economic requirements. Chapter 4 places these requirements in the context of existing monitoring and tracking solutions and identifies of the SSP project while deliberately leaving architecture and implementation decisions to subsequent whether the resulting system provides measurable advantages relative to specific existing solutions.

 Claims concerning commercial competitiveness, superiority or comparative performance are therefore outside the scope of the present specification unless supported by appropriate experimental evidence.

 ## 4.7 Chapter 4 to Future Engineering Work

 The existing-solutions analysis provides context for the requirements established in Chapter 3.

 The resulting development logic is:

 **Problem and objectives → operational use cases → measurable requirements → existing-solution context → architecture and implementation → validation**

 The architecture required to satisfy these requirements will be developed in the subsequent D3 deliverable. Hardware, communication technologies, implementation mechanisms and AI models will be selected and evaluated against the D2 requirements rather than being assumed in advance.

---

 # 5\. D2 Scope Boundary and Relationship to Subsequent Deliverables

 D2 deliberately stops at the requirements level.

 The following distinction shall be maintained throughout the project:

 **D2 → What SSP shall do and how well it shall perform**

 **D3 → How SSP is architected to satisfy the requirements**

 **D4 → How the selected hardware and implementation realize the architecture**

 **D5 → How AI and related intelligent-processing functions are developed and evaluated**

 **D6 → How the implemented system is validated and economically evaluated**

 Accordingly, no final device, edge, communication or cloud architecture is specified in this document.

 The conceptual operational relationships presented in Chapters 1 and 2 are used only to establish system behaviour and requirements. They shall not be interpreted as the final technical architecture.

---

 # Conclusion

 This D2 document establishes the functional and performance requirements of the Smart Safety & Protection IoT system.

 The document follows the progression:

 **SSP motivation and objectives → target users and operational scenarios → functional and performance requirements → existing solutions and improvement opportunities**

 Chapter 1 establishes the problem addressed by SSP and defines the intended system-level improvement objectives. Chapter 2 describes how SSP is expected to be used through operational scenarios involving normal monitoring, perimeter approach, high-risk events, connectivity loss, device abnormalities, privacy-aware monitoring and operator interaction. Chapter 3 translates these scenarios into measurable functional, data, performance, energy, communication, resilience, security, privacy, AI and economic requirements. Chapter 4 places these requirements in the context of existing monitoring and tracking solutions and identifies areas for further engineering investigation.

 The principal improvement objectives are expressed through:

 **distributed processing → adaptive monitoring → energy-aware operation → privacy-aware information flow → contextual event interpretation → resilient operation**

 These objectives are not presented as already-achieved results. They constitute engineering targets that will be evaluated through subsequent implementation and validation activities.

 D2 therefore provides the requirements baseline for the next stages of the SSP project while deliberately leaving architecture and implementation decisions to subsequent deliverables.

 The detailed architecture belongs to D3 and shall be derived from the requirements established in this document.

 This version keeps the **stronger structure of the latest D2**, while recovering the technically useful material from the previous document. Most importantly, **Chapter 5 is no longer an architecture chapter**: D2 ends at the requirements/context level, and D3 is explicitly reserved for architecture.
