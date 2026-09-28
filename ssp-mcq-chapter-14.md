## Chapter 14\. Study and Assessment 
## Chapter 14\. Business, architecture into a productization, economic and deployment model. It does not introduce a new technical architecture; instead, it derives the business consequences of the decisions Costs and Scalability

 Chapter 14 translates the technically defined SmartSecurePerimeter (SSP) architecture into a productization, economic and deployment model. It does not introduce a new technical architecture; instead, it derives the business consequences of the decisions established in Chapters 3–13.

 A central methodological principle is:

 > **The figures in this chapter are engineering and business-planning estimates, not validated supplier quotations or commercial offers.**

 The distinction between confirmed design decisions, budgetary assumptions and items requiring future supplier validation is therefore maintained throughout.

 ## 14.1 Value Proposition

 The SSP architecture developed in Chapters 5–13 defines an integrated **Device → Edge/Mobile → Cloud → User** IoT system for intelligent perimeter and proximity monitoring.

 The proposed value does not originate from any individual technology such as GNSS, BLE, cellular communication, cloud computing or artificial intelligence. Rather, it arises from integrating these technologies into a coordinated system capable of providing:

 - continuous location and contextual monitoring;
- proximity and perimeter protection;
- local and Edge/Mobile processing;
- context-aware event interpretation;
- adaptive monitoring;
- communication resilience;
- privacy-aware processing;
- centralized fleet management;
- secure lifecycle management;
- operational alerting and visualization;
- historical analytics and system-wide intelligence.

 The resulting value proposition is:

 > **SSP provides an integrated platform for continuous, context-aware and resilient perimeter monitoring, combining wearable sensing, local/edge intelligence and cloud-based operational management while considering energy, security, privacy and scalability from the beginning of the design.**

 The principal value dimensions are summarized below.

 | Value dimension | SSP contribution |
| --- | --- |
| Protection | Continuous monitoring of defined people, devices and protection zones |
| Situational awareness | Combination of location, motion, proximity and device-state information |
| Response time | Local and Edge processing can reduce dependence on cloud round-trip processing |
| Resilience | Selected functions can continue during connectivity disruption |
| Energy efficiency | Monitoring and communication intensity can adapt to operational context |
| Privacy | Processing can be distributed according to necessity and sensitivity |
| Security | Device identity, authentication, secure communication and lifecycle management are incorporated |
| Scalability | Centralized cloud services and fleet management support larger deployments |
| Analytics | Historical information can support analysis and model improvement |
| Integration | APIs allow controlled exchange with authorized external systems |

Therefore, SSP should be evaluated as a **complete operational system**, rather than as a collection of individual components.

---

 ## 14.2 Business Model

 SSP is most appropriately considered a **hardware-enabled IoT service** rather than a standalone hardware product.

 The proposed model contains three principal layers:

 **SSP Device**

 → wearable/perimeter-monitoring hardware;

 **SSP Platform**

 → Edge/Mobile software, cloud infrastructure, event processing, data storage, device management and analytics;

 **SSP Operational Service**

 → dashboards, alerts, configuration, support, maintenance, security updates and lifecycle management.

 The resulting model is:

 > **Hardware + Platform + Recurring Service**

 A customer therefore acquires a complete monitoring capability rather than simply purchasing an electronic device.

 The conceptual commercial structure is:

 **Initial deployment**

 → devices + installation/configuration + integration

 **Recurring operation**

 → platform access + cloud processing + storage + device management + connectivity \+ support

 **Lifecycle services**

 → maintenance + software updates + security management \+ replacement/upgrade.

 This structure is consistent with the architecture because cloud, connectivity and operational services remain active throughout the device lifecycle.

---

 ## 14.3 Customer Model

 The organization purchasing SSP and the people using SSP do not necessarily have to be the same entity.

 ### 14.3.1 Customer

 The customer is the organization contracting for the SSP service.

 Potential customer categories include:

 - public-sector organizations;
