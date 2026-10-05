# SmartSecurePerimeter (SSP): A Privacy-Aware Multi-Tier IoT Platform for Perimeter Security and Personal Safety

 **Louis-Marie Loe and Cheong Travis**\
 **Group 14, IoT Design Project 2026/2027**

 ## Abstract

 SmartSecurePerimeter (SSP) is a wearable and edge-assisted Internet of Things (IoT) platform intended to support perimeter security and personal safety monitoring. The system combines a low-power wearable sensing node, an edge processing layer, cloud services, and authorized user interfaces. Its principal design objectives are rapid event detection, adaptive energy operation, offline continuity, privacy-aware data processing, and scalable monitoring. Unlike conventional location trackers that primarily transmit positioning information, SSP performs local and edge processing to classify relevant motion and contextual events before transmitting selected information to the cloud. This paper summarizes the P2 functional and performance specification, market positioning, system architecture, operational workflow, artificial-intelligence strategy, energy requirements, environmental constraints, security, privacy, and scalability targets. Detailed individual requirements are maintained separately in the requirements annex.

 **Index Terms—** IoT, wearable sensing, perimeter security, edge computing, artificial intelligence, privacy, geofencing, personal safety.

 ## I. INTRODUCTION

 Perimeter security and personal safety applications require monitoring systems that can detect abnormal situations while remaining practical for continuous wearable operation. Existing consumer trackers provide useful location and geofencing capabilities, but many rely heavily on cloud connectivity and continuous communication. SSP addresses this limitation through a distributed architecture in which sensing, event evaluation, edge processing, and cloud analytics are separated according to latency, energy, privacy, and computational requirements.

 The target SSP system consists of four principal layers: a wearable device, an edge gateway, cloud services, and authorized user interfaces. The wearable collects relevant motion and positioning information and performs local filtering and event evaluation. The edge layer provides low-latency contextual processing and selected artificial-intelligence functions. The cloud provides persistent storage, multi-device analytics, historical analysis, administration, and authorized access. Communication loss does not disable the core local monitoring function.

 The P2 specification deliberately remains technology-neutral. Specific processors, sensors, radio technologies, cloud providers, databases, and machine-learning frameworks are to be selected during later architecture and implementation activities. The requirements instead specify measurable capabilities and performance targets.

 ## II. MARKET BENCHMARK AND ECONOMIC POSITIONING

 SSP is positioned between conventional location trackers and more specialized safety-monitoring systems. The principal differentiation is not basic location tracking but the combination of adaptive sensing, distributed intelligence, offline operation, privacy-aware processing, and perimeter-risk evaluation.

 ### TABLE I

 ### MARKET COMPARISON

 | Solution | Primary Mechanism | Representative Features | Retail Position | SSP Differentiation |
| --- | --- | --- | --- | --- |
| AngelSense GPS Tracker | Cellular positioning | Location tracking, geofencing, alerts | Approx. $99–$150 + subscription | Local/edge event processing and privacy-aware data reduction |
| Jiobit Smart Tag | Multi-source positioning | Trusted places, geofencing, proximity alerts | Approx. $130–$150 + subscription | Adaptive sensing and offline-capable edge intelligence |
| T-Mobile SyncUP TRACKER | Cellular + positioning | Tracking, geofencing, mobile application | Approx. $48–$96 + subscription | Greater emphasis on perimeter-risk intelligence |
| **SSP** | Wearable sensing + edge/cloud processing | Adaptive monitoring, event classification, geofencing, offline continuity | **Target RRP: €80–€120** | Distributed intelligence, privacy-first processing, resilience |

The SSP economic specification concerns **target retail selling price (RRP)** rather than hardware bill of materials (BOM), cloud hosting cost, or long-term maintenance cost. The P2 target is therefore an RRP of **€80–€120 per wearable unit**. Manufacturing BOM, cloud expenditure, service costs, and total cost of ownership are deferred to later project deliveries.

 The intended value proposition is a safety-monitoring device that reduces unnecessary raw-data transmission while providing faster local and edge decisions than a cloud-only architecture.

 ## III. SYSTEM ARCHITECTURE AND OPERATIONAL MODEL

 ### A. Multi-Tier Architecture

 The SSP architecture separates functions according to their timing, energy, privacy, and computational requirements.

 **Device layer:** A low-power wearable sensing node performs sensor acquisition, filtering, feature extraction, local event-rule evaluation, temporary buffering, device-health monitoring, and selected low-complexity intelligence. The device is designed to continue monitoring during communication loss.

 **Edge layer:** A nearby gateway performs higher-cost event interpretation, contextual risk evaluation, selected AI inference, data aggregation, and buffering. The edge layer reduces dependence on continuous cloud connectivity.

 **Cloud layer:** Cloud services provide persistent storage, historical analysis, multi-device correlation, long-term analytics, user/account management, alert workflows, and scalable computation.

 **User layer:** Authorized users interact through monitoring and administrative interfaces. The protected person receives appropriate local notifications, while security operators receive prioritized events, location/context information, and system-health information.

 **Security and privacy:** Security controls span all layers. Authentication, authorization, protected communication, data integrity, auditability, data minimization, retention control, and authorized deletion are system-level requirements.

 ### B. End-to-End Processing Path

 The principal operational path is:

 **Sensor observation → local device processing → edge processing → cloud processing → authorized UI**

 Normal events have a target end-to-end latency of **≤10 s**, while high-priority events have a target of **≤5 s** under nominal operating conditions.

 The architecture does not assign the complete latency budget independently to each subsystem. Instead, each stage must provide sufficient performance margin for the complete sensor-to-user path to satisfy the system-level target.

 ### C. Operational Storyboard

 ### TABLE II

 ### SSP OPERATIONAL STORYBOARD

 | Phase | System and Sensor Action | User / Operator Interaction |
