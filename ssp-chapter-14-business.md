## Chapter 14 — Plan

 The chapter will follow the frozen structure exactly.

 | Section | Purpose | Main design question |
| --- | --- | --- |
| **14.1 Value proposition** | Translate SSP technical capabilities into customer/operational value | Why would an organization deploy SSP? |
| **14.2 Business model** | Define how SSP is delivered as a product/service | Product, SaaS, managed service, or hybrid? |
| **14.3 Customer model** | Identify who purchases and who operates SSP | Who pays vs. who uses it? |
| **14.4 Revenue model** | Define possible revenue streams | Hardware, subscription, service, integration? |
| **14.5 Hardware BOM** | Connect Chapter 6 hardware to economics | What is the approximate per-device material cost? |
| **14.6 Manufacturing cost** | Estimate production economics | What does a deployable device cost beyond the BOM? |
| **14.7 Development cost** | Estimate engineering investment | What is required to turn the design into a product? |
| **14.8 Cloud/operational cost** | Estimate recurring infrastructure cost | What does operating SSP cost per device/deployment? |
| **14.9 Maintenance cost** | Account for lifecycle operations | Updates, support, replacement, calibration, security? |
| **14.10 TCO** | Combine capital and recurring costs | What is the cost over the system lifetime? |
| **14.11 Pricing assumptions** | Establish a future commercial model without pretending it is validated | What assumptions would determine price? |
| **14.12 Production volumes** | Examine economies of scale | How does unit economics change from pilot to fleet? |
| **14.13 Scalability** | Connect business scale to technical architecture | Can the same architecture support larger fleets? |
| **14.14 Deployment strategy** | Define realistic product rollout | How would SSP move from engineering to deployment? |
| **14.15 Development roadmap** | Establish remaining product-development stages | What happens after the PoC? |

A key methodological rule will be maintained throughout:

 > **The numbers in Chapter 14 are engineering/business planning estimates, not validated supplier quotations or commercial offers.**

 The chapter will therefore distinguish **known design decisions**, **budgetary assumptions**, and **items requiring future supplier validation**.

---

 # 14\. Business / Costs / Scalability

 ## 14.1 Value Proposition

 The technical architecture developed in Chapters 5–13 defines SSP as a complete Device → Edge/Mobile → Cloud → User IoT system for intelligent perimeter and proximity monitoring.

 The business value of SSP does not arise from any individual technology such as GNSS, BLE, cellular communication, cloud computing or artificial intelligence. These technologies are individually established. The proposed value lies in their integration into a system that can combine:

 - continuous location and contextual monitoring;
- proximity and perimeter protection;
- local and edge processing;
- context-aware event interpretation;
- adaptive monitoring;
- communication resilience;
- privacy-aware information processing;
- centralized fleet management;
- secure lifecycle management;
- operational alerting and visualization.

 The resulting value proposition can therefore be expressed as:

 > **SSP provides an integrated platform for continuous, context-aware and resilient perimeter monitoring, combining wearable sensing, local/edge intelligence and cloud-based operational management while considering energy, security, privacy and scalability from the beginning of the design.**

 The principal value dimensions are summarized below.

 | Value dimension | SSP contribution |
| --- | --- |
| Protection | Continuous monitoring of defined people, devices and protection zones |
| Situational awareness | Combination of location, motion, proximity and device-state information |
| Response time | Local and edge processing can reduce dependence on round-trip cloud processing |
| Resilience | Selected monitoring and event functions can continue during connectivity disruption |
| Energy efficiency | Monitoring and communication intensity can adapt to operational context |
| Privacy | Information processing can be distributed according to necessity and sensitivity |
| Security | Device identity, authentication, secure communication and lifecycle management are included in the design |
| Scalability | Centralized cloud services and device management support fleet deployment |
| Analytics | Historical data and AI services can support analysis and model improvement |
| Integration | APIs allow SSP to exchange information with authorized external systems |

The value proposition should therefore be evaluated at the **system level** rather than by comparing individual components.

