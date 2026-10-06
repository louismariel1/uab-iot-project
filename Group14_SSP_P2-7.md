Yes. I would make only the agreed wording corrections: standardize **“edge gateway”**, preserve the rest of the document as-is, and repair the corrupted Section VIII paragraph. Below is the complete updated version.

 # SmartSecurePerimeter (SSP): Distributed IoT Architecture for Perimeter Security and Personal Safety Monitoring

 **Louis-Marie Loe, Cheong Travis — Group 14, IoT Design Project 2026/2027**

 ## Abstract

 SmartSecurePerimeter (SSP) is a distributed IoT monitoring platform for perimeter security and personal safety using a wearable sensing device, edge processing, cloud services, and an authorized user interface. The system combines adaptive sensing, local and edge event processing, positioning, secure communication, and optional artificial intelligence (AI) to identify significant events while reducing unnecessary raw-data transmission. Unlike conventional trackers that depend primarily on continuous cloud connectivity, SSP retains selected monitoring and decision functions during communication loss.

 This paper presents the SSP architecture, operational storyboard, market positioning, quantitative performance targets, distributed AI strategy, energy model, security/privacy approach, and environmental constraints. At P2, the design remains platform- and protocol-neutral; specific hardware, communication protocols, and AI frameworks will be selected during implementation. The target retail selling price is €80–€120 per wearable unit, with a minimum battery-autonomy target of seven days and an extended objective of fourteen days.

 **Index Terms—** Internet of Things, wearable sensing, perimeter security, edge computing, artificial intelligence, geofencing, privacy, adaptive sensing.

 ## I. INTRODUCTION

 Conventional personal and asset tracking systems provide location and geofencing capabilities but often depend on continuous connectivity and centralized processing. This can increase energy and bandwidth consumption and limit response when communication is interrupted or contextual information requires low-latency evaluation. SSP addresses these limitations by distributing sensing, processing, and intelligence across the wearable, edge gateway, and cloud.

 The principal objective is a wearable monitoring node capable of detecting changes in location, motion, and device state while allowing computationally demanding interpretation at the edge gateway or cloud. Target scenarios include sensitive-zone protection, perimeter monitoring, personal safety, and monitoring of individuals subject to defined protection policies.

 The P2 design remains implementation-independent. The wearable is therefore defined as an ultra-low-power embedded platform with sensing, positioning, local processing, short-range communication, and temporary storage rather than a specific commercial IC. Communication is likewise described through functional classes. This preserves flexibility for subsequent hardware and architecture selection.

 The main contributions are:

 1. Distributed processing across device, edge, and cloud tiers.
2. Adaptive sensing based on operational context.
3. Intelligence placement according to latency, computational, and connectivity requirements.
4. Offline monitoring continuity through local decisions and buffering.
5. Privacy-aware reduction of unnecessary raw sensor transmission.

 ## II. SYSTEM CONCEPT AND ARCHITECTURE

 SSP comprises four functional tiers: wearable device, edge gateway, cloud services, and user interface. Security and privacy mechanisms apply across the architecture.

 **Fig. 1. SSP multi-tier architecture**

