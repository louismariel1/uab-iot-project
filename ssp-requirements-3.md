# Final D2 Plan
 
 > **The final D2 should not simply reproduce the previous document. It should preserve its quantitative requirements and data specifications, while reorganizing them into Chapters 1–4 so that the document follows the intended reasoning chain: SSP idea → operational use → requirements → existing solutions/market context.**

 IEEE's own guidance emphasizes a clear scientific structure with title, authors, abstract, introduction, references, and appropriate technical organization, and recommends using the IEEE article templates and editorial guidance.  IEEE Author Center+1

 ### Coverage review

 | D2 question | Status | What the final version should do |
| --- | --- | --- |
| Functions at device, edge, cloud and UI | **Covered** | Preserve the detailed functional requirements, but derive them from Chapter 2 use cases. |
| Data at every node | **Mostly covered** | Preserve the previous device/edge/cloud/UI data definitions, including types, formats, packet sizes and rates. |
| Functional vs. performance specifications | **Covered** | Make this distinction explicit in Chapter 3. |
| Device→edge computational requirements | **Covered** | Retain latency, throughput, processing duty-cycle and buffering targets. |
| Device→edge communications | **Covered, but refine** | State explicitly that the target is wireless, short-range, bidirectional, with ≥10 m target range and ≥100 kbit/s application capacity. |
| Energy | **Covered for device; should clarify edge** | Device power/autonomy requirements remain. Edge should be treated primarily as externally powered unless a portable gateway is required; otherwise unnecessary battery requirements should not be invented. |
| Mechanical | **Covered** | Retain device mass/volume/environmental requirements and conditional requirements for a dedicated edge gateway. |
| Cloud | **Covered** | Retain storage, scalability, ingestion, analytics, availability, retention and API/UI requirements. |
| Economics | **Covered** | Retain device, recurring and global deployment cost targets. |
| Consistency with market | **Covered** | Chapter 4 should explicitly map established market functions to SSP requirements. |
| Is SSP competitive? | **Needs careful wording** | D2 can establish **intended areas of differentiation**, but cannot claim that SSP is competitive until implementation and measurements exist. |

There is also a useful point from the current market evidence. Commercial systems already provide location tracking, geofencing, alerts, historical information and adaptive tracking-related functions. For example, T-Mobile documents near-real-time location, virtual boundaries, motion alerts and location history for SyncUP TRACKER, while its KIDS Watch provides live tracking and virtual-boundary alerts.  T-Mobile+2  AngelSense similarly documents continuous monitoring, geofencing, route/activity-related alerts and historical timelines.  AngelSense+1

 That means the D2 should **not present location tracking, geofencing or alerts as SSP innovations**. Instead, the scientific argument should be:

 **Existing solutions establish the baseline → SSP requirements identify limitations/opportunities → SSP specifies distributed, adaptive, energy-aware, privacy-aware and resilient operation as intended improvements → later deliveries determine whether those improvements are achieved.**

 That is much stronger academically than saying simply that SSP is "competitive."

---

 # Final D2 structure

 I would therefore use the following final organization:

 **Title / Authors / Abstract / Index Terms**

 **Chapter 1 — Introduction and SSP Concept**

 This establishes the motivation, problem, scope, objectives and intended improvements. It should introduce the device, edge and cloud computational roles conceptually without becoming an architecture chapter.

 **Chapter 2 — Target Users, Use Cases and Operational Scenarios**

 This is the revised chapter you proposed. It explains actors and, more importantly, how SSP is actually used. The normal-monitoring, perimeter-approach, critical-event, connectivity-loss, tampering, privacy-aware and operator scenarios provide the behavioral foundation for the requirements.

 **Chapter 3 — Functional and Performance Specifications**

 This becomes the principal requirements chapter. It should contain the functional requirements and all measurable specifications from the previous D2: data, computational, communication, resilience, energy, mechanical contains the relevant findings from the previous market study, identifies established functions and limitations/opportunities, and explains how those observations inform the SSP requirements. It should, cloud, UI, security, privacy, AI and economic requirements.

 **Chapter 4 — Existing Solutions, Market Context and Requirements Implications**

 This contains the relevant findings from the previous market study, identifies established functions and limitations/opportunities, and explains how those observations inform the SSP requirements. It should explicitly avoid unsupported claims of commercial superiority.

 **References**

 This structure gives the clean progression:

 **Problem → SSP concept → Users/use → Required behavior → Measurable requirements → Existing solutions → Requirements implications → D3 architecture**

 And importantly, **there is no Chapter 5 architecture in D2**. Architecture belongs to D3.