---

 ## 14.2 Business Model

 SSP is most appropriately considered a **hardware-enabled IoT service** rather than a standalone hardware product.

 The proposed business model contains three principal layers:

 **SSP Device**

 → wearable/perimeter-monitoring hardware deployed to the protected or monitored user;

 **SSP Platform**

 → mobile/edge services, cloud infrastructure, event processing, device management, data storage and analytics;

 **SSP Operational Service**

 → dashboards, alerts, configuration, support, maintenance, security updates and lifecycle management.

 This produces a hybrid business model:

 **Hardware + Platform + Recurring Service**

 A deployment organization would therefore not simply purchase an electronic device. It would acquire a complete monitoring capability.

 The conceptual commercial structure is:

 **Initial deployment**

 → devices + installation/configuration + integration

 **Recurring operation**

 → platform access + cloud processing + storage + device management + support

 **Lifecycle services**

 → maintenance + software updates + security management + replacement/upgrade

 This model is consistent with the architecture because the cloud and operational components represent continuing services rather than one-time hardware functions.

---

 ## 14.3 Customer Model

 SSP involves several different roles that should not be assumed to be the same organization.

 ### 14.3.1 Customer

 The customer is the organization that contracts for the SSP service.

 Potential customer categories include:

 - public-sector organizations;
- authorized monitoring organizations;
- institutional protection services;
- private security organizations;
- organizations responsible for high-risk personnel or facilities;
- other legally authorized organizations requiring controlled perimeter monitoring.

 The precise customer segment would depend on the final deployment context and applicable legislation.

 ### 14.3.2 Operational user

 The operational user is the person who interacts with the SSP monitoring interface.

 Typical operational users could include:

 - monitoring operators;
- security personnel;
- authorized supervisors;
- system administrators;
- incident-response personnel.

 ### 14.3.3 Protected/monitored user

 The protected or monitored user interacts primarily with the physical device and may have limited interaction with the software platform.

 ### 14.3.4 Technical administrator

 The technical administrator manages:

 - device registration;
- configuration;
- firmware/software versions;
- connectivity status;
- credentials;
- system health;
- maintenance activities.

 This separation is important because the person wearing the device, the person monitoring an event and the organization paying for the service may be three different entities.

---

 ## 14.4 Revenue Model

 The proposed SSP revenue model can combine several components.

 ### 14.4.1 Hardware revenue

 The initial deployment may include a charge for each SSP device.

 This can cover:

 - electronics;
- sensors;
- enclosure;
- battery;
- connectivity hardware;
- device assembly;
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

 A per-device-per-month model is particularly compatible with an IoT fleet architecture because recurring cost scales approximately with the number of active devices and associated service usage.

 ### 14.4.3 Integration services

 Larger deployments may require integration with existing institutional systems.

 Integration services could therefore represent a separate revenue component covering:

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
- service-level commitments.

 The final revenue model would need to be validated against the target market and procurement environment. The present project establishes the technical basis for such a model rather than claiming that a particular commercial price has already been validated.

---

 ## 14.5 Hardware BOM

 The hardware architecture defined in Chapter 6 provides the starting point for estimating the cost of one SSP device.

 The exact component selection and supplier prices would be confirmed during detailed engineering and procurement. The following therefore represents a **budgetary BOM structure**, rather than a supplier quotation.

 | Hardware category | Typical SSP function | Budgetary cost category |
| --- | --- | --- |
| MCU/SoC | Embedded control and local processing | Medium |
| GNSS subsystem | Outdoor positioning | Medium |
| Cellular subsystem | Wide-area communication | Medium/High |
| BLE subsystem | Local communication/proximity | Low/Medium |
| IMU | Motion sensing | Low |
| Additional sensors | Tamper/device-state/context | Low/Medium |
| Flash/RAM/storage | Local data/event buffering | Low |
| Power-management ICs | Battery regulation and charging | Low/Medium |
| Battery | Autonomous operation | Low/Medium |
| Antennas | GNSS/BLE/cellular communication | Low/Medium |
| Security element, if required | Hardware-backed credentials | Low/Medium |
| Haptic/LED/audio actuator | Local notification | Low |
| PCB | Hardware integration | Medium |
| Enclosure | Physical protection | Medium |
| Charging/service interface | Maintenance | Low/Medium |
| Assembly and test | Manufacturing | Medium |

A useful distinction must be made between:

 **Electronic BOM**

 and

 **complete manufactured device cost**.

 The BOM does not include all manufacturing, testing, certification, logistics, warranty and engineering costs.

 For planning purposes, the project should therefore use the following relationship:

 > **Manufacturing cost \> electronic component BOM**

 and:

 > **Commercial cost \> manufacturing cost**

 The difference between these levels is important when Chapter 14 is later converted into a detailed financial model.

