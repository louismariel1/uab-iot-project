 # D2 — SmartSecurePerimeter (SSP)

 ## Chapters 1–4: Problem Definition, Operational Scenarios, Market and Context Analysis, and System Requirements

---

 # Chapter 1. SmartSecurePerimeter Concept, Problem Definition and Objectives

 ## 1.1 Introduction

 The SmartSecurePerimeter (SSP) project investigates the development of an intelligent IoT-based monitoring and protection system capable of supporting location-aware, proximity-aware and context-aware protection scenarios.

 The fundamental concept is based on the continuous observation of relevant physical and contextual conditions associated with a monitored person, device or geographical area. The system is intended to determine whether the observed conditions remain consistent with an authorized monitoring policy and, when relevant conditions occur, to provide appropriate information to authorized users or operational systems.

 The SSP concept is therefore broader than a conventional location-tracking system. Its intended operation can be represented as:

 **Sensing -\> Positioning -\> Context interpretation -\> Event assessment -\> Communication -\> Operational response**

 The project further investigates whether this process can be made more efficient and resilient through distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation.

 The objective of the project is not to claim that these capabilities are individually novel. Technologies such as GNSS, BLE, inertial sensing, cellular communication, cloud computing, geofencing and machine learning are already established. The engineering objective is instead to investigate how these capabilities can be integrated and coordinated within a coherent IoT protection system.

---

 ## 1.2 Problem Definition

 Location-aware protection applications operate under several simultaneous constraints. The system must obtain sufficiently reliable information about position and movement, determine whether observed conditions correspond to relevant operational events, communicate important information in a timely manner and remain operational despite limitations in energy, connectivity, computation and environmental conditions.

 A simple monitoring process can be represented as:

 **Sense -\> Transmit -\> Central processing -\> Alert**

 Such an approach can be appropriate for relatively simple monitoring requirements, but it does not necessarily exploit the information available close to the data source or account explicitly for uncertainty, energy constraints, communication disruption or privacy considerations.

 SSP therefore investigates a more general operational process:

 **Sense -\> Interpret -\> Assess -\> Select information -\> Communicate -\> Respond -\> Learn**

 The distinction is important. The second representation does not prescribe a particular technical architecture; rather, it defines the intended system behavior that subsequent engineering work must translate into an implementable architecture.

---

 ## 1.3 SSP Concept

 SSP is conceived as an IoT-based monitoring platform capable of combining positioning, motion, proximity, device-state and communication information to support authorized protection and perimeter-monitoring scenarios.

 The system is intended to operate across three conceptual processing domains:

 **Device -\> Edge/Mobile -\> Cloud**

 These domains are introduced here as functional processing concepts rather than as a finalized technical architecture. The detailed allocation of functions among them is intentionally deferred to Chapter 5.

 The Device domain represents information generated close to the monitored physical environment. The Edge/Mobile domain represents intermediate processing that can provide local or near-local interpretation and resilience. The Cloud domain represents centralized processing, historical analysis, fleet management and system-wide services.

 The central engineering principle is:

 **Function -\> Operational requirement -\> Appropriate processing location**

 Consequently, a function should not automatically be centralized or decentralized. Its allocation should be determined according to latency, energy, privacy, computational requirements, connectivity and resilience.

---

 ## 1.4 Intended Application Context

 SSP is intended as a general technological platform that can be adapted to authorized applications in which geographical, proximity or contextual monitoring is required.

 Potential application contexts include personal protection, authorized perimeter monitoring, connected wearable monitoring and other IoT applications in which the system must determine whether monitored conditions remain within predefined operational rules.

 The project does not assume that a single configuration is appropriate for all applications. Instead, SSP is intended to provide configurable policies and system functions that can be adapted to the requirements of a particular deployment.

 The relationship can therefore be expressed as:

 **Application scenario -\> Operational policy -\> Monitoring requirements -\> System behavior**

 The legal, institutional and regulatory conditions of a real deployment are outside the scope of the generic SSP concept and would require separate assessment for each application.

---

 ## 1.5 Fundamental SSP Operating Principle

 The intended SSP operating principle is based on continuous contextual monitoring rather than isolated sensor measurements.

 A position measurement alone may not fully describe an operational situation. Motion information may provide additional context, while proximity information may provide evidence about relative presence. Device state and communication state may further affect the interpretation of an event.

 The intended information relationship is therefore:

 **Position + Motion + Proximity \+ Device state + Communication state + Historical context -\> Event interpretation**

 The resulting interpretation may then influence monitoring intensity, processing requirements and communication priority.

 This produces an adaptive relationship:

 **Operational context -\> Monitoring intensity -\> Processing intensity -\> Communication intensity -\> Energy consumption**

 The purpose of this relationship is to investigate whether system resources can be concentrated on operationally significant situations without unnecessarily maintaining maximum resource consumption under all conditions.

---

 ## 1.6 Project Objectives

 The primary objective of SSP is to define, engineer and evaluate an IoT-based monitoring platform capable of supporting reliable, secure, privacy-aware and adaptive protection-oriented monitoring.

 The project objectives are to investigate the integration of sensing, positioning, event detection, contextual assessment, communication, operational visualization and lifecycle management within a coherent system.

 A second objective is to investigate distributed processing. Functions may be processed close to the source of information when this provides measurable benefits in latency, energy consumption, privacy, connectivity resilience or operational continuity.

 A third objective is to investigate adaptive monitoring. The system should be capable of changing sensing, processing and communication behavior according to operational context rather than continuously operating at maximum intensity.

 A fourth objective is to investigate energy-efficient operation. The system should reduce unnecessary sensing, processing and communication while preserving functions that are necessary for the required level of protection.

 A fifth objective is to investigate privacy-aware information flow. Information should be collected, processed, transmitted and retained according to operational necessity.

 A sixth objective is to investigate contextual and predictive event interpretation. Relevant information may be combined to distinguish between conditions that would otherwise appear similar when evaluated using a single measurement.

 A seventh objective is to investigate resilient operation during temporary communication or subsystem failures.

 An eighth objective is to investigate distributed AI capabilities where machine-learning methods provide a measurable benefit over appropriate deterministic or statistical alternatives.

---

 ## 1.7 SSP Improvement Objectives

 The intended improvements of SSP are defined as engineering objectives rather than claims of already demonstrated superiority.

 At the Device level, SSP is intended to investigate local preprocessing, adaptive sensing, device-state monitoring, selected event detection, local buffering and secure lifecycle management. These capabilities are intended to reduce unnecessary raw-data transmission, reduce energy consumption and maintain useful operation during temporary connectivity interruptions.

 At the Edge/Mobile level, SSP is intended to investigate processing beyond simple communication forwarding. Intermediate processing may validate, filter, aggregate and interpret information before transmission to centralized services. This may reduce unnecessary cloud traffic, support lower-latency decisions and provide continued operation during selected cloud connectivity disruptions.

 At the Cloud level, SSP is intended to support centralized historical storage, scalable event ingestion, system-wide analytics, fleet management, model management, authorized access and integration with external systems.

 Privacy is treated as an architectural and system-level objective. Where an operational function can be satisfied using processed, aggregated or event-oriented information rather than continuous transmission of raw information, the system should investigate the lower-data approach.

 AI is treated as a distributed capability rather than a cloud-only function. Lightweight processing may be performed close to the data source, more computationally demanding inference may be performed at an intermediate processing layer, and computationally intensive analytics and model-management functions may be performed centrally.

 Energy efficiency is similarly treated as a system-level objective. The intended relationship is:

 **Operational context -\> Adaptive sensing -\> Local processing -\> Selective communication -\> Reduced energy consumption**

 These objectives will only be considered achieved if later engineering and validation activities demonstrate measurable performance against the requirements established in Chapter 4.