```
┌──────────────────────────────────────────────────────────────┐
│                         CLOUD TIER                           │
│ Historical Analytics • Cloud AI • Storage • Alert Services │
│ Spatial Heatmaps • Multi-device Correlation • APIs         │
└──────────────────────────────▲───────────────────────────────┘
                               │
                    Secure wide-area connection
                               │
┌──────────────────────────────┴───────────────────────────────┐
│                          EDGE TIER                           │
│ Event Fusion • Edge AI • Geofence Evaluation • Buffering   │
│ Offline Operation • Risk Scoring • Data Filtering           │
└──────────────────────────────▲───────────────────────────────┘
                               │
                     Low-power local connection
                               │
┌──────────────────────────────┴───────────────────────────────┐
│                         DEVICE TIER                          │
│ Motion/Position Sensors • ULP MCU • Local Processing       │
│ Local AI • Event Detection • Temporary Storage             │
│ Adaptive Sensing • Device-State Monitoring                  │
└──────────────────────────────┬───────────────────────────────┘
                               │
                               ▼
                  Protected Person / Environment
```

 ### A. Device Tier

 The wearable performs sensor acquisition, filtering, validation, feature extraction, and deterministic event evaluation. It operates at low duty cycle during normal monitoring and increases sensing activity under elevated-risk conditions. Selected information may be buffered locally.

 Normal sensing is supported up to 50 Hz and elevated/event-driven sensing up to 100 Hz. Sensor acquisition targets ≤20 ms and complete local event decisions ≤500 ms.

 Lightweight on-device AI may perform motion-pattern classification, sudden-motion/fall-like detection, and preliminary anomaly or tamper detection. These functions provide low latency and reduce communication overhead while preserving selected decision capability during connectivity loss.

 ### B. Edge Tier

 The edge combines motion, positioning, and device-state information, performs event validation, and executes selected AI functions. Edge intelligence includes motion/location fusion, trajectory prediction, geofence prediction, contextual risk scoring, and event confirmation. Selected edge AI inference targets ≤200 ms.

 The edge therefore provides the primary low-latency contextual interpretation layer. It can combine recent sensor history with positioning information to predict an approaching geofence boundary, assess contextual risk, and confirm events without requiring continuous raw sensor transmission to the cloud.

 The edge maintains selected processing and buffering functions during cloud loss; latency-critical monitoring therefore does not depend exclusively on cloud AI. The edge gateway may be implemented using a smartphone, computer, or dedicated gateway device.

 ### C. Cloud Tier

 The cloud provides persistent storage, historical analytics, device/user management, multi-device correlation, cloud AI, and authorized application access.

 Cloud AI is primarily intended for computationally intensive and historical functions, including spatial analytics and risk heatmaps, long-term movement and pattern analysis, cross-device/offender-proximity correlation across authorized monitoring sources, aggregate risk analysis, automated alert-support functions, and model evaluation/retraining. Cloud processing is not required for every sensing operation.

 The initial architecture supports ≥100 active devices and ≥100 telemetry messages/s, with a scalability objective toward 10,000 devices.

 ### D. User Interface and Roles

 Three principal personas are considered:

 - **Protected person:** wears the device and may receive local warnings.
- **Security operator:** monitors authorized individuals/zones and responds to priority events.
- **System administrator:** manages devices, policies, users, roles, and settings.

 Role-based security and privacy controls apply across all functions.

 ## III. OPERATIONAL STORYBOARD

 Table I summarizes the end-to-end interaction between the wearable, edge/cloud processing, protected person, operator, and administrator.

 **TABLE I — SSP OPERATIONAL STORYBOARD**

 | Phase | System / Sensor Action | User / Operator Interaction |
| --- | --- | --- |
| 1\. Pairing/setup | Protected connection established; identity, monitoring profile, zone, and configuration assigned. | Protected person equips device; administrator/operator assigns authorized role and zone. |
| 2\. Normal monitoring | Sensors operate at low duty cycle; local processing filters and summarizes information. | Person moves normally; operator sees status, battery, and connectivity. |
| 3\. Perimeter approach / abnormal motion | Adaptive sensing increases; local/edge processing evaluates trajectory, motion, and context. | Person may receive a warning; operator is notified when risk threshold is exceeded. |
| 4\. Priority event | Edge validates event and prioritizes location, event type, and relevant context for transmission. | Operator receives priority alert and initiates the response workflow. |
| 5\. Connectivity loss/recovery | Local/edge functions continue where possible; required information is buffered and synchronized after reconnection. | Operator can distinguish communication loss from normal operation; required history is restored. |

Normal operation is therefore low-power and information-minimal, while elevated-risk conditions activate additional sensing, processing, and communication resources.

 ## IV. MARKET BENCHMARK AND ECONOMIC TARGET

 Commercial personal trackers demonstrate established demand for positioning, geofencing, and mobile monitoring. Representative solutions include AngelSense, Jiobit, and T-Mobile SyncUP TRACKER \[4\]–\[8\]. SSP differentiates itself through distributed intelligence, adaptive sensing, privacy-aware information reduction, and local/edge operation during communication interruption.

 **TABLE II — COMPARATIVE MARKET POSITION**

 | Solution | Mechanism | Representative capability | Indicative retail position\* | SSP differentiation |