---

 ## 14.6 Manufacturing Cost

 Manufacturing cost includes significantly more than individual components.

 A simplified manufacturing-cost model is:

 **Manufacturing cost = Components + PCB fabrication/assembly + enclosure + assembly + programming + calibration + functional testing + packaging + manufacturing overhead**

 The production process would include at least:

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

 The economics will change significantly between prototype and production.

 A prototype may require:

 - engineering-grade components;
- manual assembly;
- development boards;
- laboratory instrumentation;
- manual configuration.

 A production device should instead use:

 - production PCB design;
- optimized component sourcing;
- automated or semi-automated assembly;
- automated testing;
- controlled provisioning;
- repeatable calibration;
- production-grade enclosure manufacturing.

 Consequently, the laboratory PoC cost should **not** be used as the predicted manufacturing cost of the final SSP device.

---

 ## 14.7 Development Cost

 The complete SSP system requires considerably more engineering than the physical wearable device.

 The development program can be divided into the following work packages:

 | Work package | Main activities |
| --- | --- |
| System engineering | Requirements, architecture, interfaces and verification |
| Hardware engineering | Schematics, PCB, power design, RF and sensor integration |
| Embedded software | Drivers, sensing, power management, communication and firmware |
| Mobile/edge software | BLE communication, local processing and user functions |
| Cloud/backend | APIs, event processing, databases and device management |
| Frontend | Operational dashboards and administration interfaces |
| AI/analytics | Dataset preparation, model development and deployment |
| Security | Identity, credentials, secure boot/update and penetration testing |
| Industrial design | Enclosure, ergonomics and environmental protection |
| Testing | Functional, environmental, communication, security and reliability tests |
| Regulatory/certification | Applicable radio, EMC, safety and product compliance activities |
| Deployment engineering | Installation, configuration and operational integration |
| Documentation | Technical documentation, user documentation and maintenance procedures |

Development cost should therefore be treated as a **multi-disciplinary product-development investment**.

 A simple planning model is:

 > **Total development cost = Engineering personnel + specialist services + prototypes + test equipment + certification + software/cloud development + project management**

 The actual value would depend on development duration, staffing level, geographic location, certification scope and the amount of existing technology reused.

---

 ## 14.8 Cloud and Operational Cost

 The cloud architecture described in Chapter 12 introduces recurring operational costs.

 These can be divided into:

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

 A simplified recurring-cost relationship can be expressed as:

 > **Monthly operational cost = Cloud infrastructure + connectivity + storage + data processing + monitoring + support + maintenance**

 The cost will not scale perfectly linearly.

 For example, some resources such as a baseline cloud environment are shared across the fleet, while other costs such as cellular connectivity and device-specific storage increase approximately with the number of deployed devices.

 This distinction creates an important scalability principle:

 **Fleet size ↑ → variable costs ↑**

 while:

 **Fleet size ↑ → cost per device can decrease**

 provided that shared infrastructure is efficiently utilized.

---

 ## 14.9 Maintenance Cost

 SSP is a connected security-oriented system and therefore requires lifecycle maintenance.

 Maintenance should include:

 ### Hardware maintenance

 - battery replacement;
- device replacement;
- enclosure repair;
- sensor recalibration where necessary;
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
- rollback capability.

 ### Operational maintenance

 The service should also support:

 - device inventory;
- configuration management;
- credential management;
- incident investigation;
- replacement management;
- service monitoring.

 This reinforces the lifecycle-security decision established in Chapters 4–8.

---

 ## 14.10 Total Cost of Ownership

 The TCO should include the complete lifecycle rather than only the initial hardware purchase.

 A simplified model for a deployment containing $N$ devices over $Y$ years is:

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

 - $C_{development}$ = product-development cost allocated to the deployment;
- $C_{deployment}$ = installation and initial configuration;
- $C_{hardware}$ = per-device acquisition/manufacturing cost;
- $C_{platform}$ = recurring platform/cloud cost;
- $C_{connectivity}$ = recurring communications cost;
- $C_{maintenance}$ = recurring maintenance and support cost;
- $C_{integration}$ = customer-specific integration cost.

 For a more detailed financial model, these costs should also be discounted to present value.

 The key principle is:

 > **The economic evaluation of SSP must include both capital expenditure and recurring operational expenditure.**

 For example, a device with a lower acquisition price but substantially higher communication, battery replacement or maintenance costs could produce a higher lifetime cost.

 Therefore, component selection in Chapter 6 and communication selection in Chapter 7 must ultimately be evaluated together with the TCO model.

