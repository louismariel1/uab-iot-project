 ## SSP — D2 Presentation Narrative Script

 ### Opening

 Good morning.

 Our project is called **SSP, Smart Safety and Protection**, and it is an IoT system designed to support safety monitoring through the combination of positioning, movement information, proximity information, device status, local processing, edge processing and cloud services.

 In this presentation, I will explain the first four chapters of our D2 document.

 The purpose of D2 is not to present the final architecture or the implemented system. Instead, D2 establishes what SSP is intended to do and how well it is expected to perform.

 The logical progression of our work is therefore:

 **Problem and motivation → users and operational scenarios → existing solutions and opportunities for improvement → functional and performance requirements.**

 The architecture that will implement these requirements belongs to the next delivery, D3.

---

 # Chapter 1 — SSP Motivation and Scope

 Let me start with the motivation behind SSP.

 Many safety and protection applications need to know where a person or protected asset is, how it is moving, whether it is approaching a relevant location, and whether the monitoring device itself is operating correctly.

 A conventional tracking system can collect location information and transmit it to an application. However, a safety-oriented IoT system may need to do more.

 For example, the system may need to distinguish between normal movement and an abnormal event. It may need to increase monitoring when a potentially dangerous situation develops. It may need to continue detecting important events when connectivity is temporarily unavailable. It may also need to reduce unnecessary communication and energy consumption.

 This leads to the central idea of SSP.

 SSP is conceived as a **distributed IoT safety and protection system** in which information can be sensed, processed and interpreted at different levels.

 At the device level, sensor information can be acquired and locally processed.

 At the edge level, information can be validated, aggregated and interpreted with lower latency and with less dependence on cloud connectivity.

 At the cloud level, historical information, fleet management, analytics, access control and other centralized functions can be provided.

 Finally, authorized users can interact with the system through a user interface.

 An important point is that D2 does not claim that these improvements have already been achieved.

 They are **engineering objectives translated into requirements**.

 The subsequent project deliveries will determine whether the implemented system actually meets these requirements.

 The main intended improvements concern distributed processing, adaptive monitoring, energy-aware operation, privacy-aware information flow, contextual event interpretation and resilient operation.

 The system is therefore intended to move beyond the idea of simply collecting and transmitting raw sensor data.

 For example:

 **Sensing → local processing → relevant information → event interpretation → operational response.**

 Another important principle is that SSP should not necessarily transmit all available raw information continuously.

 If a required function can be achieved using locally processed or aggregated information, the system should prefer the lower-data approach when this provides benefits in energy consumption, communication efficiency or privacy.

 This principle will become important when we define the functional and performance requirements.

---

 # Chapter 2 — Target Users, Use Cases and Operational Scenarios

 The second chapter explains SSP from the perspective of how it will actually be used.

 We begin by identifying the principal actors.

 The **protected person** is the person whose protection perimeter or safety status is being monitored.

 The **monitored person** is the person or device whose location or movement is subject to an authorized monitoring rule.

 The **protection operator** monitors the system, reviews alerts and performs the corresponding operational actions.

 The **system administrator** manages users, devices, policies and configuration.

 The **authorized organization** is the institution responsible for deploying and operating SSP.

 Finally, the **technical or service operator** maintains the devices, connectivity, cloud services and supporting infrastructure.

 However, simply listing these users is not sufficient to understand the system.

 For that reason, D2 describes SSP through operational use cases.

---

 ## Normal Monitoring

 The first scenario is normal monitoring.

 The process can be summarized as:

 **Device activated → sensing → local processing → relevant information transmitted → status updated → authorized operator monitors the system.**

 The important point is that normal monitoring does not necessarily mean continuous transmission of every raw sensor measurement.

 The device can adapt its sensing and communication behavior according to the current monitoring context.

 This establishes the concept of **adaptive monitoring**.