| --- | --- | --- |
| **1\. Pairing and setup** | Wearable establishes an authorized relationship with an edge gateway; device identity and monitoring configuration are registered. | Protected person equips the device. Administrator/operator assigns the device and monitoring role. |
| **2\. Normal monitoring** | Motion and position sensors operate using an energy-aware sampling profile. Local processing filters and summarizes information. | Protected person continues normal activity. Operator dashboard displays normal status, battery and connectivity state. |
| **3\. Perimeter approach** | Position and motion processing identifies movement toward a configured restricted boundary. Sampling and processing may increase adaptively. | User receives an appropriate warning; operator interface indicates increasing risk where configured. |
| **4\. High-risk event** | Local/edge processing evaluates motion, position and contextual indicators. A priority event bypasses normal low-priority processing. | Operator receives a prioritized alert containing relevant event, location and risk information. |
| **5\. Connectivity loss** | Device and edge continue local monitoring and buffer required information. Critical local decisions remain available. | Operator sees connectivity degradation when possible; protected-person monitoring continues locally. |
| **6\. Reconnection** | Buffered information is synchronized and duplicate/sequence conditions are handled. | Historical continuity is restored without silently discarding required events. |
| **7\. Review and analysis** | Cloud services store authorized information and support historical and multi-device analytics. | Authorized users review events, trends and system status according to their access role. |

This storyboard explicitly connects the three principal human roles—protected person, security operator, and system administrator—to the corresponding system functions.

 ## IV. FUNCTIONAL AND PERFORMANCE SPECIFICATION

 Rather than reproducing the complete requirements catalogue, Table III summarizes the principal P2 targets.

 ### TABLE III

 ### KEY SSP REQUIREMENTS

 | Category | Representative P2 Target |
| --- | --- |
| Device sensing | Normal sensing up to 50 Hz; high-activity operation up to 100 Hz |
| Sensor acquisition | ≤20 ms nominal latency |
| Local preprocessing | ≤100 ms nominal latency |
| Local event evaluation | ≤200 ms nominal latency |
| Local event decision | ≤500 ms nominal latency |
| Device-to-edge application latency | Target ≤2 s |
| Edge processing | Target ≤500 ms per received record |
| Edge AI inference | Target ≤200 ms per inference |
| Normal end-to-end event latency | ≤10 s |
| High-priority event latency | ≤5 s |
| Initial cloud capacity | ≥100 active devices |
| Scalability objective | ≥10,000 active devices |
| Initial telemetry ingestion | ≥100 messages/s |
| Event burst capacity | ≥20 events/s |
| Normal API latency | p95 ≤1 s |
| Cloud event processing | p95 ≤2 s |
| Cloud availability | ≥99.5% target |
| Historical retention | ≥12 months |
| Initial usable storage | ≥500 GB |
| Device volume | ≤100 cm³ |
| Device mass | ≤100 g |
| Operating temperature | −10 °C to +50 °C |
| Storage temperature | −20 °C to +60 °C |
| Ingress protection | IP65 or better |
| Drop resistance | ≥1 m |
| Battery autonomy | Minimum 7 days; 14-day engineering objective |
| Target wearable RRP | €80–€120 |
| AI validation accuracy | ≥90% on representative validation data |

The complete F-/P-identifier catalogue is maintained in the requirements annex rather than the main paper.

 ## V. EDGE AND CLOUD AI STRATEGY

 AI is an optional intelligence capability and is used only where it provides measurable benefit over deterministic rules. The architecture distributes intelligence according to latency, computational cost, connectivity dependence, privacy, and energy constraints.

 ### A. Device and Edge Intelligence

 The wearable performs low-complexity processing such as filtering, feature extraction, deterministic event rules, tamper detection, and preliminary motion-state identification. Where computational resources permit, lightweight local classification can identify patterns such as falls, sudden running, abnormal movement, or possible physical struggle.

 The edge gateway provides the principal low-latency AI processing layer. Candidate functions include motion-pattern classification, contextual event classification, local geofence trajectory evaluation, risk scoring, and event prioritization. Edge inference shall target **≤200 ms per inference** under nominal conditions.

 This architecture avoids continuous transmission of raw sensor streams when equivalent monitoring functionality can be achieved through local or edge processing.

 ### B. Cloud Intelligence

 Cloud-side AI is reserved for computationally heavier and longer-term tasks. Candidate functions include:

 - multi-device spatial risk analysis and heatmaps;