---

 ## 14.11 Pricing Assumptions

 The project should not assign a final commercial price without market validation.

 Instead, the future pricing model can be structured around:

 ### Hardware price

 A one-time price or deployment charge for the physical SSP device.

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

 A conceptual customer pricing equation is:

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

 The actual commercial values should be established only after:

 - supplier quotations;
- target-customer interviews;
- deployment requirements;
- service-level requirements;
- expected fleet size;
- regulatory costs;
- competitive benchmarking.

 Thus, this chapter establishes the **pricing structure**, not an unsupported final selling price.

---

 ## 14.12 Production Volumes

 SSP economics should be considered across multiple production stages.

 ### Stage 1 — Engineering prototypes

 Typical characteristics:

 - very small quantity;
- high unit cost;
- manual assembly;
- development hardware;
- extensive engineering intervention.

 The objective is technical verification rather than commercial optimization.

 ### Stage 2 — Pilot deployment

 Typical characteristics:

 - tens to hundreds of devices;
- controlled production process;
- production-intent hardware;
- field testing;
- operational feedback.

 The objective is to validate the complete product and service.

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
- automated manufacturing;
- improved logistics;
- lower average unit cost.

 The expected economic relationship can therefore be represented as:

 **Prototype → Pilot → Production → Scale**

 with:

 **Unit cost ↓**

 as production volume and process maturity increase, subject to component availability and fixed-cost effects.

---

 ## 14.13 Scalability

 Scalability was incorporated into SSP from the architectural level.

 The system should support growth in:

 - number of devices;
- number of users;
- number of protection zones;
- event rate;
- stored data volume;
- number of operational organizations;
- number of geographic deployments.

 The scalability strategy is based on separation between device functions and centralized services.

 At the device level:

 **Each device operates independently**

 At the cloud level:

 **Fleet services manage many devices**

 This avoids requiring a redesign of the physical device architecture when the fleet grows.

 The cloud architecture should support horizontal scaling of suitable services.

 For example:

 **Devices**

 → ingestion services

 → event-processing services

 → storage

 → analytics

 → operational interfaces

 These services can be scaled independently according to workload.

 The same principle applies to databases and event-processing components.

 ### Fleet management

 A scalable SSP deployment should include:

 - unique device identifiers;
- automated provisioning;
- remote configuration;
- firmware-version management;
- device health monitoring;
- credential management;
- device decommissioning;
- audit logging.

 Without these capabilities, increasing fleet size would cause administrative complexity even if the underlying cloud infrastructure could technically handle the traffic.

---

 ## 14.14 Deployment Strategy

 A real-world SSP deployment should proceed incrementally.

 ### Phase 1 — Engineering validation

 Objectives:

 - verify hardware;
- validate sensors;
- verify communication;
- validate power assumptions;
- verify basic software;
- test cloud interfaces.

 The laboratory PoC described in Chapter 13 belongs primarily to this phase.

 ### Phase 2 — Engineering prototype

 The design would then move to a production-intent prototype incorporating:

 - selected components;
- integrated PCB;
- intended enclosure;
- intended communication architecture;
- production-oriented firmware;
- security architecture.

 ### Phase 3 — Controlled pilot

 A limited real-world deployment would evaluate:

 - reliability;
- usability;
- battery performance;
- communication coverage;
- false-event behavior;
- environmental performance;
- operational workflows;
- maintenance requirements.

 ### Phase 4 — Compliance and operational qualification

 The system would undergo the applicable:

 - regulatory assessments;
- radio testing;
- EMC testing;
- environmental testing;
- cybersecurity assessment;
- privacy assessment;
- operational qualification.

 ### Phase 5 — Production deployment

 Following successful validation, SSP could transition into controlled production and deployment.

 ### Phase 6 — Continuous lifecycle operation

 After deployment, the system would continue through:

 **Monitor → Maintain → Update → Validate → Improve**

 This is particularly important for cybersecurity and AI-enabled functions because both software vulnerabilities and model performance can evolve over time.

---

 ## 14.15 Development Roadmap

 The complete SSP development roadmap can be represented as follows:

 ### Phase A — Requirements and architecture

 **Chapters 1–5**

 - problem definition;
- stakeholder analysis;
- requirements;
- market analysis;
- system architecture.

 ### Phase B — Engineering design

 **Chapters 6–12**

 - hardware;