---

 ## 1.8 Scope and Boundaries

 D2 defines the problem, operational context, requirements and engineering specifications for SSP. It does not define the final implementation architecture.

 The selection of specific processors, positioning modules, communication technologies, sensors, cloud services, machine-learning models or hardware configurations belongs to subsequent engineering chapters.

 The distinction is therefore:

 **Chapters 1–4 -\> What SSP is intended to achieve**

 **Chapter 5 onward -\> How SSP will achieve it**

 This separation prevents implementation assumptions from being introduced before the requirements have been established.

---

 ## 1.9 D2 Methodological Principle

 The D2 methodology follows the engineering progression:

 **Problem -\> Users and scenarios -\> Existing solutions -\> Improvement opportunities -\> Requirements -\> Architecture -\> Implementation -\> Validation**

 The requirements defined later in this document therefore originate from the operational scenarios and the analysis of existing technologies rather than being selected arbitrarily.

 The fundamental engineering relationship is:

 **Stakeholder need -\> Operational scenario -\> Context analysis -\> System requirement -\> Design decision -\> KPI -\> Test -\> Result**

---

 ## 1.10 Chapter 1 Conclusion

 SSP is proposed as an IoT monitoring and protection platform that investigates the integration of sensing, positioning, contextual interpretation, adaptive operation, distributed intelligence, secure communication, privacy-aware processing and resilient system behavior.

 The individual technologies required to support these functions already exist. The engineering challenge is to determine how they can be integrated and allocated within a system that satisfies measurable operational requirements.

 Chapter 2 therefore examines how SSP is expected to be used by its users and how the system should behave in representative operational scenarios.

---

 # Chapter 2. Target Users, Use Cases and Operational Scenarios

 ## 2.1 Purpose of the Chapter

 The purpose of this chapter is to describe SSP from the perspective of its users and operational environment.

 The chapter does not define the technical architecture. Instead, it establishes the interactions, events, decisions and responses that the technical system must ultimately support.

 The progression is:

 **Users -\> Use cases -\> Operational scenarios -\> Expected system behavior -\> Requirements**

 This approach ensures that the requirements developed later are grounded in actual system use rather than being derived only from technology capabilities.

---

 ## 2.2 SSP Actors and Users

 The principal SSP actors are the protected person, the monitored person, the protection operator, the system administrator, the authorized organization and the technical or service operator.

 The protected person is the person whose protection perimeter or relevant protection condition is being monitored.

 The monitored person is the person associated with a monitored device whose position, movement or proximity may be subject to an authorized monitoring rule.

 The protection operator is the authorized user responsible for monitoring events, interpreting alerts and applying the applicable operational procedure.

 The system administrator manages users, devices, monitoring policies, configuration and system-level settings.

 The authorized organization is the institution responsible for deploying and operating SSP within a defined application context.

 The technical or service operator maintains the technical infrastructure, including devices, connectivity, software services and supporting infrastructure.

 These actors provide the vocabulary required to understand the operational scenarios that follow.

---

 ## 2.3 Core SSP Use-Case Model

 At a conceptual level, SSP can be represented as a monitoring system connecting the monitored environment with authorized operational users.

```
                 Authorized Operator
                         |
                         v
                  Monitor SSP
                         |
                         v
Protected Person -> SSP Monitoring <- Monitored Person
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
          Location      Risk       Device
           Status     Assessment    Status
             |           |           |
             +-----------+-----------+
                         |
                         v
                       Alert
                         |
                         v
                Operational Action
```

 This model is deliberately conceptual. It describes operational interaction and does not define the technical Device–Edge–Cloud architecture.

---

 ## 2.4 Use Case 1 — Normal Monitoring

 Normal monitoring represents the baseline operating condition of SSP.

 The monitored device is activated and acquires the information required by the current monitoring policy. Relevant position and motion information is evaluated, and the system determines what information needs to be communicated.

 The operational sequence can be represented as:

 **Device activated -\> Information acquired -\> Local interpretation -\> Policy-based communication -\> Status updated -\> Authorized operator observes status -\> Adaptive monitoring continues**

 Normal monitoring does not necessarily require continuous transmission of all raw sensor information. The operational scenario therefore introduces the principle that the amount and type of information transmitted may depend on the current monitoring state.

 This behavior later becomes relevant to the requirements for energy efficiency, privacy, communication and distributed processing.

---

 ## 2.5 Use Case 2 — Approach to a Protected Perimeter

 The approach to a protected perimeter represents a central SSP scenario because it demonstrates the difference between simple location tracking and contextual monitoring.

 A monitored person may initially be operating in a normal state. As movement continues, the system evaluates position and motion information. Where sufficient information is available, the system may assess the direction and characteristics of movement relative to the protected perimeter.

 The conceptual sequence is:

 **Movement -\> Position and motion evaluation -\> Trajectory/proximity assessment -\> Perimeter approach detected -\> Risk level increases -\> Monitoring policy adapts -\> Predictive assessment -\> Warning threshold reached -\> Authorized notification -\> Operational response**

 The scenario does not imply that a predictive algorithm must ultimately be used. Rather, it establishes an operational requirement for the system to support increasingly informative assessment when the context becomes more significant.

---

 ## 2.6 Use Case 3 — High-Risk or Critical Event

 A high-risk event represents a situation in which multiple observations indicate that an operational threshold has been reached.

 The sequence can be represented as:

 **Abnormal movement or perimeter condition -\> Local event detection -\> Risk assessment -\> High-risk condition -\> Priority communication -\> Edge or centralized assessment -\> Critical event confirmation -\> Immediate alert -\> Authorized operational response**

 The scenario establishes that event severity should influence system behavior.

 A critical event may therefore require different sensing, processing and communication behavior from routine status information.

---

 ## 2.7 Use Case 4 — Temporary Connectivity Loss

 Connectivity loss is treated as a normal engineering condition rather than an impossible event.

 The operational sequence is:

 **Normal monitoring -\> Connectivity disruption -\> Communication failure detected -\> Local functions continue -\> Relevant events buffered -\> Critical monitoring maintained -\> Connectivity restored -\> Buffered information synchronized -\> Normal operation resumes**

 The exact implementation is deferred to subsequent chapters. The requirement established by the scenario is that temporary communication loss should not automatically result in complete loss of monitoring functionality.

---

 ## 2.8 Use Case 5 — Device Tampering or Abnormal Device State

 SSP must also account for conditions in which the device itself behaves unexpectedly or indicates possible tampering.

 The operational sequence is:

 **Normal device operation -\> Abnormal or tamper condition -\> Local validation -\> Event classification -\> Priority communication -\> Event processing -\> Operator notification -\> Operational response**

 The scenario connects physical device integrity with the operational monitoring system and therefore establishes requirements for tamper awareness, device-state monitoring, security and event reporting.