---

 # D2 — Functional and Performance Specifications

 Below is the regenerated version I would treat as the new baseline document.

 # Smart Safety and Protection IoT System

 ## D2 — Functional and Performance Specifications

 **Academic Year:** 2026/2027\
 **Course:** UAB 105075 — IoT Design Project\
 **Deliverable:** D2 — Functional and Performance Specifications\
 **Acronym:** SSP\
 **IOT Group 14:** Louis-Marie Loe, Cheong Travis

 ## Abstract

 This document defines the functional and performance specifications of the proposed Smart Safety and Protection (SSP) Internet of Things (IoT) system. SSP is conceived as a distributed safety-monitoring system intended to monitor the location, movement, proximity and operational state of a protected person or monitored entity and to provide relevant information and alerts to authorized users. The specification is derived from the intended operational scenarios of SSP and from an analysis of existing commercial safety and tracking solutions.

 The document establishes the functions that SSP shall provide at the device, edge, cloud and user-interface levels and defines measurable requirements concerning data representation, communication, computational performance, energy consumption, mechanical characteristics, resilience, cloud operation, user-interface performance, security, privacy, artificial intelligence (AI) and system cost. Particular attention is given to adaptive monitoring, local and edge processing, event-oriented information exchange, communication-resilient operation, energy-aware operation and privacy-aware information processing.

 The requirements defined in this document are engineering targets and are not presented as experimentally validated results. Their feasibility and actual performance will be evaluated during subsequent project deliveries through architecture evaluation, implementation, measurement and validation. The present document therefore establishes the requirements against which subsequent design decisions and experimental results shall be evaluated.

 **Index Terms—** Internet of Things, safety monitoring, wearable device, location monitoring, motion sensing, edge computing, cloud computing, adaptive monitoring, event detection, energy management, privacy-aware computing.

 # I. INTRODUCTION

 ## A. Motivation

 Safety-monitoring applications require timely and reliable information concerning the location, movement and operational condition of a person or protected entity. A monitoring system must therefore perform more than sensor acquisition. It must transform physical observations into useful information, identify relevant events and provide authorized users with information that can support an appropriate operational response.

 The proposed Smart Safety and Protection (SSP) system addresses this problem through a distributed IoT solution in which sensing, local processing, edge processing, communication, cloud services and user interaction cooperate to provide continuous and context-dependent monitoring.

 The system is intended for scenarios in which the current or recent position of a monitored entity is relevant, movement or inactivity can provide contextual information, proximity can contribute to event detection, device status must be monitored, communication can temporarily become unavailable, and sensitive location and movement information requires controlled processing and access.

 The intended operational progression can be summarized as:

 **Physical environment → sensing → local processing → relevant information → edge processing → cloud services → authorized user → operational response**

 The system shall therefore be designed to support normal monitoring as well as changes in monitoring intensity when the operational context requires it.

 ## B. SSP Concept and Scope

 SSP is intended to combine sensing, processing, communication and information-management capabilities into an integrated safety-monitoring system. The target solution includes a monitored device, intermediate processing capabilities, communication services, cloud-based services and an authorized user interface.

 The present D2 specifies the required behavior and measurable characteristics of these functions. It does not define the final technical architecture, select the final microcontroller or communication technology, prescribe a specific cloud provider, or determine the final AI model. Those engineering decisions belong to subsequent project deliveries.

 The distinction is therefore:

 **D2 → what SSP shall do and how well it shall perform**

 **D3 → how SSP shall be architected to satisfy those requirements**

 The architecture itself is consequently outside the scope of this D2.

 ## C. SSP Improvement Objectives

 SSP is intended as an improved IoT safety and protection solution building on functions already established in existing monitoring and tracking systems. The objective of D2 is not to claim that these improvements have already been achieved, but to translate the intended improvements into measurable engineering requirements that can subsequently be validated.

 At the device level, SSP shall support local preprocessing, adaptive sensing, device-state monitoring, selected event detection, temporary buffering and energy-aware operation. The purpose is to reduce unnecessary raw-data transmission, adapt monitoring intensity to operational context and maintain useful local functionality during communication interruptions.

 At the edge level, SSP shall provide processing capabilities beyond simple forwarding. The edge shall support validation, filtering, aggregation, feature extraction, event evaluation, selected low-latency inference, buffering and synchronization. This is intended to reduce unnecessary cloud traffic, support low-latency processing and maintain selected monitoring functions during cloud unavailability.

 At the cloud level, SSP shall provide centralized historical storage, scalable telemetry and event ingestion, analytics, AI model management where applicable, user and role management, auditability, configurable retention and deletion, authorized APIs and fleet-management capabilities.

 Privacy shall be treated as a system-level requirement. Where a required function can be achieved using processed, summarized or aggregated information rather than continuous transmission of raw sensor data, the system shall prefer the lower-data approach, subject to operational requirements.

 AI shall be considered a distributed capability rather than exclusively a cloud function. Depending on latency, energy, computational-resource, connectivity and privacy constraints, selected AI-assisted functions may be performed locally, at the edge or in the cloud. D2 specifies the required capabilities and initial measurable targets without prescribing a final machine-learning architecture.

 Energy efficiency shall similarly be treated as a system-level design objective. Adaptive sensing, local processing, low-power operating states and event-driven communication shall be considered mechanisms for reducing unnecessary energy consumption.

 The intended improvements can therefore be expressed as:

 **Distributed processing + adaptive monitoring + energy-aware operation + privacy-aware information flow \+ contextual event interpretation \+ resilient operation → measurable SSP engineering requirements**

 ## D. Requirement-Level Interpretation

 The intended improvements shall be evaluated through measurable engineering outcomes rather than through unsupported claims of superiority over existing products.

 The subsequent project deliveries shall determine whether the implemented system satisfies the D2 targets for energy consumption, battery autonomy, local and edge processing latency, communication volume, offline resilience, AI performance, privacy-related data reduction, cloud scalability, system cost and end-to-end event latency.

 D2 therefore defines the requirements for the intended SSP solution, while later deliveries determine which improvements are actually achieved.

 # II. TARGET USERS, USE CASES AND OPERATIONAL SCENARIOS

 ## A. SSP Actors and Users

 The SSP operational model involves several categories of actors. The protected person is the person for whom a protection perimeter or safety condition is being monitored. The monitored person is the person or entity whose location or movement is subject to an authorized monitoring rule. The protection operator is responsible for monitoring alerts and operational status. The system administrator manages users, devices, policies and system configuration. The authorized organization is responsible for deploying and operating SSP. The technical or service operator maintains devices, connectivity, cloud services and supporting infrastructure.

 These actors establish the vocabulary required to describe the operational scenarios without yet prescribing a technical implementation.

 ## B. Core SSP Use-Case Model

 The conceptual use-case relationship is:

 **Protected person + monitored person → SSP monitoring → location status + risk assessment + device status → alert when required → authorized operational response**

 This representation is intentionally conceptual. It describes how SSP is used rather than how the system is technically implemented. The detailed Device–Edge–Cloud architecture belongs to the subsequent architecture delivery.

 ## C. Normal Monitoring

 Normal operation begins when the device is activated and acquires positioning and motion information. Local processing evaluates the current state and determines which information is relevant for transmission. Relevant information is then communicated according to the applicable monitoring policy, after which edge and cloud services update the monitored state and authorized users can inspect the current status.

 The operational sequence is:

 **Device activation → sensing → local processing → relevant information transmission → status update → authorized monitoring → adaptive monitoring**

 Normal monitoring does not necessarily require continuous transmission of all raw sensor information. The monitoring intensity may instead be adapted to activity and operational context.

 This behavior establishes requirements concerning adaptive sensing, local preprocessing, data reduction, energy consumption and periodic status updates.

 ## D. Approach to a Protected Perimeter

 When the monitored person moves toward a protected perimeter, the system shall support a progression from normal monitoring toward increased monitoring and event assessment.

 The operational sequence is:

 **Movement → position and motion evaluation → trajectory/proximity assessment → perimeter approach detection → increased risk → adapted monitoring policy → predictive assessment → warning threshold → notification → operational response**

 This scenario demonstrates that SSP is intended to interpret movement and context rather than simply report isolated location measurements.

 ## E. High-Risk or Critical Event

 A high-risk event may result from abnormal movement, a perimeter violation or another configured safety condition. The system shall support local event detection followed by prioritized communication and further event evaluation.

 The operational sequence is:

 **Abnormal condition → device detection → local assessment → high-risk condition → priority communication → edge assessment → event confirmation → immediate alert → authorized response**

 The detailed event-classification mechanism is implementation-dependent, but the functional requirement to support event detection and prioritized handling is established in D2.

 ## F. Temporary Connectivity Loss

 SSP shall support useful operation during temporary communication disruption.

 The operational sequence is:

 **Normal monitoring → connectivity disruption → communication failure detection → continued local operation → event/data buffering → connectivity recovery → synchronization → normal operation**

 Loss of cloud connectivity shall therefore not automatically imply loss of all protection functionality. The exact distribution of these functions will be determined during architecture design.

 ## G. Device Tampering or Abnormal Device State

 The system shall support detection of device tampering or other abnormal device states.

 The operational sequence is:

 **Normal device operation → abnormal device condition → local validation → event classification → priority communication → edge/cloud processing → operator notification → operational response**

 This use case connects physical device integrity with the wider security and monitoring functions of SSP.

 ## H. Privacy-Aware Monitoring

 SSP shall consider whether information generated by sensors is necessary for the intended monitoring function before transmitting it beyond the processing level at which it is generated.

 The conceptual information flow is:

 **Sensor information → local processing → information classification → necessity assessment → necessary information transmitted according to policy / unnecessary information processed or retained locally → SSP monitoring**

 This scenario establishes the behavioral basis for the privacy and data-minimization requirements specified later in this document.

 ## I. Operator Workflow

 From the operator perspective, SSP shall provide a workflow in which the operator authenticates to the system, reviews monitored devices and examines status, location, risk, battery, connectivity and alerts.

 The operational sequence is:

 **Operator authentication → monitored-device overview → status/location/risk review → continued monitoring or alert review → information assessment → operational procedure → event acknowledgement/closure**

 The workflow establishes the need for an authorized user interface, role-based access, current status information, event history and operational event handling.

 ## J. End-to-End SSP Operational Storyboard

 The principal operational flow can be summarized as:

 **Environment → sensing → local intelligence → edge processing → cloud intelligence → authorized user → operational response**

 Operational information may subsequently influence policies and configuration:

 **Operational response → policy/configuration → device and edge behavior → subsequent monitoring**

 This feedback relationship emphasizes that SSP is intended as an operational monitoring system rather than merely a collection of IoT components.

 ## K. Stakeholder Interaction Summary

 The protected person interacts primarily with SSP through protection notifications and protection status information. The monitored person carries or uses the monitored device, which generates position, movement and device-state information. The protection operator consumes location, risk, event and device-status information and performs operational responses. The administrator manages users, devices and policies. The authorized organization manages deployment and service operation. The technical or service operator maintains devices, connectivity and infrastructure.

 ## L. Chapter 2 to Chapter 3 Transition

 The use cases presented in this chapter define how SSP is expected to operate from the perspective of its users and operational environment. They identify the principal interactions, events, decisions and responses that the system must support. These scenarios provide the basis for translating the expected behavior into measurable functional, performance, security, privacy, reliability and scalability requirements in Chapter 3.

 # III. FUNCTIONAL AND PERFORMANCE SPECIFICATIONS

 ## A. Specification Principles

 Functional requirements describe what SSP shall do. Performance requirements describe measurable limits on how well those functions shall operate. The two categories shall remain explicitly separated throughout the subsequent project deliveries.

 The requirements in this chapter describe the target SSP solution. They are engineering targets and shall not be interpreted as experimentally achieved results.

 ## B. Device Functional Requirements

 The device shall acquire motion information using inertial sensors suitable for detecting movement, inactivity, acceleration patterns and other relevant motion states. It shall acquire positioning information when an appropriate positioning source is available and shall support proximity detection where proximity information is required by the application.

 The device shall monitor its battery state, communication state, sensor state and relevant internal health indicators. It shall perform local preprocessing such as filtering, validation, transformation and aggregation where this can reduce unnecessary and events when communication is unavailable. It shall generate local device-status information and adapt its operating state according to monitoring requirements, detected activity communication or energy consumption.

 The device shall support local event detection using deterministic rules and/or lightweight inference. It shall temporarily store relevant measurements, status information and events when communication is unavailable. It shall generate local device-status information and adapt its operating state according to monitoring requirements, detected activity and available battery energy.

 The device shall receive authorized configuration parameters such as sampling rates, monitoring modes and communication settings. It shall maintain a unique identity for data association and authenticated communication and shall support authenticated firmware updates in the target product.

 These functions are summarized by the following requirements:

 **F-D01 — Motion sensing:** The device shall acquire motion information using suitable inertial sensors.

 **F-D02 — Position determination:** The device shall acquire positioning information when a positioning source is available.

 **F-D03 — Proximity detection:** The device shall detect relevant proximity states where required.

 **F-D04 — Device-state monitoring:** The device shall monitor battery, communication, sensor and internal health states.

 **F-D05 — Local preprocessing:** The device shall filter, validate, transform and/or aggregate sensor information before transmission when appropriate.

 **F-D06 — Local event detection:** The device shall detect configured events using deterministic rules and/or lightweight inference.

 **F-D07 — Temporary storage:** The device shall buffer relevant information during temporary communication loss.

 **F-D08 — Local status generation:** The device shall generate information describing its operational state.

 **F-D09 — Energy management:** The device shall adapt operating states according to monitoring context and available energy.

 **F-D10 — Configuration reception:** The device shall receive authorized configuration parameters.

 **F-D11 — Device identification:** The device shall maintain a unique device identity.

 **F-D12 — Secure firmware lifecycle:** The target product shall support authenticated firmware updates.

 ## C. Edge Functional Requirements

 The edge processing function shall receive information from one or more devices and validate message structure, device identity, sequence information and data validity. It shall preserve measurement and reception timestamps and shall identify out-of-order information, execute local event rules and support selected low-latency inference where this provides a latency, resilience or connectivity CBOR, Protocol Buffers or an equivalent representation may be used for constrained device communication. JSON or an equivalent structured representation may be used for cloud APIs data model shall include a device identifier, timestamp, sequence number, accelerometer information, gyroscope information, latitude, longitude, position confidence, proximity state, battery bytes, a 64-bit timestamp, inertial values represented using suitable 16-bit or floating-point values, 32-bit floating-point latitude and longitude, a position-confidence.

 The edge shall aggregate incoming information into structured records and shall filter invalid, redundant or irrelevant information according to configured rules. It shall calculate selected features, execute local event rules and support selected low-latency inference where this provides a latency, resilience or connectivity advantage.

 The edge shall buffer information when cloud connectivity is unavailable and shall synchronize buffered information after connectivity is restored. It shall identify duplicate messages, forward relevant records and events to the cloud, forward authorized configuration information to devices and continue selected monitoring functions during cloud unavailability.

 The corresponding requirements are:

 **F-E01 — Data reception.**\
 **F-E02 — Message validation.**\
 **F-E03 — Timestamping.**\
 **F-E04 — Data ordering.**\
 **F-E05 — Aggregation.**\
 **F-E06 — Local filtering.**\
 **F-E07 — Feature extraction.**\
 **F-E08 — Event evaluation.**\
 **F-E09 — Low-latency inference.**\
 **F-E10 — Offline buffering.**\
 **F-E11 — Synchronization.**\
 **F-E12 — Duplicate handling.**\
 **F-E13 — Cloud forwarding.**\
 **F-E14 — Configuration forwarding.**\
 **F-E15 — Local operational continuity.**

 ## D. Communication Functional Requirements

 The communication subsystem shall provide device-to-edge and edge-to-cloud communication and shall support bidirectional exchange of telemetry, events, device status and authorized configuration information.

 It shall support event prioritization, retry and synchronization mechanisms and shall provide message integrity and device authentication. Communication failures shall be detectable and temporary offline operation shall be supported.

 The corresponding requirements are:

 **F-C01 — Device-to-edge communication.**\
 **F-C02 — Edge-to-cloud communication.**\
 **F-C03 — Bidirectional communication.**\
 **F-C04 — Telemetry transmission.**\
 **F-C05 — Event transmission.**\
 **F-C06 — Status transmission.**\
 **F-C07 — Configuration transmission.**\
 **F-C08 — Retry and synchronization.**\
 **F-C09 — Message integrity.**\
 **F-C10 — Device authentication.**\
 **F-C11 — Communication-failure detection.**\
 **F-C12 — Temporary offline operation.**

 The final communication technologies shall be selected during subsequent architecture and hardware evaluation.

 ## E. Cloud Functional Requirements

 The cloud subsystem shall support device registration and authentication, user authentication, telemetry and event ingestion, incoming-data validation, historical storage and current device-state management.

 It shall support event processing, cloud-level analytics and AI model management where applicable. It shall manage users and roles, enforce access permissions, maintain audit information and provide authorized APIs.

 The cloud shall support fleet management, configurable retention and deletion, authorized notifications and historical-data queries.

 The corresponding requirements are:

 **F-CL01 — Device registration.**\
 **F-CL02 — Device authentication.**\
 **F-CL03 — User authentication.**\
 **F-CL04 — Telemetry ingestion.**\
 **F-CL05 — Event ingestion.**\
 **F-CL06 — Data validation.**\
 **F-CL07 — Historical storage.**\
 **F-CL08 — Current-state management.**\
 **F-CL09 — Event processing.**\
 **F-CL10 — Cloud analytics.**\
 **F-CL11 — AI model management where applicable.**\
 **F-CL12 — User and role management.**\
 **F-CL13 — Access control.**\
 **F-CL14 — Audit information.**\
 **F-CL15 — Authorized APIs.**\
 **F-CL16 — Device/fleet management.**\
 **F-CL17 — Retention and deletion.**\
 **F-CL18 — Authorized notifications.**\
 **F-CL19 — Historical queries.**

 The target cloud deployment shall use public-cloud infrastructure capable of supporting international deployment without requiring each deployment to operate its own physical cloud infrastructure.

 ## F. User Interface Functional Requirements

 The user interface shall provide authorized users with current device status, current or most recent position, event notifications, event history, map-based visualization, battery information, communication status and historical sensor/event summaries.

 Authorized users shall be able to perform device management, user management and configuration functions according to their permissions. Event acknowledgement shall be supported where applicable, and authorized administrative users shall be able to access relevant audit information.

 The corresponding requirements are:

 **F-U01 — Current device status.**\
 **F-U02 — Current or most recent position.**\
 **F-U03 — Event notifications.**\
 **F-U04 — Event history.**\
 **F-U05 — Map-based visualization.**\
 **F-U06 — Battery information.**\
 **F-U07 — Communication status.**\
 **F-U08 — Historical summaries.**\
 **F-U09 — Authorized device management.**\
 **F-U10 — Authorized user management.**\
 **F-U11 — Authorized configuration.**\
 **F-U12 — Event acknowledgement where applicable.**\
 **F-U13 — Authorized audit information.**

 The UI shall not expose information for which the authenticated user does not have permission.

 ## G. Data Representation Requirements

 SSP shall use a compact logical representation for device-level communication and a structured representation for edge and cloud processing.

 Compact binary, CBOR, Protocol Buffers or an equivalent representation may be used for constrained device communication. JSON or an equivalent structured representation may be used for cloud APIs. The final encoding shall be selected during subsequent implementation.

 The data model shall preserve device identity, timestamps, sequence information, measurement values, units, quality or confidence information, source information and event metadata where applicable.

 ## H. Device Data

 The device data model shall include a device identifier, timestamp, sequence number, accelerometer information, gyroscope information, latitude, longitude, position confidence, proximity state, battery level, device state, communication state and event state.

 The logical representation shall support a device identifier of approximately 16 bytes, a 64-bit timestamp, inertial values represented using suitable 16-bit or floating-point values, 32-bit floating-point latitude and longitude, a position-confidence value, one-byte state fields and a sequence number.

 The exact binary packet overhead shall be determined by the selected communication protocol. The logical application payload shall remain within the packet rates up to 50 Hz, while event or high-activity operation shall support rates up to 100 Hz. Positioning shall support approximately  be updated approximately every 60 s, with a configurable range of approximately 10–60 s under limits defined below.

 ## I. Device Sampling and Packet Requirements

 The device shall support adaptive sampling. Normal accelerometer and gyroscope sampling shall support rates up to 50 Hz, while event or high-activity operation shall support rates up to 100 Hz. Positioning shall support approximately 0.1–1 Hz during normal operation, with dynamically increased updates when required by the operational context.

 Battery and device-status information shall normally be updated approximately every 60 s, with a configurable range of approximately 10–60 s under event or high-priority conditions.

 The device shall not continuously transmit every raw inertial sample during normal operation unless a diagnostic or specifically configured monitoring mode requires it.

 A normal telemetry application payload shall have a target maximum size of **128 bytes**. An event application payload shall have a target maximum size of **512 bytes**. These limits exclude lower-layer protocol overhead.

 ## J. Device Data Volume and Communication Performance

 Normal application traffic shall not exceed an average target of **10 kbit/s per device**. The device-to-edge communication link shall provide a target application capacity of at least **100 kbit/s per device**, providing capacity for event bursts, retransmissions and protocol overhead.

 The target event-burst capacity shall be at least **50 kbit/s per device**.

 ## K. Edge Data

 The edge shall transform device information into structured records containing, as applicable, device identifier, measurement timestamp, edge reception timestamp, sequence number, sensor or feature values, position, position confidence, battery state, communication state, event state, processing status and source identifier.

 The target maximum size of a structured edge record shall be **1 kB**.

 Normal aggregated telemetry shall normally be forwarded toward the cloud at approximately 10–60 s intervals. Event information shall be forwarded immediately when connectivity is available.

 ## L. Edge-to-Cloud Data

 A telemetry record shall contain device identifier, timestamp, data type, measurement, unit, quality or confidence information, source and sequence number.

 An event record shall additionally contain event identifier, event type, severity, confidence, triggering information, event timestamp, processing status and acknowledgement status where applicable.

 The target maximum application size for a normal telemetry or event record shall be **1 kB**. Larger historical responses shall use pagination.

 ## M. Cloud Data

 Cloud information shall be organized into telemetry data, event data, device-management data and user/audit data.

 The cloud data model shall support chronological queries, device-based queries, event-based queries, aggregation, analytics, retention control, deletion and auditing.

 ## N. UI and API Data

 The UI shall normally request processed and summarized information rather than continuously retrieving raw sensor streams.

 Normal responses shall include current device state, current or recent position, recent events, battery state, communication state, historical summaries and authorized configuration information.

 The target normal UI/API response size shall be **100 kB or less per request/page**. Larger historical responses shall use pagination.

 ## O. Computational Performance

 The device shall provide sensor-acquisition latency of no more than **20 ms**, local preprocessing latency of no more than **100 ms**, local event-rule evaluation of no more than **200 ms**, and event-decision generation of no more than **500 ms** under nominal operating conditions.

 Local buffer-write latency shall not exceed **100 ms**, and average local processing duty cycle shall target no more than **20%** during normal operation.

 For device-to-edge operation, nominal application latency shall target **2 s or less**. The system shall support at least **24 h** of relevant offline buffering.

 ## P. Communication Performance

 The device-to-edge communication link shall be wireless, short-range, low-power and bidirectional. The target nominal range shall be at least **10 m**, with **5 m** considered a minimum practical range target for constrained deployment scenarios.

 The target application-level capacity shall be at least **100 kbit/s**, and typical communication latency shall target **500 ms or less**. Event delivery shall target **2 s or less** under nominal connectivity conditions.

 The edge-to-cloud communication path shall use wireless wide-area connectivity suitable for the intended deployment. The minimum application-capacity target shall be **50 kbit/s per device**, while typical event latency shall target **5 s or less** under nominal network conditions.

 The system shall support operation during external-network interruption and synchronization after recovery.

 ## Q. Communication Resilience

 During cloud connectivity loss, the device shall continue local monitoring, relevant events shall be buffered and the edge shall continue selected local processing where available. After reconnection, buffered information shall be synchronized.

 Sequence numbers shall support identification of missing or duplicated information, and duplicate messages shall be detectable. Critical events shall not be silently discarded solely because cloud connectivity is unavailable.

 The target minimum buffering capacity for relevant event and status information shall be **24 h**.

 ## R. Energy Performance

 Energy consumption shall be considered a primary system constraint because the device is intended to be wearable or portable.

 The device shall target a deep-sleep power level of **1 mW or less**, normal-monitoring average power of **50 mW or less**, active-sensing average power of **150 mW or less**, communication burst power of **500 mW peak or less**, and positioning active power of **300 mW peak or less**.

 The minimum target battery autonomy shall be **7 days**, while the engineering objective shall be **14 days** under nominal monitoring conditions.

 The energy model shall consider sleep, sensing, local computation, positioning, wireless transmission, wireless reception and event processing. Adaptive operation shall be used to reduce unnecessary energy expenditure.

 The edge shall normally be treated as externally powered infrastructure. If a later deployment scenario requires a battery-powered portable edge gateway, an additional energy budget shall be defined during architecture and hardware design rather than assumed in D2.

 ## S. Mechanical and Environmental Performance

 The target device volume shall not exceed **100 cm³**, and the target device mass shall not exceed **100 g**. The device shall use a wearable or portable form factor.

 The target operating temperature range shall be **−10 °C to +50 °C**, with a storage range of **−20 °C to +60 °C**. The target ingress-protection level shall be **IP65 or better**, and the target drop-resistance requirement shall be at least **1 m**.

 If a dedicated physical edge gateway is required, its target mass shall not exceed **500 g** and its target volume shall not exceed **2 L**. Passive cooling shall be preferred and continuous operation shall be supported. These requirements shall be treated as deployment-dependent because an edge function may alternatively be hosted on an existing smartphone, computer or gateway.

 ## T. Cloud Performance and Scalability

 The initial cloud deployment shall support at least **100 active devices**. The architecture shall have a scalability objective of at least **10,000 devices**, without requiring 10,000 devices to be deployed during the academic project.

 The initial cloud capacity shall target at least **100 telemetry messages/s**, with event-ingestion burst capacity of at least **20 events/s**.

 Normal API queries shall target a **p95 latency of 1 s or less**, and cloud event processing shall target a **p95 latency of 2 s or less**.

 The target cloud service availability shall be **99.5% or greater** under the conditions of the selected cloud deployment.

 Historical information shall be retained for at least **12 months**, subject to applicable privacy and data-retention policies.

 ## U. Cloud Storage

 For planning purposes, a representative telemetry record size of 200 bytes and an update interval of 30 s gives:

 $$