- authorized monitoring organizations;
- institutional protection services;
- private security organizations;
- organizations responsible for high-risk personnel or facilities;
- other legally authorized organizations requiring controlled perimeter monitoring.

 The precise target market depends on the final deployment context, procurement requirements and applicable legislation.

 ### 14.3.2 Operational user

 The operational user interacts with the SSP monitoring interface.

 Typical users may include:

 - monitoring operators;
- security personnel;
- authorized supervisors;
- system administrators;
- incident-response personnel.

 ### 14.3.3 Protected or monitored user

 The protected user primarily interacts with the physical SSP device and may have limited interaction with the cloud platform.

 ### 14.3.4 Technical administrator

 The technical administrator manages:

 - device registration;
- configuration;
- firmware/software versions;
- connectivity status;
- credentials;
- system health;
- maintenance activities.

 This separation is important because the person wearing the device, the person monitoring an event and the organization paying for the service may be different parties.

---

 ## 14.4 Revenue Model

 The SSP revenue model can combine several components.

 ### 14.4.1 Hardware revenue

 The initial deployment may include a charge for each SSP device covering, as appropriate:

 - electronics;
- sensors;
- enclosure;
- battery;
- connectivity hardware;
- assembly;
- testing;
- initial configuration.

 ### 14.4.2 Platform subscription

 A recurring platform fee can cover:

 - cloud infrastructure;
- device management;
- data storage;
- event processing;
- dashboards;
- APIs;
- software maintenance;
- security updates.

 A per-device-per-month model is compatible with an IoT fleet because a significant proportion of service usage grows with the number of active devices.

 ### 14.4.3 Integration services

 Larger deployments may require integration with existing institutional systems.

 Potential integration services include:

 - API integration;
- identity integration;
- data migration;
- deployment configuration;
- operational workflow integration;
- training.

 ### 14.4.4 Support and maintenance

 An annual support agreement could cover:

 - technical support;
- hardware replacement;
- preventive maintenance;
- firmware updates;
- security updates;
- system monitoring;
- agreed service-level commitments.

 The project therefore establishes a **commercial structure**, rather than claiming that a final market price has already been validated.

---

 ## 14.5 Hardware BOM

 The hardware architecture established in Chapter 6 provides the starting point for the economic analysis.

 The exact component selection and supplier prices must be confirmed during detailed engineering and procurement. The following is therefore a **budgetary BOM structure**, not a supplier quotation.

 | Hardware category | SSP function | Expected cost significance |
| --- | --- | --- |
| MCU/SoC | Embedded control and local processing | Medium |
| GNSS subsystem | Outdoor positioning | Medium |
| Cellular subsystem | Wide-area communication | Medium/High |
| BLE subsystem | Local communication/proximity | Low/Medium |
| IMU | Motion sensing | Low |
| Additional sensors | Tamper/device-state/context | Low/Medium |
| Flash/RAM/storage | Local buffering | Low |
| Power-management ICs | Regulation and charging | Low/Medium |
| Battery | Autonomous operation | Low/Medium |
| Antennas | GNSS/BLE/cellular | Low/Medium |
| Security element, if required | Hardware-backed identity | Low/Medium |
| Haptic/LED/audio actuator | Local notification | Low |
| PCB | Hardware integration | Medium |
| Enclosure | Physical protection | Medium |
| Charging/service interface | Maintenance | Low/Medium |
| Assembly and testing | Manufacturing | Medium |

A critical distinction is required between:

 **Electronic BOM**

 and

 **complete manufactured-device cost**.

 The BOM does not include all manufacturing, testing, certification, logistics, warranty and engineering costs.

 Thus:

 > **Manufacturing cost \> electronic component BOM**

 and:

 > **Commercial cost \> manufacturing cost**

 These distinctions should remain explicit when the economic model is later refined.