---

 ## Approach to a Protected Perimeter

 The second scenario considers a monitored person approaching a protected perimeter.

 The process is:

 **Movement detected → position and motion evaluated → trajectory or proximity assessed → approach detected → risk level increases → monitoring policy adapts → predictive assessment → warning or alert → operational response.**

 This scenario illustrates why SSP is intended to be more than a conventional location tracker.

 The system is intended to support a progression from:

 **normal monitoring → increased monitoring → prediction → alert → response.**

 This progression later becomes important when defining requirements for event detection, latency, adaptive sensing and risk assessment.

---

 ## High-Risk or Critical Event

 The third scenario considers a high-risk condition.

 The sequence is:

 **Abnormal movement or perimeter violation → device detection → local assessment → high-risk condition → priority communication → edge evaluation → critical event confirmation → immediate alert → operational response.**

 This scenario establishes the need for different event priorities and for low-latency processing.

 It also shows why some functions should be available locally or at the edge rather than depending entirely on the cloud.

---

 ## Temporary Connectivity Loss

 The fourth scenario addresses resilience.

 Suppose the system temporarily loses connectivity.

 The intended behavior is:

 **Normal monitoring → connectivity disruption → communication problem detected → local monitoring continues → relevant events are buffered → connectivity restored → buffered information synchronized → normal operation resumes.**

 The important requirement is that loss of cloud connectivity should not automatically mean loss of protection functionality.

 Selected local and edge functions should continue operating during temporary communication failures.

---

 ## Device Tampering or Abnormal Device State

 Another scenario concerns the device itself.

 A device may detect a tamper condition or another abnormal internal state.

 The sequence is:

 **Normal operation → abnormal device condition → local validation → event classification → priority communication → edge/cloud processing → operator alert → operational response.**

 This demonstrates that SSP monitors not only the protected environment but also the operational condition of the monitoring device.

---

 ## Privacy-Aware Monitoring

 Privacy is another important operational consideration.

 The system may generate information that is potentially sensitive, particularly location and movement information.

 The intended behavior is therefore:

 **Sensor information generated → local processing → information classified → necessary information identified → required information transmitted according to policy → unnecessary information retained or processed locally where appropriate.**

 The objective is not to define the final privacy implementation in D2.

 Instead, D2 establishes the requirement that privacy should influence the information flow throughout the system.

 This includes data minimization, controlled access, encryption, configurable retention and deletion, and auditable administrative access.

---

 ## Operator Workflow

 SSP can also be described from the operator's perspective.

 The operator logs into the system and reviews the monitored devices.

 The system provides information such as:

 **Status → location → risk information → battery state → connectivity → alerts.**

 If there is no critical event, monitoring continues.

 If an alert occurs, the operator reviews the available information, assesses the event according to the operational procedure, takes the required action and records or closes the event where appropriate.

 This operational workflow provides the basis for the later requirements concerning the user interface and cloud services.

---

 ## End-to-End Operational View

 Putting these scenarios together gives us the overall SSP operational concept.

 The environment produces physical information.

 That information is acquired by the device.

 The device performs local sensing and intelligence.

 Relevant information is processed at the edge.

 The cloud provides centralized intelligence, historical information and management functions.

 An authorized user receives the relevant information.

 The user can then initiate an operational response.

 The response can influence policies or configuration, which can subsequently modify the behavior of the device and edge processing.

 So SSP can be understood as an operational feedback loop:

 **Environment → Device → Local intelligence → Edge intelligence → Cloud intelligence → Authorized user → Operational response → Policy/configuration → Device and edge.**

 This is important because SSP is not intended to be simply a collection of sensors and communication components.

 It is intended to operate as a complete safety-monitoring system.