- long-term movement-pattern analysis;
- correlation of events across authorized monitoring sources;
- historical anomaly analysis;
- automated alert prioritization and dispatch support; and
- model evaluation and retraining workflows.

 Cloud processing is therefore complementary to, rather than a replacement for, local and edge event decisions.

 ### C. AI Resource Constraints

 AI models intended for wearable or edge execution shall be selected or optimized to operate within the available computational and energy budget. Model compression and reduced-precision inference shall be considered, with an engineering target of a lightweight model footprint suitable for constrained embedded execution.

 A representative design objective is an inference memory footprint in the **50–100 KB range** for the most constrained local models, subject to validation against the selected hardware. The P2 specification does not mandate a particular AI framework, processor, model architecture, or commercial implementation.

 The principal AI performance target is **≥90% prediction/classification accuracy on representative validation data**, with the final task definition, dataset, classes, and evaluation methodology established during implementation.

 ## VI. ENERGY, MECHANICAL AND ENVIRONMENTAL REQUIREMENTS

 ### A. Energy Budget

 P2 shall specify energy primarily through operating time and autonomy rather than component-level electrical consumption, because exact power consumption depends on hardware selected in later deliveries.

 The nominal operating profile shall therefore favor a low-duty-cycle state:

 - **Deep sleep:** target \>95% of normal operating time.
- **Sensing and local processing:** target \<4% of normal operating time.
- **Wireless transmission/reception bursts:** target \<1% of normal operating time, excluding defined exceptional high-activity periods.

 The wearable shall provide a **minimum target autonomy of 7 days**, with an engineering objective of **14 days** under the defined nominal monitoring profile. Adaptive sensing, processing and communication shall reduce unnecessary activity.

 ### B. Mechanical and Environmental Requirements

 The wearable shall have a target volume below **100 cm³** and mass below **100 g**, excluding deployment-specific mounting accessories. It shall support a wearable or portable form factor and withstand a drop of at least 1 m without loss of required monitoring functionality.

 The target environmental operating range is **−10 °C to +50 °C**, with storage from **−20 °C to +60 °C**. The enclosure shall target **IP65 or better**.

 Because the device is intended for prolonged wearable use, the enclosure and mounting components shall use materials and surface treatments appropriate for prolonged skin contact and shall be designed with reference to applicable **ISO 10993 biocompatibility requirements**. Materials shall tolerate perspiration, rain, and routine surface cleaning/disinfection without unacceptable degradation.

 The enclosure shall also target **IK07/IK08 impact resistance** and incorporate appropriate physical tamper detection. These requirements address intentional damage, physical altercation, and enclosure opening in addition to normal environmental exposure.

 ## VII. SECURITY, PRIVACY AND SCALABILITY

 Security is implemented as a system-level property. Each device shall have a unique identity and protected communication relationship. Users shall be authenticated and authorized according to role and scope. Sensitive information in transit and at rest shall be protected against unauthorized access and modification. The system shall support message-integrity validation, replay protection where required, secure firmware update, audit records, and controlled session management.

 Privacy is addressed through data minimization and distributed processing. SSP shall avoid transmitting raw sensor information when processed or summarized information is sufficient for the intended monitoring function. Sensitive location and movement information shall be accessible only according to authorization policy. Retention shall be configurable and authorized deletion shall be supported.

 The cloud architecture shall initially support at least **100 active devices**, **100 telemetry messages/s**, and **20 event messages/s in bursts**, while maintaining a scalability objective of at least **10,000 active devices**. Storage shall initially provide at least **500 GB usable capacity** and support at least **12 months of historical retention**, with scalable expansion as the monitored population increases.

 ## VIII. CONCLUSION

 The revised P2 specification defines SSP as a multi-tier IoT safety-monitoring platform emphasizing low-latency event detection, adaptive energy use, privacy-aware processing, offline continuity, and scalable cloud analytics. The principal P2 contribution is the allocation of functions across wearable, edge, cloud, and user-interface layers rather than dependence on a single centralized processing stage.

 The proposed targets establish measurable criteria for subsequent architecture and implementation activities: ≤5 s high-priority end-to-end event latency, ≥7-day battery autonomy, €80–€120 target wearable RRP, ≥90% AI validation accuracy, and scalable support for up to 10,000 devices. Detailed requirements remain available in the accompanying annex so that the main P2 paper remains concise and suitable for the required IEEE two-column format.

 ## REFERENCES

 \[1\] IEEE Author Center, “Authoring Tools and Templates,” IEEE.

 \[2\] IEEE Author Center, “Structure Your Paper,” IEEE.

 \[3\] IEEE, “IEEE Editorial Style Manual for Authors,” IEEE Author Center.

 \[4\] T-Mobile, “SyncUP TRACKER,” T-Mobile Support.

 \[5\] AngelSense, “Safeguard GPS Location Tracker,” AngelSense.

 \[6\] AngelSense, “Named Places (Geofences),” AngelSense Help Center.

 \[7\] AngelSense, “Notification Types,” AngelSense Help Center.

 \[8\] Jiobit, “Personal Safety,” Jiobit.