---

 ## 14.6 Manufacturing Cost

 Manufacturing cost includes substantially more than the electronic components.

 A simplified model is:

 > **Manufacturing cost = Components \+ PCB fabrication/assembly \+ enclosure + assembly \+ programming + calibration \+ functional testing + packaging + manufacturing overhead**

 A production process would include:

 1. PCB procurement;
2. component placement and soldering;
3. board-level electrical testing;
4. firmware programming;
5. sensor calibration;
6. enclosure assembly;
7. device identification and credential provisioning;
8. communication testing;
9. functional validation;
10. final packaging.

 Prototype and production economics will differ substantially.

 A prototype may require development boards, manual assembly and engineering-grade components. A production device should instead use production PCB designs, optimized component sourcing, automated or semi-automated assembly, automated testing and controlled provisioning.

 Consequently:

 > **The laboratory PoC cost must not be interpreted as the expected manufacturing cost of the final SSP product.**

---

 ## 14.7 Development Cost

 The complete SSP system requires substantially more engineering than the wearable hardware alone.

 | Work package | Main activities |
| --- | --- |
| System engineering | Requirements, architecture, interfaces and verification |
| Hardware engineering | Schematics, PCB, power, RF and sensor integration |
| Embedded software | Drivers, sensing, power management and communications |
| Mobile/Edge software | BLE, local processing and user functions |
| Cloud/backend | APIs, event processing, databases and device management |
| Frontend | Operational dashboards and administration |
| AI/analytics | Dataset preparation, model development and deployment |
| Security | Identity, credentials, secure update mechanisms and testing |
| Industrial design | Enclosure, ergonomics and environmental protection |
| Testing | Functional, environmental, communication, security and reliability testing |
| Regulatory/compliance | Applicable radio, EMC, safety and product assessments |
| Deployment engineering | Installation, configuration and integration |
| Documentation | Technical, operational and maintenance documentation |

A planning relationship is:

 > **Total development cost = Engineering personnel \+ specialist services + prototypes + test equipment \+ certification + software/cloud development + project management**

 The actual value depends on development duration, staffing, geographic location, certification scope and the amount of technology reused.

---

 ## 14.8 Cloud and Operational Cost

 The cloud architecture defined in Chapter 12 creates recurring operational expenditure.

 These costs can be divided into:

 ### Infrastructure

 - compute;
- managed databases;
- object storage;
- backups;
- networking;
- monitoring.

 ### Communication

 - cellular connectivity;
- messaging;
- API traffic;
- notification services.

 ### Software services

 - authentication;
- observability;
- logging;
- security monitoring;
- model-serving infrastructure where required.

 ### Human operations

 - system administration;
- technical support;
- incident response;
- security operations;
- customer support.

 A simplified relationship is:

 > **Monthly operational cost = Cloud infrastructure \+ connectivity + storage \+ processing + monitoring \+ support + maintenance**

 Not all costs scale linearly.

 For example, cellular connectivity and device-specific storage may increase approximately with fleet size, while some cloud services and operational functions can be shared across the entire fleet.

 Therefore:

 **Fleet size ↑ → variable costs ↑**

 while, subject to efficient utilization:

 **Fleet size ↑ → average cost per device may decrease.**

 This relationship should be validated using actual workload measurements rather than assumed in advance.

---

 ## 14.9 Maintenance Cost

 SSP is a connected security-oriented system and therefore requires lifecycle maintenance.

 ### Hardware maintenance

 - battery replacement;
- device replacement;
- enclosure repair;
- sensor recalibration where required;
- damaged-device handling.

 ### Firmware maintenance

 - bug fixes;
- security patches;
- communication-stack updates;
- power-management improvements;
- sensor-driver updates.

 ### Cloud/software maintenance

 - backend updates;
- database maintenance;
- API evolution;
- dashboard updates;
- security patches;
- infrastructure upgrades.

 ### AI maintenance

 AI models may require:

 - performance monitoring;