---

 ## 2.9 Use Case 6 — Privacy-Aware Monitoring

 SSP may generate information containing sensitive location, movement or proximity data. The system should therefore determine whether information generated at one layer is actually required by another layer.

 The conceptual sequence is:

 **Information generated -\> Local processing -\> Information classified -\> Operational necessity evaluated -\> Necessary information transmitted according to policy -\> Unnecessary raw information retained or discarded according to policy -\> Monitoring continues**

 The scenario does not prescribe a particular privacy mechanism. It establishes the desired system behavior.

 This principle later becomes a formal requirement:

 **Operational requirement -\> Minimum necessary information -\> Controlled information flow**

---

 ## 2.10 Use Case 7 — Operator Workflow

 The operator workflow the monitored devices and their current operational status. Relevant information may include position, risk status, battery condition, connectivity and active describes SSP from the perspective of the person responsible for monitoring and responding to events.

 The operator accesses the system and reviews the monitored devices and their current operational status. Relevant information may include position, risk status, battery condition, connectivity and active alerts.

 If no significant event exists, monitoring continues.

 If an alert is generated, the operator reviews the available contextual information, determines the applicable operational procedure and records or closes the event according to the authorized workflow.

 The conceptual process is:

 **Operator authentication -\> Current status -\> Event monitoring -\> Alert detected -\> Context reviewed -\> Operational procedure applied -\> Event recorded -\> Monitoring continues**

 This scenario provides the basis for later requirements concerning visualization, role-based access, alert prioritization and operational traceability.

---

 ## 2.11 End-to-End SSP Operational Storyboard

 The complete operational concept can be represented as:

```
+----------------+
|  Environment   |
+-------+--------+
        |
        v
+----------------+
|  SSP Device    |
|  Sensing       |
|  Position      |
|  Motion        |
+-------+--------+
        |
        v
+----------------+
| Local          |
| Interpretation |
+-------+--------+
        |
        v
+----------------+
| Edge/Mobile    |
| Assessment     |
| Prediction     |
| Risk           |
| Privacy        |
+-------+--------+
        |
        v
+----------------+
| Cloud          |
| Analytics      |
| Management     |
| Historical     |
| Information    |
+-------+--------+
        |
        v
+----------------+
| Authorized     |
| User           |
+-------+--------+
        |
        v
+----------------+
| Operational    |
| Response       |
+----------------+
```

 The operational response can influence subsequent system behavior:

 **Operational response -\> Policy/configuration -\> Monitoring behavior -\> Device/Edge operation**

 This feedback relationship is important because SSP is intended to be a configurable operational system rather than a static sensor network.

---

 ## 2.12 Stakeholder Interaction Summary

 The principal interactions can be summarized as follows.

 | Actor | Interaction with SSP | Principal information |
| --- | --- | --- |
| Protected person | Receives authorized protection-related information | Alerts and protection status |
| Monitored person | Carries or uses the monitored device | Position, motion and device status |
| Protection operator | Monitors events and applies operational procedures | Location, risk, alerts and device status |
| System administrator | Manages users, devices and policies | Configuration and management information |
| Authorized organization | Deploys and operates SSP | Operational and management information |
| Technical/service operator | Maintains technical infrastructure | Device, connectivity and system-health information |

The table supports the operational scenarios rather than replacing them.

---

 ## 2.13 Chapter 2 to Chapter 3 Transition

 The use cases presented in this chapter define how SSP is expected to operate from the perspective of its users and operational environment. They identify the principal interactions, events, decisions and responses that the system must support.

 The next question is therefore:

 **How are these needs addressed by existing systems and technologies, and where are opportunities for improvement?**

 Chapter 3 addresses this question through a market, technology and context analysis.

---

 # Chapter 3. Market, Technology and Context Analysis

 ## 3.1 Purpose of the Market and Context Analysis

 The purpose of this chapter is to establish the technological, operational and market context in, BLE, cellular communication, geofencing, cloud computing and machine learning are already established. SSP instead investigates which SSP is proposed.

 The analysis considers existing operational solutions, relevant technological capabilities, security and privacy considerations, and areas in which the integration of existing capabilities may provide opportunities for improvement.

 The reasoning chain is:

 **Existing solutions -\> Existing capabilities -\> Current limitations and constraints -\> Improvement opportunities -\> SSP requirements**

 The purpose is not to claim novelty for individual technologies. Technologies such as GNSS, BLE, cellular communication, geofencing, cloud computing and machine learning are already established. SSP instead investigates their integration and coordinated use within a common system.

---

 ## 3.2 Market and Application Context

 SSP operates at the intersection of electronic monitoring, personal protection, perimeter monitoring, connected wearables, IoT sensing, wireless communication, edge computing, cloud services and intelligent event processing.

 These domains are interconnected. A practical monitoring system must combine physical sensing with positioning, communications, event processing, alerting, operational visualization, security, privacy and lifecycle management.

 Operational electronic monitoring systems provide an important reference point because they demonstrate that combinations of wearable devices, GNSS, BLE, cellular communication, motion sensing, proximity detection, tamper monitoring and centralized monitoring can already be used in real operational contexts.

 This establishes the baseline:

 **Positioning + Motion + Proximity \+ Communication + Tamper detection + Alerting**

 SSP therefore does not claim that these individual capabilities are absent from existing systems.

---

 ## 3.3 Existing Operational Solutions

 Electronic monitoring systems provide one of the closest operational reference domains for SSP.

 The Spanish telematic monitoring system for judicially imposed proximity restrictions provides a representative example of an operational system combining wearable and control devices, BLE, GNSS, cellular communication, motion sensing, proximity detection, device-integrity mechanisms and centralized monitoring.

 Such systems also demonstrate the importance of contingency behavior when normal communication paths are disrupted may provide context about whether a device is moving, stationary or undergoing a particular movement positioning. GNSS may provide an estimate of geographical location, while BLE.

 A second relevant reference is the VioGén ecosystem, which demonstrates a broader institutional model in which information from multiple sources can support risk assessment, monitoring, protection activities and automated notification.

 These examples establish two important observations.

 First, the fundamental technologies required for connected monitoring are operationally feasible.

 Second, protection systems can extend beyond simple location tracking toward broader information integration and risk-management processes.

 SSP is not intended to replace institutional systems such as these. Its purpose is to investigate an IoT platform capable of supplying structured sensing, contextual information and event processing to authorized operational environments.

---

 ## 3.4 Existing Technology Capabilities

 ### 3.4.1 Positioning

 GNSS provides an established mechanism for outdoor positioning and is already used in electronic monitoring applications.

 However, positioning quality can vary according to environmental conditions, including buildings, urban environments, indoor operation and signal obstruction.

 Consequently, SSP should treat positioning as a measurement with an associated quality or confidence rather than as an infallible representation of physical location.

 The engineering implication is:

 **Position measurement -\> Position confidence -\> Contextual interpretation**

---

 ### 3.4.2 Motion and Inertial Sensing

 Accelerometers and gyroscopes are established components of wearable and mobile systems.

 Within SSP, motion information may provide context about whether a device is moving, stationary or undergoing a particular movement pattern. It may also help determine whether an apparent position transition is physically plausible.

 The resulting relationship is:

 **Position + Motion -\> Improved event interpretation**