| --- | --- | --- | --- | --- |
| AngelSense | Cellular + positioning | Tracking, geofencing, emergency functions | Premium + subscription | Local/edge processing; reduced raw-data transmission |
| Jiobit | Multi-radio positioning | Trusted places, geofencing, proximity alerts | Mid/high + subscription | Contextual motion/risk processing; offline capability |
| SyncUP TRACKER | Cellular + positioning | Location tracking, geofencing, mobile application | Lower-cost + subscription | Perimeter-oriented risk intelligence |
| Proposed SSP | Wearable + edge + cloud | Adaptive sensing, distributed AI, geofencing, offline monitoring | RRP €80–€120 | Distributed intelligence, privacy-aware processing, resilience |

\*Competitor retail prices and subscription conditions vary by market and date; the table therefore uses relative retail positioning rather than fixed currency values.

 The P2 economic specification is the target retail selling price (RRP) rather than hardware BOM, infrastructure expenditure, or lifetime operating cost. SSP targets an RRP of €80–€120 per wearable unit. Detailed BOM and TCO analysis are deferred to later phases.

 ## V. FUNCTIONAL AND PERFORMANCE SPECIFICATION

 The detailed requirement catalogue is retained in Appendix A. Table III presents the principal P2 engineering targets.

 **TABLE III — PRINCIPAL SSP P2 REQUIREMENTS**

 | Domain | Principal target |
| --- | --- |
| Sensing | Normal ≤50 Hz; elevated ≤100 Hz |
| Device processing | Acquisition ≤20 ms; preprocessing ≤100 ms; local evaluation ≤200 ms; decision ≤500 ms |
| Device–edge path | Information availability ≤2 s nominal |
| Edge processing | ≤500 ms |
| Edge AI | ≤200 ms where implemented |
| Normal end-to-end latency | ≤10 s |
| High-priority event latency | ≤5 s |
| Cloud capacity | ≥100 devices initially; objective toward 10,000 |
| Cloud ingestion | ≥100 telemetry messages/s; ≥20 event messages/s burst |
| Cloud API | p95 ≤1 s |
| Cloud event processing | p95 ≤2 s |
| Availability | ≥99.5% target |
| Historical retention | ≥12 months, subject to policy |
| Size / mass | ≤100 cm³ / ≤100 g |
| Environment | −10 °C to +50 °C operating; −20 °C to +60 °C storage |
| Ingress | IP65 or better |
| Mechanical | ≥1 m drop; target IK07/IK08 |
| Battery | ≥7 days; 14-day engineering objective |
| Retail price | €80–€120 RRP |

The latency values are system-level budgets rather than independent subsystem allowances. In particular, the ≤5 s high-priority target covers the complete sensor-to-authorized-UI path.

 ## VI. DISTRIBUTED AI STRATEGY AND ENERGY MODEL

 ### A. AI Distribution

 AI is optional and complements deterministic processing. Simple threshold/state functions remain deterministic, while AI is applied where classification or prediction provides measurable benefit. Intelligence is distributed according to latency, computational complexity, connectivity, and data locality.

 **TABLE IV — DISTRIBUTION OF INTELLIGENCE**

 | Tier | AI / intelligent function | Primary objective |
| --- | --- | --- |
| Wearable | Motion-pattern classification, fall-like/sudden-motion detection, preliminary anomaly/tamper detection | Very low latency, low communication overhead, selected local operation |
| Edge / mobile gateway | Motion/location fusion, trajectory and geofence prediction, contextual risk scoring, event confirmation | ≤200 ms inference target; contextual low-latency processing and resilience during cloud loss |
| Cloud | Spatial risk analytics/heatmaps, long-term pattern analysis, cross-device correlation, aggregate risk, alert-support analytics, model evaluation/retraining | Historical, spatial, multi-device, computationally intensive analysis |

The wearable tier handles lightweight latency-critical functions within constrained resources. The edge gateway is the primary location for contextual event interpretation using multiple sensor sources or short-term history. This includes trajectory/geofence prediction and contextual risk scoring. The cloud handles historical, spatial, and multi-device intelligence.

 Latency-critical monitoring shall not depend exclusively on cloud AI. During temporary cloud loss, wearable and edge functions retain the monitoring, event evaluation, and buffering required by policy. Cloud-only functions such as heatmaps, long-term pattern analytics, and model evaluation may be deferred.

 Constrained wearable models shall use appropriate compression and/or quantization, including reduced-precision inference where suitable. A preliminary target is a 50–100 KB RAM footprint for the most constrained AI functions. An AI function selected for validation shall target ≥90% on an appropriate task-specific primary metric, with dataset, classes, and metric defined before evaluation. Safety-critical threshold/state functions retain deterministic fallback behaviour.

 ### B. Energy Strategy

 P2 energy requirements are defined through duty cycles and battery autonomy rather than component-level power values.

 **TABLE V — NOMINAL ENERGY DUTY-CYCLE TARGET**

 | Operating state | Nominal allocation |