- communications;
- software;
- data flow;
- AI;
- energy/performance;
- cloud architecture.

 ### Phase C — Laboratory proof of concept

 **Chapter 13**

 - implement representative device;
- establish BLE communication;
- implement mobile/edge functions;
- connect to cloud services;
- demonstrate event flow;
- document limitations.

 ### Phase D — Engineering prototype

 The PoC is replaced progressively by production-intent hardware and software.

 Activities include:

 - custom PCB;
- integrated sensors;
- production communication modules;
- enclosure;
- security provisioning;
- complete software stack;
- initial cloud deployment.

 ### Phase E — Verification and validation

 **Chapter 15**

 The complete system is evaluated against:

 **Requirement → Metric → Test → Result → Pass/Fail**

 ### Phase F — Pilot deployment

 A limited real-world deployment validates:

 - operational usability;
- communication reliability;
- energy performance;
- event detection;
- maintenance processes;
- cloud scalability;
- security controls.

 ### Phase G — Production

 The system moves to controlled manufacturing and operational deployment.

 ### Phase H — Lifecycle evolution

 Future releases can introduce:

 - improved hardware;
- improved battery performance;
- new communication options;
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

 Hardware, connectivity, cloud and maintenance costs must be considered together.

 ### Principle 2 — Avoid unnecessary hardware complexity

 Each additional component increases:

 - BOM cost;
- power consumption;
- software complexity;
- manufacturing complexity;
- failure opportunities.

 A component should therefore be included when its contribution is justified by a system requirement.

 ### Principle 3 — Use the architecture to control recurring costs

 Local and edge processing can reduce unnecessary communication and cloud processing when technically appropriate.

 This creates the relationship:

 **More useful local processing**

 → potentially less unnecessary data transmission

 → potentially lower recurring communication/storage cost.

 This is not assumed to produce a guaranteed financial saving; it must be quantified during Chapter 11 and Chapter 15.

 ### Principle 4 — Design for fleet management

 The cost of manually maintaining thousands of devices can exceed the cost of the hardware itself.

 Automated provisioning, monitoring, configuration and software updates are therefore economically significant.

 ### Principle 5 — Security is a lifecycle cost

 Security should be budgeted from the beginning.

 Costs may include:

 - secure hardware;
- certificate/credential management;
- secure update infrastructure;
- penetration testing;
- vulnerability management;
- security monitoring.

 ### Principle 6 — AI must justify its operational cost

 AI processing introduces:

 - development cost;
- training-data requirements;
- model-management cost;
- computational cost;
- validation requirements.

 AI should therefore be retained where it provides measurable improvement over an appropriate deterministic approach.

---

 ## 14.17 Relationship Between Technical Architecture and Business Scalability

 The SSP architecture and business model are directly connected.

 The relationship can be summarized as:

 **Device**

 → generates sensing information

 **Edge/Mobile**

 → performs selected local processing

 **Communication layer**

 → transports required information

 **Cloud**

 → provides centralized services

 **Operational interface**

 → converts system information into operational action

 This architecture enables a service-based commercial model because the physical device and the continuously operating digital platform are separated.

 Consequently:

 **Hardware deployment**

 creates the installed device base,

 while:

 **Cloud + connectivity + support**

 create the recurring service component.

 This is one reason the architecture was designed as a Device → Edge/Mobile → Cloud → User system rather than as a standalone tracking device.

---

 ## 14.18 Business Risks

 The SSP business case contains uncertainties that should be explicitly recognized.

 ### Regulatory risk

 The applicable legal framework may limit where and how monitoring technology can be deployed.

 ### Procurement risk

 Institutional customers may require formal procurement, certification, integration and service-level commitments.

 ### Hardware supply risk

 Component availability can affect both cost and product continuity.

 ### Connectivity cost risk

 Recurring cellular or other wide-area communication costs can become significant at fleet scale.

 ### Support-cost risk

 Large deployments may require substantial operational support.

 ### Security risk

 A security incident could create financial, operational and reputational consequences.

 ### AI performance risk

 AI-based functionality may require continuing validation and maintenance.

 ### Adoption risk

 Organizations may require integration with existing systems before SSP can be operationally useful.

 ### Cost-estimation risk

 The values presented at this design stage are budgetary assumptions and will change when supplier quotations and production data become available.

 These risks should therefore be incorporated into the later validation and business-planning stages rather than hidden within the cost model.