---

 ### 3.4.3 BLE and Proximity

 BLE provides short-range communication and proximity information.

 Its functional role differs from geographical positioning. GNSS may provide an estimate of geographical location, while BLE or similar technologies can provide information about local relative presence.

 The conceptual distinction is:

 **GNSS -\> Geographical position**

 **BLE/proximity -\> Local relative presence**

 The combination may provide information that neither source provides independently.

---

 ### 3.4.4 Cellular Communication

 Cellular communication provides wide-area connectivity for mobile devices.

 Its suitability for SSP must be evaluated according to coverage, latency, energy consumption, availability, communication cost, device constraints and fallback requirements.

 The final technology selection is intentionally deferred to the communication design.

---

 ### 3.4.5 Edge Computing

 Edge processing provides the possibility of interpreting information closer to its source.

 Potential functions include local event filtering, sensor fusion, geofence evaluation, trajectory estimation, anomaly detection, communication prioritization and local fallback.

 The market context therefore supports investigation of distributed processing processing domain, but the market analysis indicates that centralized processing does not necessarily need to be without prescribing the final architecture.

---

 ### 3.4.6 Cloud Computing

 Cloud services provide centralized storage, fleet management, large-scale analytics, historical analysis, model management, dashboards and system-wide integration.

 The cloud is therefore an important SSP processing domain, but the market analysis indicates that centralized processing does not necessarily need to be used for every function.

 The intended principle is:

 **Local requirement -\> Local processing where justified**

 **System-wide requirement -\> Centralized processing where justified**

---

 ## 3.5 Existing Approaches to Geofencing and Protection Zones

 Geofencing is an established mechanism for translating geographical information into operational rules.

 Typical concepts include inclusion zones, exclusion zones, permitted areas, restricted areas, proximity thresholds and entry or exit conditions.

 However, a static boundary crossing does not necessarily contain sufficient context to determine the operational significance of an event.

 For example:

 **Boundary crossing + movement away from protected area**

 may represent a different situation from:

 **Boundary approach + increasing proximity + high-confidence position**

 Similarly:

 **Boundary approach + uncertain position**

 may require different interpretation from a high-confidence measurement.

 This provides a rationale for investigating contextual event interpretation.

---

 ## 3.6 Existing Limitations and Opportunities for Improvement

 The existence of an established technology does not imply that all possible system-level integrations or operating strategies have been exhausted.

 The analysis identifies opportunities for improvement using distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation.

 These opportunities are considered engineering hypotheses rather than demonstrated advantages.

 ### 3.6.1 Distributed Processing

 A conventional monitoring process can be represented as:

 **Sense -\> Transmit -\> Central processing -\> Alert**

 SSP investigates:

 **Sense -\> Local interpretation -\> Edge assessment -\> Cloud analysis -\> Operational response**

 The purpose is to determine whether distributing selected functions provides measurable benefits.

 ### 3.6.2 Adaptive Monitoring

 Continuous maximum-intensity sensing and communication may consume resources unnecessarily during low-significance states.

 SSP therefore investigates resulting energy benefit:

 **Operational context -\> Monitoring intensity -\> Processing intensity -\> Communication intensity**

 ### 3.6.3 Energy-Aware Operation

 Energy consumption is affected by sensing, processing and communication.

 The intended objective is:

 **Operational significance -\> Resource allocation -\> Energy consumption**

 The resulting energy benefit must subsequently be measured rather than assumed.

 ### 3.6.4 Privacy-Aware Information Flow

 Location and movement information may be sensitive. SSP therefore investigates whether processing information locally can reduce unnecessary transmission.

 The intended principle is:

 **Raw information -\> Local processing -\> Necessary information -\> Controlled transmission**

 ### 3.6.5 Contextual Event Interpretation

 SSP investigates whether position, motion, proximity, device state categories without constit, communication state and historical context can be considered together.

 The intended relationship is:

 **Multiple observations -\> Context -\> Event interpretation -\> Severity assessment**

 ### 3.6.6 Resilient Operation

 Connectivity disruption is treated as an engineering condition that must be handled explicitly.

 The intended relationship is:

 **Communication failure -\> Local/edge continuity -\> Event preservation -\> Recovery -\> Synchronization**

---

 ## 3.7 Technology Alternatives Relevant to SSP

 The following table identifies technology categories without constituting a final selection.

 | Function | Candidate approaches | Principal engineering considerations |
| --- | --- | --- |
| Outdoor positioning | GNSS and assisted GNSS | Accuracy, availability and energy |
| Local proximity | BLE and other short-range technologies | Range, energy and environmental conditions |
| Motion sensing | Accelerometer, gyroscope and sensor fusion | Information quality, computation and energy |
| Local connectivity | BLE and Wi-Fi | Range, infrastructure and energy |
| Wide-area connectivity | Cellular and LPWAN alternatives | Coverage, bandwidth, latency, energy and cost |
| Local processing | MCU and embedded processors | Computational capability and energy |
| Edge processing | Mobile device, gateway or local server | Deployment complexity and connectivity |
| Cloud processing | Public or private cloud infrastructure | Scalability, cost and connectivity dependency |
| Event detection | Rule-based, statistical and machine-learning methods | Interpretability, adaptability and data requirements |
| Position/risk interpretation | Static geofencing and contextual/predictive analysis | Complexity and contextual capability |

The final technology selections are therefore intentionally deferred until the requirements have been established and the architecture is developed.

---

 ## 3.8 Security, Privacy and Regulatory Context

 SSP may process location, movement, proximity and operational information that can be sensitive.

 Security therefore needs to extend from the device through communications and processing services to authorized user access.

 Relevant security capabilities include device identity, protected configuration, authenticated communication, credential protection, secure software updates, access control, auditability and lifecycle management.

 Privacy similarly affects the complete information lifecycle.

 The relevant relationship is:

 **Collection -\> Processing -\> Transmission -\> Storage -\> Access -\> Retention -\> Deletion**

 Each stage may affect privacy risk.

 NIST IoT cybersecurity guidance, the NIST Privacy Framework and relevant ETSI IoT cybersecurity guidance provide useful engineering references for establishing such controls. However, the precise legal and regulatory requirements of a real SSP deployment would depend on jurisdiction, application and organizational responsibilities.

 A technically functional SSP system should therefore not automatically be interpreted as legally deployable.

---

 ## 3.9 Benchmarking Framework

 The relevant comparison between SSP and existing solutions should focus on documented capabilities and architectural approaches rather than on unsupported claimsofencing, motion interpretation, event detection, contextual assessment, local processing, centralized processing, communication resilience, energy management, privacy, security, alerting, scalability, fleet management, AI or of superiority.

 Relevant dimensions include sensing, positioning, proximity, geofencing, motion interpretation, event detection, contextual assessment, local processing, centralized processing, communication resilience, energy management, privacy, security, alerting, scalability, fleet management, AI or analytics, interoperability and operational usability.

 The analysis must distinguish:

 **Documented existing capability**

 from

 **Proposed SSP capability**

 The absence of publicly available documentation about a capability must not be interpreted as proof that an existing system lacks that capability.