- dataset updates;
- retraining;
- model validation;
- controlled deployment;
- rollback.

 ### Operational maintenance

 The service should also support:

 - device inventory;
- configuration management;
- credential management;
- incident investigation;
- replacement management;
- service monitoring.

 Maintenance is therefore part of the SSP product lifecycle rather than an optional activity after deployment.

---

 ## 14.10 Total Cost of Ownership

 The economic evaluation should cover the complete system lifetime rather than only the initial device purchase.

 For a deployment containing $N$ devices over $Y$ years:

 $$
TCO =
C_{development}
+
C_{deployment}
+
N C_{hardware}
+
Y C_{platform}
+
Y C_{connectivity}
+
Y C_{maintenance}
+
C_{integration}
$$

 where:

 - $C_{development}$ = allocated product-development cost;
- $C_{deployment}$ = installation and initial configuration;
- $C_{hardware}$ = per-device acquisition/manufacturing cost;
- $C_{platform}$ = recurring cloud/platform cost;
- $C_{connectivity}$ = recurring communications cost;
- $C_{maintenance}$ = recurring maintenance/support cost;
- $C_{integration}$ = customer-specific integration cost.

 For a detailed financial analysis, these values may additionally be discounted to present value.

 The fundamental principle is:

 > **SSP must be evaluated using lifecycle cost, not hardware acquisition cost alone.**

 For example, a lower-cost device could have higher connectivity, battery replacement or maintenance costs. Therefore, hardware and communication decisions from Chapters 6 and 7 must ultimately be evaluated together with the TCO model.

---

 ## 14.11 Pricing Assumptions

 A final commercial selling price should not be assigned without market and supplier validation.

 Instead, the pricing architecture can consist of:

 ### Hardware price

 A one-time price or deployment charge for the physical device.

 ### Recurring service price

 A recurring charge covering:

 - cloud platform;
- device management;
- data processing;
- storage;
- connectivity;
- support.

 ### Professional services

 Additional charges for:

 - integration;
- deployment;
- customization;
- training;
- migration.

 A conceptual pricing relationship is:

 $$
P_{customer}
=
P_{hardware}
+
P_{deployment}
+
Y(P_{platform}+P_{connectivity}+P_{support})
+
P_{integration}
$$

 The actual commercial values require future validation through:

 - supplier quotations;
- target-customer research;
- deployment requirements;
- service-level requirements;
- expected fleet size;
- regulatory costs;
- competitive benchmarking.

 Thus, Chapter 14 defines the **pricing structure**, not a final unsupported selling price.

---

 ## 14.12 Production Volumes

 SSP economics should be considered across several production stages.

 ### Stage 1 — Engineering prototypes

 Typical characteristics:

 - very small quantity;
- high unit cost;
- manual assembly;
- development hardware;
- extensive engineering intervention.

 The objective is technical verification rather than cost optimization.

 ### Stage 2 — Pilot deployment

 Typical characteristics:

 - tens to hundreds of devices;
- controlled production;
- production-intent hardware;
- field testing;
- operational feedback.

 The objective is to validate the product and service under realistic conditions.

 ### Stage 3 — Initial production

 Typical characteristics:

 - hundreds to thousands of devices;
- improved supplier agreements;
- automated testing;
- controlled manufacturing;
- formal fleet management.

 ### Stage 4 — Scaled production

 Typical characteristics:

 - larger purchasing volumes;
- optimized component sourcing;
- increased manufacturing automation;
- improved logistics;
- lower average unit cost.

 The general economic progression is:

 **Prototype → Pilot → Production → Scale**

 with unit cost potentially decreasing as production volume and process maturity increase, subject to component availability, supplier pricing and fixed-cost allocation.

---

 ## 14.13 Scalability

 Scalability has been incorporated into SSP at the architectural level.

 The system must accommodate growth in:

 - number of devices;