---

 # Chapter 3 — Existing Solutions and Opportunities for Improvement

 After defining how SSP is intended to be used, the next question is:

 **What already exists, and therefore what requirements are genuinely justified?**

 Our market study shows that several functions considered important for SSP are already established in commercial safety and tracking products.

 Existing solutions provide functions such as location tracking, geofencing, notifications, historical information and application-based monitoring.

 This means that these basic functions should not be presented as unique SSP innovations.

 Instead, the market study helps us identify the areas where further investigation and improvement are appropriate.

 The analysis identifies opportunities for improvement using:

 **distributed processing → adaptive monitoring → energy-aware operation → privacy-aware information flow → contextual event interpretation → resilient operation.**

 These improvement objectives are distributed across the SSP computational layers.

 At the **device level**, SSP is intended to perform local preprocessing, adaptive sensing, selected event detection, device-state monitoring and local buffering.

 The objective is to reduce unnecessary raw-data transmission, reduce energy consumption and maintain useful operation during communication interruptions.

 At the **edge level**, SSP is intended to provide more than simple protocol forwarding.

 The edge should be capable of validating, filtering, aggregating and interpreting information before it reaches the cloud.

 This can reduce cloud traffic, support low-latency processing and allow selected monitoring functions to continue when cloud connectivity is unavailable.

 At the **cloud level**, SSP is intended to provide centralized historical storage, scalable telemetry and event ingestion, analytics, AI model management, user and role management, auditing, data-retention control and authorized APIs.

 Another important objective is **privacy-aware processing**.

 Instead of treating privacy only as a cloud security issue, SSP treats data minimization as a system-level principle.

 Where a function can be achieved using processed or aggregated information instead of continuously transmitting raw sensor data, the lower-data approach should be preferred where appropriate.

 AI is also considered a distributed capability.

 Depending on latency, energy, computational resources, connectivity, privacy and model complexity, AI-assisted processing may potentially take place at the device, at the edge or in the cloud.

 D2 therefore defines AI capabilities and measurable targets without prescribing the final machine-learning model.

 Finally, energy efficiency is considered a system-level objective.

 Adaptive sensing, local processing, low-power operating modes and event-driven communication are intended to reduce unnecessary energy consumption.

 The important distinction is that these are **intended improvements**, not claims of already demonstrated superiority.

 The question of whether SSP is actually better than a particular commercial product can only be answered after implementation and measurement.

---

 # Chapter 4 — Functional and Performance Specifications

 The fourth chapter translates the previous chapters into engineering requirements.

 This is where we move from:

 **What problem do we have?**

 to:

 **How will SSP be used?**

 to:

 **What does the existing market already provide?**

 and finally:

 **What exactly must our system do, and how well must it do it?**

 We separate the requirements into two categories.

 A **functional requirement** describes what the system shall do.

 A **performance requirement** describes how well that function shall operate.

 This distinction is important throughout D2.

---

 ## Device Functions

 At the device level, SSP shall acquire motion information, positioning information and proximity information where applicable.

 It shall monitor its own battery, communication state, sensor state and relevant health indicators.

 It shall support local preprocessing and selected local event detection.

 It shall buffer relevant information when communication is temporarily unavailable.

 It shall manage its energy consumption according to the monitoring context.

 It shall receive authorized configuration information and maintain a unique device identity.

 The target product shall also support a secure firmware lifecycle.

---

 ## Edge Functions

 At the edge, SSP shall receive device information and validate message structure, identity, sequence information and data validity.

 It shall support timestamp verification, data ordering, aggregation, filtering and feature extraction.

 It shall execute selected event-processing functions and, where appropriate, low-latency inference.

 It shall provide offline buffering and synchronization after connectivity recovery.

 It shall detect duplicates and forward relevant information to the cloud.

 Most importantly, selected monitoring and event-processing functions shall continue when cloud connectivity is unavailable.

---

 ## Communication Functions

 The communication subsystem shall provide bidirectional device-to-edge and edge-to-cloud communication.

 It shall support telemetry, event information, device status and authorized configuration.

 It shall support retry and synchronization mechanisms and protect message integrity.

 Devices shall be authenticated, and communication failures shall be detectable.

 The exact communication technologies are intentionally not frozen in D2 because their selection belongs to the later architecture and implementation work.

---

 ## Cloud Functions

 The cloud shall register and authenticate devices and users.

 It shall receive and validate telemetry and events.

 It shall store historical information and maintain current device state.

 It shall provide event processing, analytics and AI model management where applicable.

 It shall manage users and roles and enforce access permissions.

 It shall maintain audit information and provide authorized APIs.

 It shall support fleet management, configurable retention and deletion, notifications and historical queries.