---

 ## 3.10 SSP Improvement Objectives Derived from the Analysis

 The market and technology analysis supports seven principal SSP. The Edge/Mobile domain should be capable of performing more than protocol forwarding. It should investigate validation, filtering, aggregation, local feature extraction, selected event processing, low-latency inference and temporary continuation, system-wide analytics, fleet management, controlled user access, model management, retention management improvement objectives.

 The first is Device-layer improvement. The device should not be limited to collecting and transmitting raw information. It should investigate local preprocessing, adaptive sensing, selected event detection, local buffering, device-state monitoring and energy-aware operation.

 The second is Edge-layer improvement. The Edge/Mobile domain should be capable of performing more than protocol forwarding. It should investigate validation, filtering, aggregation, local feature extraction, selected event processing, low-latency inference and temporary continuation of selected monitoring functions.

 The third is Cloud-layer improvement. The cloud domain should support centralized historical information, scalable ingestion, system-wide analytics, fleet management, controlled user access, model management, retention management and authorized integration interfaces.

 The fourth is privacy-aware information flow. The system should minimize unnecessary collection and transmission of sensitive information and should investigate processing information as close to the source as technically and operationally is energy-efficient operation. SSP should investigate adaptive sensing, local processing, low-power operating states and event-driven communication as mechanisms for reducing unnecessary the corresponding functionality exists. They must appropriate.

 The fifth is distributed AI capability. AI functions should be allocated according to latency, energy, computational capability, connectivity, privacy and model complexity. Device-level inference, Edge-level inference and Cloud-level analytics are therefore considered possible processing domains.

 The sixth is energy-efficient operation. SSP should investigate adaptive sensing, local processing, low-power operating states and event-driven communication as mechanisms for reducing unnecessary energy consumption.

 The seventh is measurable engineering validation. None of these objectives should be treated as demonstrated simply because the corresponding functionality exists. They must be translated into requirements and validated quantitatively.

---

 ## 3.11 Design Implications

 The analysis leads to several engineering implications.

 Multi architecture because the location of processing determines what information must technical information about commercial and institutional monitoring systems is incomplete. A capability that is not publicly documented cannot-source sensing should be considered because position, motion and proximity can provide complementary information.

 Position uncertainty should influence event interpretation because uncertain measurements should not automatically be treated identically to high-confidence measurements.

 Processing should not automatically be centralized because some functions may benefit from local execution.

 Communication should be policy-aware because information can have different operational significance.

 Connectivity loss must be explicitly handled because communication disruption is a realistic operating condition.

 Energy management should be integrated with system logic because resource consumption depends on sensing, processing and communication behavior.

 Privacy should influence architecture because the location of processing determines what information must cross system boundaries.

 Security must extend to the device because device compromise can affect the integrity of the complete monitoring system.

 AI requires measurable justification because a machine-learning component is not inherently beneficial merely because it is technically possible.

 Scalability should be considered from the beginning because device registration, event ingestion, storage and processing requirements can increase significantly with deployment size.

---

 ## 3.12 Relationship Between Market Analysis and Requirements

 The market analysis supports the requirements that will be formalized in Chapter 4.

 Existing use of GNSS and geofencing supports positioning and geographical monitoring requirements.

 Existing use of BLE and proximity detection supports proximity-monitoring requirements.

 Existing contingency mechanisms support communication-loss and local-fallback requirements.

 Existing centralized protection systems support cloud integration and system-wide analysis requirements.

 Environmental variation in positioning supports position-confidence requirements.

 Wearable energy constraints support adaptive energy-management requirements.

 The sensitivity of location information supports data-minimization and privacy-aware processing requirements.

 IoT cybersecurity guidance supports device identity, authentication, secure updates and lifecycle-management requirements.

 The increasing importance of system integration supports interoperability and structured interface requirements.

 The use of analytics and predictive processing supports evaluation of AI where measurable benefit can be established.

 The result is:

 **Operational scenarios + Existing landscape + Improvement objectives -\> Formal SSP requirements**

---

 ## 3.13 Limitations of the Market Analysis

 Public technical information about commercial and institutional monitoring systems is incomplete. A capability that is not publicly documented cannot therefore be assumed to be absent.

 Operational systems may also be subject to legal, institutional and security restrictions that limit public disclosure.

 The present analysis is a technical and contextual study rather than a complete, tamper monitoring and centralized alerting. Broader protection platforms demonstrate the value of integrating commercial market-validation exercise. Supplier pricing, procurement conditions, certification requirements and contractual service conditions require separate analysis.

 Technologies and standards also evolve over time. Technical selections must therefore be validated against current documentation during detailed engineering.

 Finally, the opportunities identified in this chapter are not guaranteed performance improvements. Any claimed SSP improvement must be demonstrated through quantitative requirements and subsequent validation.

---

 ## 3.14 Chapter 3 Conclusion

 The market and technology landscape demonstrates that the principal building blocks required for SSP already exist.

 Existing operational systems demonstrate the feasibility of combining positioning, proximity, motion sensing, communication, tamper monitoring and centralized alerting. Broader protection platforms demonstrate the value of integrating information, risk assessment, monitoring and notification.

 The analysis identifies opportunities for improvement using distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation.

 These opportunities are treated as engineering objectives rather than as unsupported claims of superiority.

 The next step is therefore to translate the operational scenarios and the identified improvement objectives into formal and measurable SSP requirements.

 This is the purpose of Chapter 4.

---

 # Chapter 4. SSP System Requirements and Engineering Specifications

 ## 4.1 Purpose and Requirements Methodology

 This chapter defines what the SSP system must achieve and establishes the measurable criteria against which the architecture and implementation will subsequently be designed and validated.

 The requirements are derived from the problem definition in Chapter 1, the operational scenarios in Chapter 2 and the market, technology and context analysis in Chapter 3.

 The resulting engineering progression is:

 **Problem -\> Operational scenario -\> Existing context -\> Improvement objective -\> Requirement -\> Architecture -\> Implementation -\> Validation**

 The requirements are intentionally defined independently of specific hardware, communication technologies, cloud platforms and machine-learning models.

 This prevents premature implementation decisions from constraining the system requirements.

 The requirements are organized into system-level, functional, performance, positioning and sensing, communication, intelligence and AI, energy, security, privacy, reliability, usability, physical, scalability, maintainability and economic categories.

 Each significant requirement shall ultimately be associated with a verification method and, where applicable, an acceptance criterion.

 The fundamental-end IoT monitoring platform capable of monitoring defined geographical, proximity or perimeter conditions, detecting relevant events, these domains shall be determined, contextual assessment, risk or severity assessment, communication, alert generation, device and system monitoring, data storage, operational visualization, configuration, relationship is:

 **Stakeholder need -\> Requirement -\> Design decision -\> KPI -\> Test -\> Result**

 Chapter 4 therefore defines what SSP must achieve. Chapter 5 and subsequent chapters will define how those requirements are achieved.

---

 ## 4.2 SSP System-Level Requirements

 SSP shall provide an end-to-end IoT monitoring platform capable of monitoring defined geographical, proximity or perimeter conditions, detecting relevant events, assessing their significance and delivering appropriate information to authorized users or operational systems.

 SSP shall support the conceptual processing domains:

 **Device -\> Edge/Mobile -\> Cloud**

 The detailed allocation of functions among these domains shall be determined during architecture development.

 SSP shall provide mechanisms for sensing, positioning, motion analysis, event detection, contextual assessment, risk or severity assessment, communication, alert generation, device and system monitoring, data storage, operational visualization, configuration, security, privacy-aware information management, fault detection and recovery.

 Security and privacy shall be treated as system properties rather than isolated application-layer functions.

 The system shall support configurable monitoring policies so that the same platform can be adapted to different authorized operational scenarios.