- number of users;
- number of protection zones;
- event rate;
- stored data volume;
- operational organizations;
- geographic deployments.

 The basic strategy is to separate device functions from centralized fleet services.

 At the device level:

 > **Each device operates independently.**

 At the cloud level:

 > **Fleet services manage many devices.**

 This means that increasing the fleet does not require a fundamental redesign of the individual device.

 The cloud architecture can scale suitable services independently:

```
Devices
   ↓
IoT ingestion
   ↓
Event processing
   ↓
Storage
   ↓
Analytics
   ↓
Operational interfaces
```

 ### Fleet management

 A scalable deployment should include:

 - unique device identifiers;
- automated provisioning;
- remote configuration;
- firmware-version management;
- device-health monitoring;
- credential management;
- device decommissioning;
- audit logging.

 Without these capabilities, administrative complexity could become a greater constraint than raw cloud processing capacity.

---

 ## 14.14 Deployment Strategy

 A real SSP deployment should proceed incrementally.

 ### Phase 1 — Engineering validation

 Objectives:

 - verify hardware;
- validate sensors;
- verify communication;
- validate power assumptions;
- verify basic software;
- test cloud interfaces.

 Chapter 13's laboratory PoC belongs primarily to this phase.

 ### Phase 2 — Engineering prototype

 The PoC is progressively replaced by production-intent hardware and software, including:

 - selected components;
- integrated PCB;
- intended enclosure;
- intended communication architecture;
- production-oriented firmware;
- security architecture.

 ### Phase 3 — Controlled pilot

 A limited real-world deployment evaluates:

 - reliability;
- usability;
- battery performance;
- communication coverage;
- false-event behavior;
- environmental performance;
- operational workflows;
- maintenance requirements.

 ### Phase 4 — Compliance and operational qualification

 The system undergoes applicable:

 - regulatory assessments;
- radio testing;
- EMC testing;
- environmental testing;
- cybersecurity assessment;
- privacy assessment;
- operational qualification.

 ### Phase 5 — Production deployment

 Following successful validation, SSP can transition into controlled manufacturing and deployment.

 ### Phase 6 — Continuous lifecycle operation

 The operational lifecycle becomes:

 **Monitor → Maintain → Update → Validate → Improve**

 This is especially relevant to cybersecurity and AI-enabled functions, because software vulnerabilities and model performance can change over time.

---

 ## 14.15 Development Roadmap

 The complete SSP development roadmap is:

 ### Phase A — Requirements and architecture

 **Chapters 1–5**

 - problem definition;
- stakeholder analysis;
- requirements;
- market/context analysis;
- system architecture.

 ### Phase B — Engineering design

 **Chapters 6–12**

 - hardware;
- communication;
- software;
- data flow;
- AI;
- energy/performance;
- cloud architecture.

 ### Phase C — Laboratory proof of concept

 **Chapter 13**

 - representative device;
- BLE communication;
- Mobile/Edge functions;
- cloud connectivity;
- event demonstration;
- limitations analysis.

 ### Phase D — Engineering prototype

 The PoC is progressively replaced by production-intent hardware and software:

 - custom PCB;
- integrated sensors;
- production communication modules;
- enclosure;
- security provisioning;
- complete software stack;
- initial production-oriented cloud deployment.

 ### Phase E — Verification and validation

 **Chapter 15**

 The complete system is evaluated through:

 > **Requirement → Metric → Test → Result → Pass/Fail**

 ### Phase F — Pilot deployment

 A limited real-world deployment evaluates:

 - operational usability;
- communication reliability;
- energy performance;
- event detection;
- maintenance processes;
- cloud scalability;
- security controls.

 ### Phase G — Production

 The system transitions to controlled manufacturing and operational deployment.

 ### Phase H — Lifecycle evolution

 Future releases may introduce:

 - improved hardware;