---

 ## User Interface Functions

 The user interface shall provide authorized users with current device status, current or recent position, events, battery state and communication status.

 It shall provide historical information and map-based visualization.

 Authorized users shall be able to perform permitted device, user and configuration management functions.

 The UI shall enforce the permissions of the authenticated user and shall not display information for which that user is not authorized.

---

 # Data Requirements

 D2 also defines what information is generated and exchanged.

 At the device level, the relevant data includes device identity, timestamps, motion information, positioning information, proximity state, battery state, device state, communication state, event information and sequence numbers.

 The logical representation is designed around two levels.

 The device uses a compact representation optimized for bandwidth and energy efficiency.

 The edge and cloud use a more structured representation optimized for processing and maintainability.

 The exact encoding technology will be selected later.

 The requirements also define target data volumes.

 A normal device telemetry packet has a target maximum application payload of **128 bytes**.

 An event packet has a target maximum application payload of **512 bytes**.

 The target normal application traffic is **no more than 10 kilobits per second per device on average**.

 The device-to-edge communication link is targeted at **at least 100 kilobits per second of application capacity**.

 This distinction is important because the communication link needs enough capacity for normal traffic as well as event bursts, retransmissions and protocol overhead.

 At the edge, structured records have a target maximum size of **1 kilobyte**.

 For UI and API communication, the target normal response size is **100 kilobytes**, with larger historical results handled through pagination.

---

 # Computational Performance

 The performance requirements establish measurable engineering targets.

 For the device, sensor acquisition latency is targeted at **20 milliseconds or less**.

 Local preprocessing is targeted at **100 milliseconds or less**.

 Local event-rule evaluation is targeted at **200 milliseconds or less**.

 Generation of a local event decision is targeted at **500 milliseconds or less**.

 The average local processing duty cycle is targeted at **20 percent or less**.

 For device-to-edge communication, the nominal application latency target is **2 seconds or less**.

 The system should support at least **24 hours of offline buffering** for relevant information.

---

 # Communication Performance

 The target device-to-edge communication is wireless, short-range, low-power and bidirectional.

 The nominal target range is **at least 10 metres**, with **5 metres defined as a minimum practical range target**.

 The target application capacity is **at least 100 kilobits per second**.

 Event delivery is targeted at **2 seconds or less** under nominal conditions.

 For edge-to-cloud communication, the system targets wireless wide-area connectivity, with an application capacity of at least **50 kilobits per second per device** and typical event latency of **5 seconds or less** under nominal connectivity conditions.

 The requirements explicitly recognize that external network availability cannot be guaranteed.

---

 # Energy Requirements

 Energy is a major constraint because the SSP device is intended to be portable or wearable.

 The target deep-sleep power is **1 milliwatt or less**.

 Normal monitoring is targeted at **50 milliwatts or less**.

 Active sensing is targeted at **150 milliwatts or less**.

 Communication bursts may reach a target peak of **500 milliwatts**.

 Positioning operation has a target peak of **300 milliwatts**.

 The minimum target battery autonomy is **7 days**, with an engineering objective of **14 days under nominal monitoring conditions**.

 These values are targets to be validated after hardware and software implementation.

---

 # Mechanical and Environmental Requirements

 The target device volume is **100 cubic centimetres or less**, and its mass is targeted at **100 grams or less**.

 The device should be wearable or portable.

 The target operating temperature range is **minus 10 to plus 50 degrees Celsius**.

 The target ingress protection is **IP65 or better**, and a drop resistance of at least **1 metre** is targeted.

 If a dedicated physical edge gateway is used, its target mass is **500 grams or less** and its target volume is **2 litres or less**.

 These requirements may be interpreted differently if the edge function is implemented using an existing smartphone, computer or gateway.