---

 ## 4.3 Functional Requirements

 ### 4.3.1 Device Functions

 Each deployed SSP device shall have a unique identity allowing it to be associated with an authorized configuration and deployment context.

 The system shall acquire positioning information using one or more appropriate positioning mechanisms.

 Positioning information shall, where technically feasible, include an indication of quality or confidence.

 The system shall acquire and process relevant movement information.

 The device shall support local preprocessing where such processing provides a measurable benefit in latency, energy consumption, privacy, resilience or communication efficiency.

 The device shall support selected local event detection where cloud-only processing would not satisfy the applicable operational requirements.

 The device shall monitor relevant device-state information, including battery and defined abnormal conditions.

 The device shall support local buffering of relevant events during temporary communication disruption, subject to available storage and policy constraints.

 The device shall support adaptive sensing and processing behavior according to operational state and configured policy.

---

 ### 4.3.2 Geographical and Proximity Functions

 SSP shall support configurable geographical rules, including inclusion and exclusion zones.

 The system shall determine whether observed or predicted movement satisfies configured geographical conditions.

 Where required by the application, SSP shall support proximity monitoring between authorized devices or between a monitored device and a protected-person device.

 The system shall be capable of combining geographical and proximity information where such combination improves event interpretation.

---

 ### 4.3.3 Event and Risk Functions

 SSP shall convert relevant sensing, positioning, communication, device-state and system conditions into structured events.

 Events shall contain sufficient contextual information for subsequent processing and operational interpretation.

 The system shall support risk or severity assessment using relevant information such as position, position confidence, motion, proximity, historical information, geographical rules, device state, communication state and event history.

 The system shall generate alerts when configured conditions are satisfied.

 Alerts shall include appropriate severity or priority information where required.

---

 ### 4.3.4 Adaptive Monitoring

 SSP shall support adaptive changes in sensing, processing and communication between the Device and Edge/Mobile, Edge/Mobile and Cloud, and Cloud and authorized communication failures and execute defined fallback behavior behavior according to operational context, configured policy and system state.

 The intended relationship is:

 **Context -\> Risk/significance -\> Monitoring intensity -\> Processing intensity -\> Communication intensity**

 The purpose is to reduce unnecessary resource consumption while maintaining required protection functions.

---

 ### 4.3.5 Edge Functions

 Where an Edge/Mobile processing domain is deployed, it shall support functions that benefit from local or near-local processing.

 Such functions may include validation, filtering, aggregation, feature extraction, event interpretation, predictive processing, risk assessment, communication prioritization and local fallback.

 The final function allocation shall be determined during architecture design.

---

 ### 4.3.6 Cloud Functions

 The cloud environment shall support functions benefiting from centralized information and computation.

 These functions may include historical analysis, fleet management, policy management, long-term storage, system-wide analytics, model management, operational reporting and integration with authorized external systems.

---

 ### 4.3.7 Operational Visualization

 Authorized users shall have interfaces appropriate to their roles for viewing relevant system information, device status, events, alerts and operational context.

 The interfaces shall support the operator workflow established in Chapter 2.

---

 ### 4.3.8 Configuration Management

 Authorized users shall be able to configure applicable monitoring policies, geographical zones, thresholds, notification rules, device configurations and permissions without modification of the underlying application architecture.

---

 ### 4.3.9 Device Management

 The system shall support device registration, provisioning, configuration, status monitoring, diagnostics and lifecycle management.

---

 ### 4.3.10 Event History

 Relevant events shall be stored according to the applicable retention policy so that authorized users can review historical activity.

---

 ### 4.3.11 Communication-Loss Operation

 The system shall define behavior for temporary communication loss between the Device and Edge/Mobile, Device and Cloud, and Edge/Mobile and Cloud.

 Where required by the operational scenario, selected monitoring and decision functions shall continue locally during temporary disruption.

 Important events generated during communication disruption shall be retained until secure forwarding becomes possible, subject to policy and storage constraints.

---

 ## 4.4 Performance Requirements

 Performance requirements shall ultimately be expressed in measurable form:

 **Function X -\> Operating conditions C -\> Maximum/minimum measurable value**

 Examples include alert latency, positioning accuracy, detection performance, local inference latency, communication latency, cloud response time, system availability and recovery time.

 At the current D2 stage, numerical targets that depend on subsequent hardware, communication or deployment decisions shall remain explicitly identified as provisional.

 | Parameter | Initial requirement | Final definition |
| --- | --- | --- |
| Critical-event alert latency | ≤ TBD | Architecture and validation |
| Positioning accuracy | ≤ TBD error | Positioning design and validation |
| Event-detection performance | ≥ TBD | Intelligence design and validation |
| Local inference latency | ≤ TBD | Hardware/software validation |
| Communication latency | ≤ TBD | Communication design |
| Cloud response time | ≤ TBD | Cloud design |
| System availability | ≥ TBD | Deployment and resilience analysis |
| Communication recovery time | ≤ TBD | Communication and resilience validation |

The final values shall be established before formal validation and shall be traceable to the relevant operational scenario.

---

 ## 4.5 Positioning, Sensing and Event-Detection Requirements

 The positioning subsystem shall provide accuracy appropriate to the intended monitoring scenario.

 The system shall identify conditions under which the primary positioning source becomes unreliable or unavailable.

 Where justified, multiple positioning or contextual information sources shall be capable of being combined.

 Potential information sources include GNSS, inertial sensing, Wi-Fi information, cellular information and BLE/proximity information.

 Motion information shall support identification of relevant device states and event interpretation.

 The system shall identify abnormal, inconsistent or unavailable sensor behavior where technically feasible.

 Position confidence shall be capable of influencing downstream decision functions.

 Where multiple sensing sources are used, SSP shall provide a defined mechanism for combining or correlating the information.

 The resulting relationship is:

 **Sensor information -\> Quality assessment -\> Fusion -\> Context -\> Event interpretation**

---

 ## 4.6 Communication Requirements

 The architecture shall define communication mechanisms between the Device and Edge/Mobile, Edge/Mobile and Cloud, and Cloud and authorized users.

 Communication technologies shall ultimately be selected according to range, bandwidth, latency, energy consumption, infrastructure availability, reliability, security, cost and deployment environment.

 Information shall be prioritized according to operational significance.

 Routine status information may use normal transmission behavior, whereas elevated and critical events shall receive appropriately higher communication priority.

 The system shall detect relevant communication failures and execute defined fallback behavior.

 Communication shall avoid transmitting information unnecessary for the receiving layer to perform its required function.

 Communications carrying SSP information shall provide appropriate authentication, confidentiality, integrity and replay protection where required.

 Communication status shall where its measurable benefit justifies its complexity domains where technically may support lightweight functions such as motion classification, sensor interpretation,ability shall be evaluated in terms of device registration, communication load, event ingestion, database capacity, storage, processing, dashboard performance, AI-monitoring use case establishes the need to manage information transmission efficiently. The market analysis identifies energy and privacy constraints. The improvement objectives introduce adaptive monitoring and privacy-aware information flow. Chapter 4 consequently establishes requirements for adaptive sensing, local processing and selective communication. Chapter 5 will determine the architecture required performance shall be evaluated through positioning accuracy, positioning availability, position confidence, event-detection performance,-resilience requirement shall define the disruption condition, required local functionality, maximum information-loss tolerance and recovery behavior Their actual effectiveness cannot be established by D2 alone; it must be monitored sufficiently to identify relevant degradation, interruption and recovery.