- improved battery performance;
- additional communication options;
- improved AI models;
- improved analytics;
- additional integrations;
- expanded operational capabilities.

 The overall roadmap is therefore:

 **Requirements → Architecture → Engineering Design → PoC → Prototype → Validation → Pilot → Production → Lifecycle Improvement**

---

 ## 14.16 Economic Design Principles

 Several principles emerge from the combined technical and business analysis.

 ### Principle 1 — Optimize TCO, not only unit cost

 Hardware, connectivity, cloud and maintenance costs must be evaluated together.

 ### Principle 2 — Avoid unnecessary hardware complexity

 Each additional component can increase:

 - BOM cost;
- power consumption;
- software complexity;
- manufacturing complexity;
- failure opportunities.

 A component should therefore be included when its contribution is justified by a system requirement.

 ### Principle 3 — Use the architecture to control recurring costs

 Local and Edge processing can reduce unnecessary communication and cloud processing where technically appropriate.

 The relationship is:

 **Useful local processing**

 → potentially less unnecessary data transmission

 → potentially lower communication/storage/processing requirements.

 This is not assumed to create a guaranteed financial saving. The actual effect must be measured during performance and validation testing.

 ### Principle 4 — Design for fleet management

 At large scale, the operational cost of manually maintaining devices can become significant.

 Automated provisioning, monitoring, configuration and software updates are therefore economically important.

 ### Principle 5 — Security is a lifecycle cost

 Security expenditure may include:

 - secure hardware;
- credential management;
- secure-update infrastructure;
- penetration testing;
- vulnerability management;
- security monitoring.

 Security must therefore be included in the long-term economic model.

 ### Principle 6 — AI must justify its operational cost

 AI introduces:

 - development costs;
- training-data requirements;
- model-management costs;
- computational costs;
- validation requirements.

 AI functionality should therefore remain subject to the measurable-benefit principle established in Chapter 10.

---

 ## 14.17 Relationship Between Technical Architecture and Business Scalability

 The SSP technical architecture and business model are directly connected.

 The relationship is:

 **Device**

 → generates sensing information

 **Edge/Mobile**

 → performs selected local processing

 **Communication layer**

 → transports required information

 **Cloud**

 → provides centralized services

 **Operational interface**

 → converts system information into authorized operational action.

 This separation enables a service-based commercial model.

 The physical device establishes the installed base, while:

 **Cloud + connectivity + support**

 form the recurring service component.

 Therefore, the business architecture follows naturally from the technical architecture rather than being added independently after the engineering design.

---

 ## 14.18 Business Risks

 The SSP business case contains several uncertainties.

 ### Regulatory risk

 Applicable legislation may constrain where and how monitoring technology can be deployed.

 ### Procurement risk

 Institutional customers may require formal procurement, certification, integration and service-level commitments.

 ### Hardware supply risk

 Component availability can affect both cost and product continuity.

 ### Connectivity cost risk

 Recurring cellular or other wide-area communication costs may become significant as fleet size increases.

 ### Support-cost risk

 Large deployments may require substantial operational support.

 ### Security risk

 A security incident could have financial and operational consequences.

 ### AI performance risk

 AI-based functions require continuing validation and maintenance.

 ### Integration risk

 Organizations may require integration with existing systems before SSP can be incorporated into operational workflows.

 ### Cost-estimation risk

 The values at this stage are budgetary assumptions and will change when supplier quotations, prototype data and production information become available.

 These risks should therefore be explicitly tracked during later product-development and validation stages.