---

 # Cloud Requirements

 The initial cloud deployment is designed around **100 active devices**.

 The scalability objective is **at least 10,000 devices**.

 The initial ingestion capacity target is **100 messages per second**, with a burst target of **20 events per second**.

 Normal API queries target a **95th-percentile latency of 1 second or less**.

 Cloud event processing targets a **95th-percentile latency of 2 seconds or less**.

 The target cloud service availability is **99.5 percent or greater**.

 Historical data retention is targeted at **at least 12 months**.

 The initial deployment target is **at least 500 gigabytes of usable application storage**, while the production architecture must support expansion beyond this amount.

---

 # User Interface Requirements

 The UI should remain usable on desktop and mobile-class displays.

 The target login response is **2 seconds or less**.

 Dashboard loading is targeted at **3 seconds or less**.

 Current status refresh is targeted at **5 seconds or less**.

 Historical queries are targeted at a **95th-percentile response time of 2 seconds or less**.

 The UI should prioritize current state, recent position, significant events, battery state and communication status.

---

 # End-to-End Event Performance

 The overall operational event path is:

 **Sensor → Device or Edge → Cloud → UI.**

 For normal operationally significant events, the target end-to-end latency is **10 seconds or less** under nominal connectivity conditions.

 For high-priority events, the target is **5 seconds or less**.

 These are engineering targets rather than guaranteed values under network failure.

---

 # Security and Privacy

 Security and privacy are also functional requirements.

 SSP shall use unique device identities, authenticated communication and authenticated user access.

 The system shall support role-based authorization, encrypted communication, protected credentials, secure updates, audit logging and appropriate session management.

 For privacy, the system shall minimize unnecessary data collection and transmission.

 Sensitive information shall be protected in transit and at rest.

 Retention periods shall be configurable, deletion shall be supported, and administrative access shall be auditable.

 The final implementation must comply with the applicable data-protection requirements for its intended deployment.

---

 # AI Requirements

 AI is treated as an optional intelligence capability rather than a mandatory mechanism for every SSP function.

 Potential applications include movement classification, activity recognition, anomaly detection, contextual event classification, reduction of false events and predictive maintenance.

 The initial development targets include **90 percent or greater classification accuracy** on representative validation data, **90 percent or greater event recall**, and a target false-positive rate of **5 percent or less**.

 Edge inference is targeted at **200 milliseconds or less**.

 However, these metrics remain development targets.

 Their precise interpretation depends on the final dataset, event classes and validation methodology, which will be defined in later deliveries.

---

 # Economic Requirements

 Finally, D2 establishes economic constraints.

 The initial production-oriented device cost target is **150 euros or less per device**, with an objective of **100 euros or less** at larger production scale.

 Communication and cloud operating costs are targeted at **10 euros or less per device per month** under normal conditions.

 For an initial deployment of 100 devices, the first-year operational deployment target is **25,000 euros or less**, excluding personnel salaries and academic development labor.

 This provides a system-level economic constraint rather than evaluating only the cost of the device itself.

---

 # Closing — What D2 Establishes

 To conclude, D2 establishes the requirements baseline for SSP.

 The first chapter explains **why SSP is needed and what the system is intended to achieve**.

 The second chapter have therefore not yet claimed that SSP consumes a particular amount of energy explains **who uses SSP and how it operates in realistic scenarios**.

 The third chapter examines **existing solutions and identifies areas where SSP intends to investigate improvements**.

 The fourth chapter translates these findings into **functional and measurable performance requirements**.

 The complete reasoning can therefore be summarized as:

 **Safety-monitoring problem → SSP concept → operational users and scenarios → existing market capabilities → improvement opportunities → functional requirements → measurable performance requirements.**

 The important distinction is that D2 defines **targets**, not achieved results.

 We have therefore not yet claimed that SSP consumes a particular amount of energy, achieves a particular AI accuracy, provides a particular reliability level or is commercially superior to existing products.

 Those questions require implementation, measurement and validation in later deliveries.

 D2 provides the baseline against which those later results can be evaluated.

 The next step is D3, where the requirements established here will be used to develop and justify the **block and communications architecture** of SSP.

 Thank you.