---

 ## 4.7 Intelligence and AI Requirements

 AI shall be treated as a system capability rather than as an objective in itself.

 Any AI function included in SSP shall have a defined operational purpose and measurable performance objective.

 AI shall only be introduced where its measurable benefit justifies its complexity relative to an appropriate deterministic or statistical alternative.

 The system shall support distributed intelligence across Device, Edge/Mobile and Cloud processing domains where technically justified.

 Device-level intelligence may support lightweight functions such as motion classification, sensor interpretation, event preprocessing and anomaly detection.

 Edge-level intelligence may support predictive geofencing, trajectory prediction, risk assessment, sensor fusion and anomaly detection.

 Cloud-level intelligence may support historical analytics, fleet analytics, model training, model evaluation, model management and policy optimization.

 The allocation of AI functions shall consider:

 **Latency + Energy + Computation \+ Connectivity + Privacy \+ Model complexity**

 Where machine-learning models are deployed, SSP shall support controlled model versioning, evaluation, deployment, rollback and monitoring.

 Where a model produces confidence or uncertainty information, the system shall use that information where appropriate so that low-confidence predictions are not automatically treated identically to high-confidence decisions.

 The system shall define fallback behavior when an AI model is unavailable, produces insufficient confidence, fails to execute or produces an output outside an acceptable operational range.

 AI shall not constitute an uncontrolled single point of failure for critical system functions.

---

 ## 4.8 Energy Requirements

 Energy efficiency shall be treated as a system-level requirement rather than solely as a battery characteristic.

 The device shall support adaptive management of sensing, processing and communication resources according to operational state.

 The device shall support low-power operating states when high-intensity monitoring is not required.

 Sensors and communication components shall support appropriate duty-cycling strategies where technically feasible.

 The communication strategy shall consider the energy cost of transmitting information.

 The device shall provide battery autonomy appropriate to its intended application and operating profile.

 Battery state shall be monitored and warnings shall be provided when available energy approaches defined operational thresholds.

 The engineering relationship shall be:

 **Operational significance -\> Monitoring intensity -\> Processing intensity -\> Communication intensity -\> Energy consumption**

 Energy-saving mechanisms shall not compromise critical protection functions beyond the limits established by the applicable requirements.

 The energy-performance framework shall ultimately include sleep power, normal-monitoring power, active-monitoring power, communication power, processing energy, sensing duty cycle, energy per event, daily energy consumption and battery autonomy.

---

 ## 4.9 Security Requirements

 SSP shall implement security as an end-to-end system property.

 Only authorized devices shall participate in the SSP system.

 Users shall be authenticated before accessing protected functions or sensitive information.

 Access to information and functions shall be controlled according to roles and operational responsibilities.

 Communication shall provide appropriate confidentiality, integrity and authentication.

 The architecture shall provide mechanisms for detecting unauthorized modification of device software or configuration where technically feasible.

 Firmware and software updates shall use authenticated and integrity-protected mechanisms.

 Sensitive credentials and cryptographic keys shall be protected against unauthorized extraction or use.

 Security-sensitive operations shall generate appropriate audit records.

 The system shall detect defined physical or logical tampering conditions.

 Security failures shall result in defined system behavior rather than being silently ignored.

 Security shall therefore extend across:

 **Device identity -\> Device integrity -\> Communication security -\> Application access -\> Cloud services -\> Lifecycle management**

---

 ## 4.10 Privacy Requirements

 SSP may process sensitive location, movement, proximity and operational information.

 The system shall therefore collect and transmit only information required for the authorized operational function.

 Where local processing can satisfy an operational requirement without unnecessary transmission of sensitive information, processing should be performed as close to the data source as technically and operationally appropriate.

 Sensitive information shall only be accessible to authorized users and system components.

 Stored and transmitted sensitive information shall be protected using appropriate security mechanisms.

 The system shall support defined retention and deletion policies appropriate to the application and applicable regulatory requirements.

 The system shall support policies that determine the level of information transmitted under different operational conditions.

 The intended relationship is:

 **Normal state -\> Minimum necessary information**

 **Elevated state -\> Additional contextual information**

 **Critical state -\> Information necessary for authorized response**

 Significant access to sensitive information and relevant privacy operations should be auditable.

 The privacy objective is therefore not simply encryption. It is:

 **Minimize collection -\> Minimize transmission -\> Control access -\> Control retention -\> Audit use**

---

 ## 4.11 Reliability, Resilience and Availability Requirements

 SSP shall maintain appropriate operational functionality despite individual subsystem failures and temporary communication disruption.

 The system shall detect relevant hardware, software, sensor and communication failures.

 When a subsystem becomes unavailable, SSP shall retain the maximum appropriate level of functionality rather than failing completely.

 Selected monitoring and decision functions shall continue during temporary loss of cloud connectivity where required by the operational scenario.

 Important events generated during communication disruption shall be preserved locally or at the Edge until secure forwarding is possible.

 The system shall achieve an availability level appropriate to the intended application.

 Defined recovery procedures shall exist for device failure, communication failure, software failure, Edge failure and cloud-service failure.

 Where operationally required, sufficient state information shall be preserved to restore normal monitoring following temporary disruption.

 The resilience relationship is:

 **Failure -\> Detection -\> Degraded operation -\> Local/Edge continuity -\> Recovery -\> Synchronization -\> Normal operation**

---

 ## 4.12 Usability and Operational Requirements

 Alerts shall communicate event type, severity and relevant contextual information required by the authorized operator.

 The system shall distinguish events according to operational importance.

 The system should reduce unnecessary repetitive alerts, duplicate notifications and low-value information.

 Users shall be presented with functions and information appropriate to their authorized role.

 Authorized administrators shall be able to configure monitoring policies without modifying the underlying application architecture.

 Authorized operators shall be able to determine the relevant status and history associated with an alert or significant event.

 These requirements directly derive from the operator workflow established in Chapter 2.

---

 ## 4.13 Physical and Environmental Requirements

 Physical requirements shall depend on the SSP deployment configuration.

 For wearable applications, the design shall consider size, weight, environmental protection, operating temperature, mechanical robustness, water and dust exposure, charging requirements, attachment security, tamper resistance and user comfort.

 For fixed or infrastructure-based applications, requirements may instead emphasize enclosure protection, mounting, external power, environmental conditions, network availability, physical security and maintenance accessibility.

 The detailed physical specification shall therefore be established separately for each device configuration.

 Representative deployment scenarios shall include, where appropriate:

 **10 devices -\> 100 devices -\> 500 devices**

 These values represent evaluation scenarios and do not constitute a claim of already demonstrated operational capacity.