| --- | --- |
| Deep sleep / minimum activity | ≥95% |
| Sensing and local processing | ≤4% |
| Wireless bursts | ≤1% |
| Exceptional event operation | Activated when required |
| Minimum autonomy | ≥7 days |
| Extended objective | 14 days |

The device shall adapt sensing, processing, and communication to operational context. Final battery capacity and component-level power consumption remain implementation-stage decisions.

 ## VII. SECURITY, PRIVACY AND PHYSICAL DESIGN

 ### A. Security

 SSP uses layered security covering device identity, authentication, authorization, protected communication, stored information, firmware, and audit. Devices require unique identities and authentication before protected operations are accepted. Sensitive information is protected in transit and at rest, with role-based access and auditable security operations. Firmware updates require authenticity verification.

 Security mechanisms shall not disable required monitoring during temporary external connectivity loss.

 ### B. Privacy

 SSP applies data minimization to sensitive location and movement information. Raw sensor data should be processed locally or at the edge when summarized or feature-level information provides equivalent functionality. Cloud transmission is limited to information required by the monitoring policy. Sensitive data are subject to role-based access, configurable retention, and authorized deletion.

 The measurable privacy objective is to reduce raw-sensor transmission whenever equivalent monitoring functionality can be achieved using processed, summarized, or aggregated information.

 ### C. Physical, Environmental and Wearability Design

 The wearable targets ≤100 cm³ and ≤100 g, with operation from −10 °C to +50 °C and storage from −20 °C to +60 °C. The enclosure shall achieve IP65 or better, tolerate a minimum 1 m drop, and target IK07/IK08 impact resistance.

 Materials exposed to prolonged skin contact shall be evaluated against applicable biocompatibility requirements, with ISO 10993 used as a reference where applicable. Materials shall tolerate expected perspiration, rain, and intended cleaning/disinfection exposure. Appropriate mechanical tamper detection shall be incorporated.

 ## VIII. VALIDATION AND CONCLUSION

 The P2 specification establishes measurable system-level targets without prematurely fixing commercial hardware, communication protocols, or AI frameworks. Subsequent development shall validate sensing and processing latency, end-to-end event response, battery autonomy, communication resilience, cloud scalability, AI performance, and physical/environmental robustness.

 Validation shall distinguish normal from elevated-risk operation and record operating mode, connectivity, system load, and event priority. AI validation shall additionally record execution tier, selected model/function, inference latency, resource use, dataset, classes, and task-specific performance metric. Cloud-only AI functions shall be evaluated separately from latency-critical device and edge functions.

 End-to-end latency shall be measured from a defined sensor-event timestamp to presentation in the authorized UI. Battery validation shall test the defined duty-cycle assumptions under representative workloads.

 SSP combines adaptive sensing, distributed intelligence, privacy-aware processing, and offline resilience. The principal engineering challenge is balancing event responsiveness against wearable energy constraints. Device and edge processing retain latency-sensitive functions near the sensing source, while cloud resources serve historical, spatial, and multi-device analysis.

 The resulting P2 design provides a basis for subsequent architecture, hardware, AI, security, and validation activities. Detailed requirement identifiers and verification criteria are retained in the accompanying single-column appendix.

 # APPENDIX A — DETAILED P2 REQUIREMENT MATRIX

 The following matrix provides the detailed P2 requirements and their planned verification basis. Requirement identifiers provide traceability between the detailed matrix and the principal P2 specifications presented in the main paper; implementation-specific verification criteria will be refined during subsequent project phases.

 The principal requirement-domain convention is:

 | Prefix | Requirement domain |
| --- | --- |
| F-Dxx | Device / wearable functional requirements |
| F-Exx | Edge functional requirements |
| F-Cxx | Cloud functional requirements |
| F-CLxx | Communication and connectivity requirements |
| F-Uxx | User-interface and user-function requirements |
| F-AIxx | Artificial-intelligence requirements |
| P-xxx | Quantitative performance requirements |
| SEC-xxx | Security and privacy requirements |
| ENV-xxx | Environmental, physical, and durability requirements |