200 \times \frac{86400}{30}=576000\text{ bytes/day}
$$

 This corresponds to approximately **0.576 MB per device per day** before infrastructure overhead.

 For 1,000 devices, the corresponding raw application data volume is approximately **576 MB/day**, or approximately **210 GB/year**.

 For 10,000 devices, the corresponding raw application data volume is approximately **2.1 TB/year**.

 These values exclude database indexes, replication, metadata, backups and other infrastructure overhead. The initial cloud deployment shall therefore provide at least **500 GB of usable application storage**, while the production-oriented solution shall support scalable expansion beyond this capacity.

 ## V. User Interface Performance

 The UI shall target a login response time of **2 s or less**, dashboard loading of **3 s or less**, current-status refresh of **5 s or less**, event display within **5 s** after cloud ingestion, historical-query p95 latency of **2 s or less**, and map display within **3 s** under nominal conditions.

 The UI shall remain usable on desktop and mobile-class displays and shall prioritize current state, current or recent position, significant events, battery state and communication state.

 ## W. End-to-End Event Performance

 Operationally significant events may originate at the device, edge or cloud level. Each event shall contain, as applicable, an event type, timestamp, source, severity, confidence or quality information and relevant triggering information.

 Under nominal connectivity conditions, the target end-to-end path is:

 **Sensor → Device/Edge → Cloud → UI ≤10 s**

 For high-priority events, the target is:

 **Sensor → Device/Edge → Cloud → UI ≤5 s**

 These targets are not guarantees during external-network unavailability.

 ## X. Security Requirements

 SSP shall provide unique device identities, authenticated device communication, authenticated user access, role-based authorization, encrypted communication, protected credential storage, secure update mechanisms, audit logging and appropriate session management.

 The system shall provide mechanisms for detecting replay, duplication or invalid message sequences where required by the selected communication protocol.

 The final cryptographic algorithms and key-management implementation shall be selected during subsequent engineering stages.

 ## Y. Privacy Requirements

 SSP shall process potentially sensitive location and movement information according to data-minimization principles.

 Only information necessary for the intended function shall be collected or transmitted. Raw sensor information shall not automatically be transmitted when derived information is sufficient to satisfy the required function.

 Sensitive information shall be protected in transit and at rest. Access shall be role-based, retention periods shall be configurable, deletion shall be supported and administrative access shall be auditable.

 The final implementation shall comply with applicable privacy and data-protection requirements for the intended deployment.

 ## Z. AI Functional and Performance Scope

 AI shall be treated as an optional intelligence capability. Potential AI-assisted functions include movement classification, activity recognition, anomaly detection, contextual event classification, false-event reduction and predictive maintenance.

 Deterministic rules shall remain available for functions that do not require machine learning.

 The initial AI cloud services, initial deployment services and an appropriate maintenance or replacement allowance. Development, certification and organizational costs shall be identified separately in later example, the functional requirement that the device shall determine its position is complemented by performance requirements concerning update frequency, latency and energy targets shall include classification accuracy of **at least 90%** on representative validation data, event recall of **at least 90%**, a target false-positive rate of **5% or less**, and edge inference latency of **200 ms or less** where edge inference is implemented.

 The target system shall support model updating and model-performance monitoring where AI functions are deployed.

 These values are development targets. Their final interpretation shall be refined after the datasets, event classes and validation methodology have been defined.

 ## AA. Economic Requirements

 The target production-oriented hardware cost shall be **€150 or less per device** for the initial low-volume design. The engineering objective for larger-scale production shall be **€100 or less per device**.

 The target recurring communication and cloud operating cost shall be **€10 or less per device per month** under normal operating conditions.

 For an initial deployment of 100 devices, the system-level first-year operational target shall be **€25,000 or less**, excluding personnel salaries and academic project-development labor.

 This global target may include device hardware, batteries and accessories, edge infrastructure, communication, cloud services, initial deployment services and an appropriate maintenance or replacement allowance. Development, certification and organizational costs shall be identified separately in later economic analysis.

 ## AB. Functional–Performance Relationship

 The distinction between function and performance shall be maintained throughout the project.

 For example, the functional requirement that the device shall determine its position is complemented by performance requirements concerning update frequency, latency and energy consumption.

 Similarly, the functional requirement that the system shall detect relevant events is complemented by measurable requirements concerning local decision–F-D12, F-E01–F-E15, F-C01–F-C12, F-CL01–F-CL19 and F-U01–F, UI, security, privacy, AI and economic requirements shall similarly be verified using appropriate analytical calculations, laboratory measurementssearch activity performed during the earlier project work. Instead, this chapter retains the observations that latency and end-to-end event latency.

 The functional requirement that the system shall transmit telemetry is complemented by requirements concerning packet size, traffic volume, communication capacity, range and latency.

 The functional requirement that the cloud shall store historical information is complemented by requirements concerning storage capacity, retention, query latency and scalability.

 This separation ensures that subsequent architecture and implementation decisions can be evaluated against both required capabilities and measurable engineering constraints.

 ## AC. Requirement Traceability

 The functional requirements F-D01–F-D12, F-E01–F-E15, F-C01–F-C12, F-CL01–F-CL19 and F-U01–F-U13 shall be verified during subsequent implementation and validation deliveries.

 The corresponding data, communication, energy, mechanical, cloud, UI, security, privacy, AI and economic requirements shall similarly be verified using appropriate analytical calculations, laboratory measurements, implementation tests, simulations or documented evaluation methods.

 The requirement-to-delivery relationship is:

 **D2 requirements → D3 architecture evaluation → D4 hardware and implementation validation → D5 AI/edge-AI validation → D6 final validation and economics**

 # IV. EXISTING SOLUTIONS, MARKET CONTEXT AND REQUIREMENTS IMPLICATIONS

 ## A. Purpose of the Market Study

 The purpose of the market study within D2 is not to repeat the complete market-research activity performed during the earlier project work. Instead, this chapter retains the observations that are directly relevant to the functional and performance requirements defined in Chapter 3.

 Existing commercial safety and tracking systems establish an important baseline for the SSP design. Their documented capabilities demonstrate that location monitoring, geofencing, event notification, historical information and application-based monitoring are established expectations in the target provides near-real-time location tracking, virtual boundaries, location history and motion alerts. Its documented system combines positioning with a wide-area cellular network and also provides a configurable tracking experience intended to balance tracking behavior and battery consumption.  Its documented live-tracking function provides location updates at increased frequency for a limited period, while noting domain.

 ## B. Existing Location and Tracking Functions

 T-Mobile's SyncUP TRACKER provides near-real-time location tracking, virtual boundaries, location history and motion alerts. Its documented system combines positioning with a wide-area cellular network and also provides a configurable tracking experience intended to balance tracking behavior and battery consumption.  T-Mobile+1

 T-Mobile's SyncUP KIDS Watch provides real-time GPS location tracking and virtual-boundary alerts through its application. Its documented live-tracking function provides location updates at increased frequency for a limited period, while noting the associated increase in battery consumption.  T-Mobile+1

 AngelSense provides continuous monitoring, real-time location visualization, geofencing, historical activity information and proactive notifications. Its documented geofence behavior also illustrates that location interpretation may require multiple observations because individual positioning measurements can contain errors.  AngelSense+1

 These examples demonstrate that the following capabilities are already established in commercial systems:

 **Location monitoring → geofencing → notifications → historical information → application-based monitoring**

 SSP therefore shall not treat these functions individually as sufficient evidence of innovation.

 ## C. Implications for SSP Requirements

 The market evidence supports the inclusion of reliable location information, event notifications, historical information and authorized user monitoring in SSP. It also supports the requirement that monitoring intensity should be adaptable to operational context rather than necessarily remaining at a constant maximum level.

 The market study consequently establishes a baseline against which SSP requirements shall be interpreted:

 **Established market functions → SSP baseline requirements**

 The intended SSP improvement is instead associated with the integration and measurable engineering treatment of distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and communication-resilient operation.

 ## D. Distributed Processing as an Improvement Objective

 Existing commercial systems demonstrate the importance of centralized monitoring and application-level interaction. SSP extends the requirements perspective by explicitly defining processing capabilities at different computational levels.

 The intended operational relationship is:

 **Local sensing and processing → edge processing → cloud analytics → authorized user**

 The D2 requirements therefore include local preprocessing, local event detection, edge feature extraction, edge event evaluation, low-latency inference and cloud analytics.

 These requirements do not imply that all functions must be implemented simultaneously at all levels. The final allocation shall depend on latency, energy, computational resources, connectivity, privacy and model complexity.

 ## E. Adaptive and Energy-Aware Monitoring

 Commercial tracking systems already demonstrate that tracking frequency can influence battery consumption. T-Mobile documents configurable tracking behavior and explicitly notes that increased live-tracking activity can reduce battery life.  T-Mobile+1

 SSP therefore treats adaptive monitoring not merely as a convenience but as an engineering requirement connected to energy consumption, communication volume and event responsiveness.

 The intended relationship is:

 **Monitoring intensity ↔ responsiveness ↔ communication volume ↔ energy consumption**

 The measurable D2 targets for sampling, communication traffic, operating-state power and battery autonomy provide a basis for validating this relationship experimentally.

 ## F. Contextual Event Interpretation

 Existing systems demonstrate the practical importance of geofence and movement-based alerts. AngelSense, for example, documents arrival, departure, unexpected-location and route-related notifications.  AngelSense+1

 SSP therefore defines event processing as more than a simple threshold notification. The intended requirement progression is:

 **Sensor information → contextual interpretation → event classification → risk assessment → prioritized notification**

 This does not require AI for every event. Deterministic rules shall remain available, retention of location information for its KIDS Watch service.  for example, describes SyncUP TRACKER as relying on its LTE network for remote location tracking.  while AI-assisted interpretation may be introduced where it provides measurable benefit.

 ## G. Privacy-Aware Information Flow

 Location and movement information can be sensitive. Existing commercial systems demonstrate that such information is collected and retained as part of monitoring services; for example, T-Mobile documents retention of location information for its KIDS Watch service.  T-Mobile

 SSP consequently defines privacy as a system-level design objective rather than only a cloud-security feature.

 The intended information-flow principle is:

 **Raw sensing → local processing → necessity assessment → minimized transmission → controlled storage → authorized access → configurable retention/deletion**

 This principle directly motivates the D2 requirements concerning local preprocessing, event-oriented communication, role-based access, encryption, retention, deletion and auditability.

 ## H. Communication Resilience

 Commercial tracking systems generally depend on external communication networks for remote monitoring. T-Mobile, for example, describes SyncUP TRACKER as relying on its LTE network for remote location tracking.  T-Mobile

 SSP therefore explicitly defines temporary connectivity loss as an operational scenario. The system shall continue selected local and edge functions, buffer relevant information and synchronize after communication recovery.

 The intended progression is:

 **Connectivity available → normal operation**

 **Connectivity unavailable → local/edge continuity → buffering → synchronization → normal operation**

 This requirement establishes resilience as an explicit engineering property of SSP.

 ## I. Market Baseline and Intended SSP Differentiation

 The market study indicates that location tracking, geofencing, notifications, historical information and mobile monitoring are established capabilities. SSP should therefore be evaluated against a broader set 1 establishes the motivation, scope and intended improvement objectives of SSP. Chapter 2 describes the principal actors and, more importantly, the operational scenarios through which SSP is expected to be used. These scenarios provide the basis for the requirements in Chapter 3, computational performance, communication characteristics, resilience, energy consumption, mechanical and environmental constraints, cloud scalability and of engineering dimensions.

 The intended areas for investigation and improvement are:

 **Distributed processing → adaptive monitoring → energy-aware operation → privacy-aware information flow → contextual event interpretation → resilient operation**

 These areas are translated into measurable D2 requirements for processing latency, communication volume, battery autonomy, offline buffering, event latency, privacy-related data reduction, cloud scalability and AI performance.

 ## J. Competitiveness Statement

 D2 shall not claim that SSP is already commercially superior or more competitive than existing products.

 A meaningful competitiveness assessment requires an implemented system, measured technical performance, verified energy consumption, demonstrated reliability, actual hardware and operating costs, and a comparison against specific competing products under defined conditions.

 The appropriate D2 conclusion is therefore:

 **Market study → established baseline → identified improvement objectives → measurable SSP requirements**

 rather than:

 **Market study → unsupported claim of superiority**

 The subsequent deliveries shall provide the evidence required to determine which intended improvements are actually achieved.

 # V. CONCLUSION

 This D2 document establishes the functional and performance specifications of the Smart Safety and Protection IoT system.

 The document follows the progression:

 **SSP concept → target users and operational scenarios → functional and performance requirements → existing solutions and market implications**

 Chapter 1 establishes the motivation, scope and intended improvement objectives of SSP. Chapter 2 describes the principal actors and, more importantly, the operational scenarios through which SSP is expected to be used. These scenarios provide the basis for the requirements in Chapter 3.

 Chapter 3 defines the required functions of the device, edge, communication subsystem, cloud services and user interface. It also specifies data representation and volume, computational performance, communication characteristics, resilience, energy consumption, mechanical and environmental constraints, cloud scalability and storage, UI performance, security, privacy, AI and economic requirements.

 Chapter 4 establishes the market baseline. Existing commercial solutions demonstrate that location tracking, geofencing, notifications, historical information and application-based monitoring are established functions. SSP therefore does not claim these functions individually as novel. defined in D2 are design targets and have not yet been presented as experimentally achieved results. Their feasibility and actual performance shall be evaluated in subsequent deliveries Instead, the D2 requirements establish intended areas of improvement through distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation.

 The requirements defined in D2 are design targets and have not yet been presented as experimentally achieved results. Their feasibility and actual performance shall be evaluated in subsequent deliveries.

 The resulting project progression is:

 **Problem → SSP concept → Users → Usage → Requirements → Existing solutions → Architecture → Implementation → Validation**

 The architecture is deliberately excluded from this D2 and shall be addressed in D3.

 # REFERENCES

 \[1\] IEEE Author Center, “IEEE Article Templates,” IEEE.  IEEE Article Templates

 \[2\] IEEE Author Center, “Structure Your Article,” IEEE.  Structure Your Article

 \[3\] IEEE Author Center, “Authoring Tools and Templates,” IEEE.  Authoring Tools and Templates

 \[4\] T-Mobile, “SyncUP TRACKER,” T-Mobile Support.  SyncUP TRACKER documentation

 \[5\] T-Mobile, “SyncUP KIDS Watch,” T-Mobile.  SyncUP KIDS Watch

 \[6\] T-Mobile, “SyncUP TRACKER,” T-Mobile Newsroom.  T-Mobile SyncUP TRACKER overview

 \[7\] T-Mobile, “SyncUP KIDS Watch Support & Set Up,” T-Mobile Support.  SyncUP KIDS Watch support

 \[8\] T-Mobile, “SyncUP KIDS Watch Privacy Notice,” T-Mobile.  T-Mobile privacy notice

 \[9\] AngelSense, “Safeguard GPS Location Tracker,” AngelSense.  AngelSense GPS Location Tracker

 \[10\] AngelSense, “Named Places (Geofences),” AngelSense Help Center.  AngelSense geofences

 \[11\] AngelSense, “Notification Types,” AngelSense Help Center.  AngelSense notification types

 \[12\] IEEE, “IEEE Editorial Style Manual for Authors,” IEEE Author Center.  IEEE Editorial Style Manual

 This version is the one I would use as the **D2 baseline going forward**. The important correction is that the previous document's quantitative material has not been discarded; it has been moved into the requirements chapter and connected explicitly to the operational scenarios and market evidence.