---

 ## 14.19 Chapter 14 Design Decisions

 The business analysis produces the following design decisions.

 ### BD-01 — SSP is a hardware-enabled IoT service

 The solution should be considered as:

 **Device + Platform + Operational Service**

 rather than only as a hardware product.

 ### BD-02 — Recurring services are part of the product architecture

 Cloud, connectivity, device management, maintenance and security updates should be considered part of the operational SSP service.

 ### BD-03 — TCO is the principal economic evaluation framework

 Hardware price alone is insufficient. The system should be evaluated across its complete lifecycle.

 ### BD-04 — Fleet management is economically necessary

 Centralized provisioning, configuration, monitoring and update capabilities are required to prevent operational costs from increasing disproportionately with fleet size.

 ### BD-05 — The PoC is excluded from commercial cost estimation

 Laboratory hardware and development-board costs should not be interpreted as the manufacturing cost of the final SSP device.

 ### BD-06 — Production economics require production-intent hardware

 Final BOM and manufacturing costs must be recalculated after component selection, PCB design, enclosure design and supplier validation.

 ### BD-07 — Cloud costs should scale with actual workload

 The cloud architecture should use scalable services and avoid allocating expensive resources permanently where workload does not justify them.

 ### BD-08 — Security is included in lifecycle economics

 Security updates, credential management, monitoring and security testing must be included in the long-term operating model.

 ### BD-09 — AI must demonstrate economic as well as technical value

 AI functionality should remain subject to the measurable-benefit principle established in Chapter 10.

 ### BD-10 — Deployment should be incremental

 SSP should progress through:

 **PoC → Engineering Prototype → Pilot → Validation → Production**

 rather than moving directly from laboratory demonstration to large-scale deployment.

---

 ## 14.20 Relationship to Previous Chapters

 Chapter 14 does not introduce a new technical architecture. Instead, it translates previous technical decisions into economic and deployment consequences.

 | Previous chapter | Business/scalability consequence |
| --- | --- |
| Chapter 3 — Requirements | Defines the capabilities that must be paid for and validated |
| Chapter 4 — Market/Context | Establishes the operational context and market opportunity |
| Chapter 5 — Architecture | Enables separation of device, edge, cloud and user services |
| Chapter 6 — Hardware | Determines major device BOM and manufacturing drivers |
| Chapter 7 — Communication | Determines connectivity cost, coverage and operational availability |
| Chapter 8 — Software | Creates continuing development and maintenance requirements |
| Chapter 9 — Data Flow | Determines storage, processing and transmission requirements |
| Chapter 10 — AI | Introduces model development, computation and lifecycle costs |
| Chapter 11 — Energy/Performance | Influences battery, connectivity and hardware requirements |
| Chapter 12 — Cloud | Defines recurring infrastructure, storage and platform costs |
| Chapter 13 — PoC | Demonstrates feasibility without defining the final product cost |

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

 The SSP business model is based on treating the proposed system as a complete **IoT monitoring service**, rather than as an isolated wearable device.

 The economic structure therefore consists of:

 **Initial investment**

 → hardware + deployment \+ integration

 **Recurring operation**

 → connectivity + cloud + storage + processing + support

 **Lifecycle operation**

 → maintenance + security \+ software updates + device replacement

 The proposed architecture supports this model because it separates device functions from centralized platform services and allows fleet management, cloud processing and operational interfaces to scale independently where appropriate.

 At the same time, the analysis demonstrates that a final commercial cost cannot yet be stated with precision. The current project has established the architecture and engineering assumptions, but detailed supplier quotations, production PCB design, certification requirements, manufacturing arrangements, connectivity contracts and operational service levels would be required before a validated commercial TCO could be produced.

 The appropriate economic progression is therefore:

 **Conceptual cost model → Engineering BOM → Prototype cost → Pilot cost → Production cost → Validated TCO**

 The laboratory PoC remains a technical demonstration and is explicitly separated from the commercial product definition.

 The next stage is therefore **Chapter 15 — Testing & Validation**, where the requirements established in Chapter 3 and the technical architecture developed in Chapters 5–13 are converted into measurable verification and validation activities.

 The fundamental evaluation chain becomes:

 **Requirement → Metric → Test → Result → Pass/Fail**

 This provides the final engineering evidence needed to determine whether the proposed SSP design satisfies its stated objectives.

 Chapter 14 is now positioned as the **economic and productization layer** of the design rather than as a second technical-design chapter. The next chapter, **15 — Testing & Validation**, should consequently be built around the requirement-to-test traceability rather than simply listing generic tests.