### A. Device and Sensing Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-D01 | Wearable sensing | Device shall acquire motion and positioning information required by the configured monitoring policy. |
| F-D02 | Adaptive sensing | Device shall support normal and elevated sensing modes. |
| F-D03 | Normal sensing rate | Up to 50 Hz. |
| F-D04 | Elevated sensing rate | Up to 100 Hz. |
| F-D05 | Local filtering | Device shall perform local filtering before transmission where appropriate. |
| F-D06 | Local feature extraction | Device shall support local extraction of selected features required for event evaluation. |
| F-D07 | Temporary storage | Device shall buffer selected information during temporary communication loss. |
| F-D08 | Device-state monitoring | Device shall monitor relevant state information such as operating mode, battery state and connectivity status. |
| F-D09 | Local event evaluation | Complete local event decision target ≤500 ms. |
| F-D10 | Sensor acquisition | Target ≤20 ms. |

### B. Edge Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-E01 | Edge processing | Edge shall receive and process information from authorized wearable devices. |
| F-E02 | Event fusion | Edge shall combine relevant motion, positioning and device-state information. |
| F-E03 | Geofence evaluation | Edge shall support configured protection-zone evaluation. |
| F-E04 | Local risk scoring | Edge shall support contextual event/risk evaluation. |
| F-E05 | Offline continuity | Selected edge processing shall remain operational during cloud connectivity loss. |
| F-E06 | Buffering | Edge shall retain required information until connectivity is restored. |
| F-E07 | Edge AI | Edge may execute selected AI inference functions. |
| P-E01 | Edge inference | Target ≤200 ms for selected latency-critical AI inference tasks. |
| P-E02 | Edge event processing | Target ≤500 ms. |

### C. Cloud Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-C01 | Device management | Cloud shall support authorized device registration and management. |
| F-C02 | User management | Cloud shall support authorized user and role management. |
| F-C03 | Historical storage | Cloud shall retain authorized historical information. |
| F-C04 | Alert service | Cloud shall support authorized priority-event notification. |
| F-C05 | Multi-device correlation | Cloud shall support correlation across authorized monitoring sources. |
| F-C06 | Cloud AI | Cloud shall support computationally intensive and historical AI functions. |
| P-C01 | Initial capacity | ≥100 active devices. |
| P-C02 | Initial telemetry ingestion | ≥100 messages/s. |
| P-C03 | Event burst capacity | ≥20 event messages/s. |
| P-C04 | Scalability objective | Architecture toward 10,000 active devices. |
| P-C05 | API latency | Normal API p95 ≤1 s. |
| P-C06 | Event processing | p95 ≤2 s. |
| P-C07 | Availability | Target ≥99.5% for selected cloud deployment. |

### D. User Interface Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-U01 | Protected-person interface | Appropriate local warning/notification capability. |
| F-U02 | Operator interface | Authorized monitoring dashboard and priority alerts. |
| F-U03 | Administrator interface | Authorized configuration and management functions. |
| F-U04 | Role-based access | Users shall only access authorized information and functions. |
| F-U05 | Connectivity indication | UI shall distinguish communication loss from normal monitoring where possible. |
| F-U06 | Event presentation | Priority alerts shall include relevant available event and location information. |

### E. AI Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-AI01 | Wearable AI | Support selected constrained motion/anomaly functions where beneficial. |
| F-AI02 | Edge AI | Support contextual motion/location, trajectory/geofence, and risk inference where beneficial. |
| F-AI03 | Cloud AI | Support historical, spatial, and multi-device analytics. |
| F-AI04 | AI optimization | Constrained models shall be optimized for available resources using suitable compression and/or quantization. |
| P-AI01 | Wearable AI memory target | Preliminary target 50–100 KB RAM for constrained functions. |
| P-AI02 | Edge inference | Target ≤200 ms for selected latency-critical inference tasks. |
| P-AI03 | AI validation | ≥90% target for an appropriate task-specific primary metric where applicable. |
| F-AI05 | Validation definition | Dataset, classes and primary metric shall be defined before evaluation. |
| F-AI06 | Deterministic fallback | Safety-critical simple threshold/state functions shall not depend exclusively on AI. |