---

 ## 14.19 Chapter 14 Design Decisions

 The business analysis establishes the following decisions.

 ### BD-01 — SSP is a hardware-enabled IoT service

 The solution is treated as:

 > **Device + Platform + Operational Service**

 rather than solely as hardware.

 ### BD-02 — Recurring services are part of the product

 Cloud, connectivity, device management, maintenance and security updates are part of the operational SSP service.

 ### BD-03 — TCO is the principal economic framework

 Hardware acquisition cost alone is insufficient for lifecycle evaluation.

 ### BD-04 — Fleet management is economically necessary

 Centralized provisioning, configuration, monitoring and updating are required to prevent operational complexity from increasing disproportionately with fleet size.

 ### BD-05 — PoC costs are excluded from final commercial costing

 Laboratory development-board and prototype costs do not represent the manufacturing cost of the final SSP device.

 ### BD-06 — Production economics require production-intent hardware

 The final BOM and manufacturing cost must be recalculated after component, PCB, enclosure and supplier validation.

 ### BD-07 — Cloud costs should follow measured workload

 The cloud architecture should use scalable services while avoiding unnecessarily expensive permanently allocated resources.

 ### BD-08 — Security is included in lifecycle economics

 Security testing, credential management, monitoring, updates and vulnerability management are part of the operating model.

 ### BD-09 — AI must demonstrate economic as well as technical value

 AI remains subject to measurable operational benefit.

 ### BD-10 — Deployment is incremental

 The intended progression is:

 **PoC → Engineering Prototype → Pilot → Validation → Production**

---

 ## 14.20 Relationship to Previous Chapters

 Chapter 14 translates the previous technical decisions into economic and deployment consequences.

 | Previous chapter | Business/scalability consequence |
| --- | --- |
| Chapter 3 — Requirements | Defines capabilities that must be developed and validated |
| Chapter 4 — Market/Context | Establishes operational context and potential market |
| Chapter 5 — Architecture | Enables separation of Device, Edge, Cloud and User services |
| Chapter 6 — Hardware | Determines major BOM and manufacturing drivers |
| Chapter 7 — Communication | Determines connectivity cost, coverage and availability |
| Chapter 8 — Software | Creates continuing development and maintenance requirements |
| Chapter 9 — Data Flow | Determines transmission, processing and storage requirements |
| Chapter 10 — AI | Introduces model-development, computational and lifecycle costs |
| Chapter 11 — Energy/Performance | Influences battery, connectivity and hardware requirements |
| Chapter 12 — Cloud | Defines recurring infrastructure and platform costs |
| Chapter 13 — PoC | Demonstrates feasibility without defining final production cost |

The resulting engineering chain is:

 **Requirements**

 → **Architecture**

 → **Hardware + Communication \+ Software**

 → **Data + AI**

 → **Performance/Energy**

 → **Cloud**

 → **PoC**

 → **Business Model + TCO \+ Scalability**

---

 ## 14.21 Chapter 14 Conclusion

 Chapter 14 establishes the economic and productization layer of SSP without changing the technical architecture established in previous chapters.

 The proposed business structure is:

 **Initial investment**

 → hardware + deployment \+ integration

 **Recurring operation**

 → connectivity + cloud + storage + processing + support

 **Lifecycle operation**

 → maintenance + security \+ software updates + device replacement.

 This structure follows naturally from the SSP **Device → Edge/Mobile → Cloud → User** architecture.

 The analysis also demonstrates why a final commercial cost cannot yet be stated with precision. Supplier quotations, production PCB design, enclosure engineering, certification requirements, manufacturing arrangements, connectivity contracts and operational service levels remain to be validated.

 The appropriate economic progression is therefore:

 > **Conceptual cost model → Engineering BOM → Prototype cost → Pilot cost → Production cost → Validated TCO**

 The laboratory PoC remains explicitly separate from the commercial product definition.

 The complete SSP development path is consequently:

 > **Requirements → Architecture → Engineering Design → PoC → Prototype → Validation → Pilot → Production → Lifecycle Improvement**

 The next stage is **Chapter 15 — Testing & Validation**, which converts the requirements and technical decisions developed throughout Chapters 3–14 into measurable verification activities.

 The central evaluation chain becomes:

 > **Requirement → Metric → Test → Result → Pass/Fail**

 This provides the final engineering evidence needed to determine whether the proposed SSP design satisfies its defined technical requirements.