---

 ## 4.14 Scalability Requirements

 SSP shall be designed so that increasing the number of monitored devices does not require a fundamental redesign of the system.

 The system shall support progressive scaling from:

 **Prototype -\> Small deployment -\> Pilot -\> Operational fleet**

 Scalability shall be evaluated in terms of device registration, communication load, event ingestion, database capacity, storage, processing, dashboard performance, AI processing, model management and operational management.

 Where appropriate, local or Edge processing should reduce unnecessary growth in centralized communication and processing requirements.

 The scalability relationship is:

 **Device count -\> Information volume -\> Event rate -\> Processing load -\> Storage -\> Operational workload**

 The architecture shall be designed to manage this progression without requiring fundamental restructuring.

---

 ## 4.15 Maintainability and Lifecycle Requirements

 SSP shall support lifecycle management of hardware and software.

 Depending on deployment configuration, the system shall support provisioning, configuration management, firmware updates, software updates, model updates, health monitoring, diagnostics, fault reporting, replacement procedures, version management and lifecycle-status tracking.

 The architecture should permit individual components to evolve without requiring complete system redesign.

 Lifecycle management shall therefore be treated as an engineering property from the beginning rather than as a post-deployment function.

---

 ## 4.16 Economic Requirements

 The SSP solution shall be evaluated technically and economically.

 The design shall provide sufficient information to estimate device bill of materials, manufacturing cost, development cost, Edge infrastructure cost, cloud cost, communication cost, maintenance cost, deployment cost and total cost of ownership.

 The economic analysis shall consider how deployment scale affects both capital and operational expenditure.

 Economic requirements shall be quantified progressively as hardware, communication, software, cloud and deployment architectures are defined.

---

 ## 4.17 Requirements Prioritization

 Requirements shall be classified according to their operational significance.

 | Priority | Meaning |
| --- | --- |
| Mandatory | Required for the fundamental SSP function |
| High | Important for operational deployment and system quality |
| Medium | Important for optimization, scalability or user experience |
| Future | Desirable capability that may be introduced later |

The initial classification places positioning, event detection, alert generation, secure communication and device authentication among the mandatory capabilities.

 Adaptive energy management, local or Edge decision capability, privacy-aware communication and predictive processing are initially considered high-priority capabilities.

 Fleet analytics and advanced AI optimization are considered important capabilities whose final priority depends on the deployment scenario and engineering evidence.

 Priorities may be refined as the architecture and validation constraints become clearer.

---

 ## 4.18 Requirements Traceability

 The requirements shall remain traceable throughout the complete design process.

 The intended traceability chain is:

 **Use case -\> Context finding -\> Improvement objective -\> Requirement -\> Architecture element -\> Component -\> Implementation -\> KPI -\> Test -\> Result**

 This provides a stronger basis for engineering justification than a requirement list without context.

 For example, the normal-monitoring use case establishes the need to manage information transmission efficiently. The market analysis identifies energy and privacy constraints. The improvement objectives introduce adaptive monitoring and privacy-aware information flow. Chapter 4 consequently establishes requirements for adaptive sensing, local processing and selective communication. Chapter 5 will determine the architecture required to satisfy those requirements.

 Similarly:

 **Connectivity-loss scenario -\> Resilience opportunity -\> Local fallback objective -\> Offline-operation requirement -\> Architecture -\> Implementation -\> Recovery test**

 And:

 **Approach scenario -\> Contextual interpretation opportunity -\> Predictive-processing objective -\> Prediction requirement -\> Architecture -\> AI implementation -\> Prediction validation**

 This traceability shall be expanded as the project develops.

---

 ## 4.19 Preliminary SSP KPI Framework

 The requirements establish the KPI categories that will be used throughout the project.

 Technical performance shall be evaluated through positioning accuracy, positioning availability, position confidence, event-detection performance, prediction performance, local-processing latency and end-to-end alert latency.

 Energy performance shall be evaluated through energy consumption by operating mode, energy per event, daily energy consumption, battery autonomy, communication energy and processing energy.

 Communication performance shall be evaluated through latency, throughput, packet reliability, communication availability, recovery time and transmitted data volume.

 Security performance shall be evaluated through authentication behavior, unauthorized-access prevention, security-event detection, update-integrity verification and security-response time.

 Privacy performance shall be evaluated through sensitive-data transmission volume, local-processing ratio, retention compliance, access-control events and data-minimization ratio.

 Reliability shall be evaluated through system availability, communication-failure recovery time, local fallback duration, event preservation and fault-detection time.

 Scalability shall be evaluated through supported device count, event-ingestion rate, storage growth, centralized-processing latency and dashboard response time.

 Economic performance shall be evaluated through device bill of materials, cost per deployed device, communication cost, cloud cost, annual operating cost and total cost of ownership.

 The relationship is:

 **Requirement -\> KPI -\> Measurement method -\> Acceptance threshold -\> Validation result**

---

 ## 4.20 Requirements Acceptance and Verification Principle

 A requirement shall not be considered satisfied merely because the corresponding function exists in a prototype or proof of concept.

 For each critical requirement, SSP shall ultimately establish:

 **What must be achieved? -\> Under what conditions? -\> How will it be measured? -\> What constitutes acceptance?**

 The final validation structure shall therefore be:

 **Requirement -\> Test condition -\> Measurement -\> Acceptance threshold -\> Result -\> Status**

 For example, an alert-latency requirement shall define the triggering condition, measurement points, operating environment, network conditions and maximum acceptable latency.

 Similarly, battery autonomy shall be measured under a defined operating profile rather than reported as an isolated nominal battery value.

 An AI requirement shall define the evaluation dataset or operating conditions, performance metric, confidence conditions and acceptance threshold.

 A communication-resilience requirement shall define the disruption condition, required local functionality, maximum information-loss tolerance and recovery behavior.

 A privacy requirement shall define the information flow being measured and the criterion used to establish compliance.

 This approach ensures that SSP is evaluated objectively rather than demonstrated only qualitatively.

---

 ## 4.21 Chapter 4 Conclusion

 The requirements defined in this chapter establish the engineering baseline for SSP.

 The requirements originate from the problem definition, operational scenarios and existing technology context established in Chapters 1–3.

 SSP is required to provide more than basic positioning and alert generation. The system must support:

 **Reliable sensing -\> Positioning -\> Contextual interpretation -\> Risk/severity assessment -\> Adaptive communication -\> Secure operation -\> Privacy-aware processing -\> Resilient monitoring -\> Operational response**

 The system must also investigate whether these functions can be distributed according to their operational requirements:

 **Device -\> Edge/Mobile -\> Cloud**

 The requirements further establish that energy, privacy, security, resilience, scalability and maintainability are system-level concerns rather than independent additions.

 The intended improvements identified in Chapter 3 are therefore converted into measurable engineering objectives in Chapter 4. Their actual effectiveness cannot be established by D2 alone; it must be determined through subsequent design, implementation and validation.

 The resulting project progression is:

 **Problem -\> Users and scenarios -\> Existing solutions -\> Improvement opportunities -\> Requirements -\> Architecture -\> Hardware -\> Communication -\> Software -\> Data -\> AI -\> Energy and performance -\> Cloud -\> PoC -\> Cost -\> Validation**

 Chapter 5 will therefore begin the detailed engineering design by translating the requirements established in this document into the SSP system architecture.

 This version is now internally consistent with the decisions we made: **Chapter 3 explains what exists and where improvement opportunities arise; Chapter 4 converts those findings into requirements; Chapter 5 is the first place where the actual architecture is designed.**