### F. Energy and Battery Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| P-EN01 | Deep sleep | ≥95% nominal time allocation. |
| P-EN02 | Sensing/processing | ≤4% nominal time allocation. |
| P-EN03 | Wireless bursts | ≤1% nominal time allocation. |
| P-EN04 | Minimum autonomy | ≥7 days under defined representative workload. |
| P-EN05 | Extended autonomy | 14-day engineering objective. |
| F-EN01 | Adaptive energy operation | Device shall adapt activity according to monitoring context. |
| F-EN02 | Event mode | High-risk event operation shall be treated as a transient state. |

No component-level mW or mA requirement is imposed at P2.

 ### G. Performance Requirements

 | ID | Requirement | Target |
| --- | --- | --- |
| P-P01 | Sensor acquisition | ≤20 ms |
| P-P02 | Local preprocessing | ≤100 ms |
| P-P03 | Selected latency-critical AI inference | ≤200 ms |
| P-P04 | Complete local event decision | ≤500 ms |
| P-P05 | Device-edge information availability | ≤2 s nominal target |
| P-P06 | Edge event processing | ≤500 ms |
| P-P07 | Normal end-to-end latency | ≤10 s |
| P-P08 | High-priority end-to-end latency | ≤5 s |
| P-P09 | Cloud API p95 | ≤1 s |
| P-P10 | Cloud event processing p95 | ≤2 s |

### H. Physical and Environmental Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| P-PHY01 | Device volume | ≤100 cm³ |
| P-PHY02 | Device mass | ≤100 g |
| P-PHY03 | Operating temperature | −10 °C to +50 °C |
| P-PHY04 | Storage temperature | −20 °C to +60 °C |
| P-PHY05 | Ingress protection | IP65 or better |
| P-PHY06 | Drop resistance | ≥1 m without loss of required functionality |
| P-PHY07 | Impact resistance | Target IK07/IK08 |
| F-PHY01 | Biocompatibility | Applicable prolonged-contact materials evaluated against relevant biocompatibility requirements; ISO 10993 used as reference where applicable. |
| F-PHY02 | Sweat resistance | Materials shall tolerate expected perspiration exposure. |
| F-PHY03 | Rain resistance | Materials/enclosure shall tolerate intended environmental exposure. |
| F-PHY04 | Cleaning resistance | Materials shall tolerate intended cleaning/disinfection agents. |
| F-PHY05 | Tamper detection | Enclosure shall provide an appropriate tamper-detection mechanism. |

### I. Security and Privacy Requirements

 | ID | Requirement | Target / Criterion |
| --- | --- | --- |
| F-S01 | Device identity | Each device shall possess a unique identity. |
| F-S02 | Authentication | Protected operations shall require authentication. |
| F-S03 | Authorization | Access shall be controlled according to role and policy. |
| F-S04 | Protected communication | Sensitive communications shall be protected. |
| F-S05 | Data protection | Sensitive stored information shall be protected. |
| F-S06 | Firmware authenticity | Firmware updates shall include authenticity verification. |
| F-S07 | Audit | Security-relevant operations shall be auditable. |
| F-S08 | Offline security | Connectivity loss shall not disable required local monitoring functions. |
| F-PR01 | Data minimization | Raw sensor information should not be transmitted when processed information provides equivalent functionality. |
| F-PR02 | Retention | Sensitive information shall be subject to configured retention policies. |
| F-PR03 | Deletion | Authorized deletion shall be supported. |
| F-PR04 | Privacy access control | Sensitive information shall be restricted according to role. |

# References

 \[1\] IEEE Author Center, “IEEE Article Templates,” IEEE.\
 \[2\] IEEE Author Center, “Structure Your Article,” IEEE.\
 \[3\] IEEE, “IEEE Editorial Style Manual for Authors,” IEEE Author Center.\
 \[4\] T-Mobile, “SyncUP TRACKER,” T-Mobile Support.\
 \[5\] AngelSense, “Safeguard GPS Location Tracker,” AngelSense.\
 \[6\] AngelSense, “Named Places (Geofences),” AngelSense Help Center.\
 \[7\] AngelSense, “Notification Types,” AngelSense Help Center.\
 \[8\] Jiobit, “Personal Safety,” Jiobit.

 This version keeps the substantive content unchanged while applying the agreed terminology cleanup and correcting the Section VIII corruption.
