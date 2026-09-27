 # 4\. Market / Context Analysis

 ## 4.1 Purpose of the Market and Context Analysis

 The purpose of this chapter is to establish the technological, operational and market context in which SmartSecurePerimeter (SSP) is proposed.

 Chapter 1 established the problem and the SSP concept. Chapter 2 described the users and operational scenarios, while Chapter 3 translated those needs into system requirements. The purpose of Chapter 4 is now to determine what is already available in the relevant technological and operational landscape and to identify the limitations, opportunities and design implications that should influence the subsequent SSP architecture.

 The analysis considers four complementary dimensions:

 1. **Existing operational solutions** for electronic monitoring, perimeter protection and location-based protection.
2. **Available technological approaches** for sensing, positioning, communication, edge processing and cloud services.
3. **Security, privacy and regulatory considerations** associated with systems that process sensitive location and movement information.
4. **Unmet or insufficiently addressed system-level needs** that motivate the proposed SSP architecture.

 The objective is not to claim that SSP invents individual technologies such as GNSS, BLE, geofencing, cloud computing or machine learning. These technologies are already established. Instead, the analysis investigates how they are currently combined and where an integrated architecture such as SSP could provide additional engineering value.

 The resulting reasoning chain is:

 **Existing solutions → Existing capabilities → Current limitations → Design implications → SSP architecture**

 This chapter therefore provides the evidence base for the architecture decisions developed beginning in Chapter 5.

---

 ## 4.2 Market and Application Context

 SSP operates at the intersection of several established technology and application domains:

 - electronic monitoring;
- personal protection;
- perimeter and geofence monitoring;
- connected wearable devices;
- location-based services;
- IoT sensing;
- wireless communication;
- edge computing;
- cloud monitoring;
- intelligent event detection;
- security and privacy engineering.

 These domains are not independent. A practical protection system must combine sensing and positioning with communications, event processing, alert generation, operational interfaces and lifecycle management.

 The Spanish electronic monitoring ecosystem provides a particularly relevant reference because it demonstrates that connected devices can already be used operationally to enforce proximity restrictions and generate alerts. The Spanish telematic monitoring system for judicially imposed proximity restrictions uses a combination of wearable and control devices, BLE, GNSS, cellular communication, motion sensing, proximity detection and centralized monitoring.  Violencia de Género

 This establishes an important baseline for SSP:

 > The fundamental technologies required to construct a connected perimeter-monitoring system are already technically feasible and are already used in operational contexts.

 Consequently, SSP should not be positioned as an invention of these individual technologies. Its contribution must instead be evaluated at the **system integration, intelligence, adaptability, resource management and architecture levels**.

---

 ## 4.3 Existing Operational Solutions

 ### 4.3.1 Telematic electronic monitoring

 Electronic monitoring systems represent one of the closest existing application domains to SSP.

 A representative Spanish system for monitoring judicially imposed proximity restrictions uses:

 - a wearable transmitter;
- BLE communication between the wearable and a control device;
- GNSS positioning;
- cellular communication;
- accelerometer and gyroscope sensing;
- proximity detection;
- device-integrity and tamper monitoring;
- autonomous alert generation;
- centralized monitoring through the COMETA control centre.  Violencia de Género

 The system also provides contingency behavior. For example, the wearable device can establish direct cellular/GNSS communication with the monitoring centre if the BLE connection with the associated control device is lost.  Violencia de Género

 This is significant for SSP because it demonstrates that several requirements identified in Chapter 3 are already operationally justified:

 **Positioning + motion + proximity + communication + tamper detection + alerting + fallback operation**

 However, the existence of these capabilities does not imply that every possible architectural improvement has already been solved. The SSP project therefore investigates how such capabilities can be organized into a more explicitly distributed and adaptive Device–Edge–Cloud architecture.

---

 ### 4.3.2 Integrated risk-management platforms

 Protection systems increasingly extend beyond simple location tracking.

 Spain's VioGén system, for example, integrates information from multiple public institutions, supports risk assessment, monitoring and protection activities, and provides automated notifications. The newer VioGén 2 platform further expands interoperability, risk indicators, algorithm calibration, security and automated notification capabilities.  Ministerio del Interior+1

 The resulting operational concept is broader than:

 **Location → Geofence → Alert**

 It can instead be represented as:

 **Information → Risk assessment → Risk level → Protection measures → Monitoring → Notification**

 This distinction is important for SSP.

 A perimeter-monitoring system that only determines whether a device is inside or outside a predefined zone provides a relatively limited interpretation of the available sensor information. SSP therefore investigates whether location, movement, proximity, device state, communication state and historical context can be combined to produce more informative event assessments.

 The objective is not to replace institutional risk-management systems such as VioGén. SSP is instead conceived as an IoT platform capable of supplying structured sensing, monitoring and event information to authorized operational systems.

---

 ## 4.4 Existing Technology Capabilities

 The technologies relevant to SSP are individually mature enough to support the proposed system concept.

 ### 4.4.1 Positioning

 GNSS provides a well-established mechanism for outdoor positioning and is already used in electronic monitoring systems. The Spanish telematic monitoring system, for example, incorporates multiple satellite-navigation constellations and uses positioning as part of its monitoring and contingency mechanisms.  Violencia de Género

 However, GNSS performance can vary according to environmental conditions. Buildings, urban environments, indoor locations and signal obstruction can affect positioning quality.

 This supports a requirement already established in Chapter 3:

 > SSP should treat positioning as information accompanied by a degree of confidence rather than as an infallible measurement.

 This creates an opportunity for contextual and multi-source positioning techniques to be investigated later.

---

 ### 4.4.2 Motion and inertial sensing

 Accelerometers and gyroscopes are established components of connected wearable and mobile systems.

 Their relevance to SSP extends beyond simple activity measurement. Motion information can provide contextual information about:

 - whether the device is moving;
- whether a position change is plausible;
- whether the wearer is stationary or travelling;
- whether a sudden movement pattern has occurred;
- whether a positioning transition is consistent with physical movement.

 Motion sensing can therefore contribute to event interpretation and adaptive monitoring.

 The market analysis consequently supports the SSP requirement for combining **position and motion information**, rather than treating position as the only relevant signal.

---

 ### 4.4.3 BLE and proximity detection

 Bluetooth Low Energy is already used for short-range communication and device association in electronic monitoring systems. The Spanish monitoring architecture uses BLE to associate the wearable transmitter with its control device and also uses BLE-based detection in proximity-related operation.  Violencia de Género

 This demonstrates that short-range proximity information can complement geographical positioning.

 A useful distinction for SSP is therefore:

 **GNSS → geographical position**

 **BLE/proximity → local relative presence**

 The two forms of information can provide different evidence about a potential event.

---

 ### 4.4.4 Cellular communication

 Cellular communication provides wide-area connectivity for devices that cannot rely on local infrastructure.

 Existing electronic monitoring systems already use cellular communication for data, voice and alert-related functions.  Violencia de Género

 For SSP, cellular communication is therefore a candidate for wide-area connectivity, but its use must be evaluated against:

 - energy consumption;
- coverage;
- latency;
- operational availability;
- communication cost;
- device size;
- fallback requirements.

 The final cellular technology should consequently be selected in Chapter 7 rather than assumed at this stage.

---

 ### 4.4.5 Edge computing

 Edge computing provides the possibility of processing information closer to where it is generated.

 This is particularly relevant to SSP because some events may require rapid response or may contain information that should not automatically be transmitted in its raw form.

 Potential edge functions include:

 - sensor fusion;
- local event filtering;
- geofence evaluation;
- trajectory estimation;
- anomaly detection;
- risk assessment;
- communication prioritization;
- local fallback operation.

 The market context therefore supports the Device–Edge–Cloud concept introduced in Chapter 1, although the exact allocation of functions remains an engineering decision for Chapter 5 onward.

---

 ### 4.4.6 Cloud computing

 Cloud platforms provide capabilities that are difficult to reproduce efficiently on constrained devices, including:

 - long-term storage;
- fleet management;
- large-scale analytics;
- centralized configuration;
- historical analysis;
- model training;
- model management;
- dashboard services;
- integration with external systems.

 VioGén 2 provides an example of how centralized information integration and automated notification can support large-scale operational processes. The platform has been designed to improve interoperability and accommodate future software and application evolution.  Ministerio del Interior

 For SSP, cloud computing therefore remains important, but the market analysis reinforces the principle that **not every function needs to be performed in the cloud**.

---

 ## 4.5 Existing Approaches to Geofencing and Protection Zones

 Geofencing is a well-established mechanism for translating geographic information into operational rules.

 A simple implementation can define:

 - inclusion zones;
- exclusion zones;
- permitted areas;
- restricted areas;
- proximity thresholds;
- entry conditions;
- exit conditions.

 Existing GPS-monitoring research has examined the use of GPS technology to enforce court-mandated no-contact conditions and geographic exclusion/inclusion zones.  National Institute of Justice+1

 This confirms the fundamental validity of geographical rules for protection applications.

 However, a static geofence does not necessarily capture the full context of an event.

 For example, the following situations may not have equivalent operational significance:

 **Situation A:**\
 A device briefly crosses a boundary while travelling away from the protected area.

 **Situation B:**\
 A device approaches a protected area at increasing speed.

 **Situation C:**\
 A device remains close to a boundary for an extended period.

 **Situation D:**\
 A device approaches a protected device while positioning confidence is poor.

 A more advanced SSP architecture can therefore investigate contextual event interpretation rather than treating every geographical boundary crossing as identical.

 This provides one of the motivations for the predictive and adaptive functions proposed in SSP.

---

 ## 4.6 Existing Limitations and System-Level Gaps

 The market analysis does not imply that existing systems are technically inadequate. Rather, it identifies areas where SSP can investigate alternative architectural approaches.

 ### 4.6.1 Predominantly event-oriented operation

 Many monitoring systems are naturally organized around detecting a predefined condition and generating an alert.

 This is appropriate for clearly defined operational rules, but it can provide limited contextual interpretation when several signals must be considered together.

 SSP therefore proposes that relevant information can be combined before an operational decision is generated.

---

 ### 4.6.2 Limited separation between sensing, decision and communication

 A conventional connected-device architecture can conceptually be represented as:

 **Sense → Transmit → Process → Alert**

 SSP investigates a more distributed approach:

 **Sense → Local interpretation → Edge assessment → Cloud analysis → Operational response**

 The purpose is not to increase architectural complexity unnecessarily. Instead, processing should be placed where it provides a measurable benefit in latency, energy consumption, privacy, resilience or scalability.

---

 ### 4.6.3 Dependence on connectivity

 Wide-area connectivity is essential for many monitoring applications, but communication can become temporarily unavailable.

 Existing operational systems already demonstrate the importance of contingency behavior. The Spanish telematic monitoring system, for example, includes autonomous alert functionality and contingency communication behavior when parts of the normal communication chain become unavailable.  Violencia de Género

 SSP therefore treats communication loss as a normal engineering condition that must be explicitly designed for rather than as an exceptional situation that can simply be ignored.

 This supports the Chapter 3 requirements for:

 - local decision capability;
- event preservation;
- graceful degradation;
- communication-failure detection;
- recovery.

---

         ### 4.6.4 Energy-resource constraints

 Wearable and autonomous devices operate under physical energy constraints.

 Continuous high-rate sensing, positioning and wide-area communication can increase energy consumption substantially. Consequently, a monitoring system cannot assume that every sensing and communication function should operate at maximum intensity continuously.

 This motivates SSP's adaptive-energy concept:

 **Context/risk → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

 The purpose is to investigate whether non-critical operating states can consume fewer resources while critical functions remain available.

---

 ### 4.6.5 Privacy and sensitive-data exposure

 Location and movement data can reveal highly sensitive information.

 The market context therefore requires privacy to be treated as an architectural property rather than solely as a database or user-interface issue.

 NIST's Privacy Framework provides a structured approach for managing privacy risk, while IoT cybersecurity guidance emphasizes that security capabilities should be considered at the device and system levels.  NIST+1

 This supports the SSP principle that data should be processed and transmitted according to operational necessity.

 For example:

 **Normal operation → minimum necessary information**

 **Elevated condition → additional contextual information**

 **Critical event → information necessary for authorized response**

 The precise implementation of this principle will be developed in Chapters 5, 7, 9 and 12.

---

 ### 4.6.6 Security and lifecycle management

 IoT devices introduce security concerns at both the device and infrastructure levels.

 NIST identifies device capabilities including device identification, configuration, data protection, logical access control, software update capability and cybersecurity-state awareness as important components of an IoT cybersecurity baseline.  NIST Pages+1

 Similarly, ETSI EN 303 645 establishes baseline cybersecurity provisions for connected IoT devices and emphasizes security and data-protection considerations throughout product development. The current published version is EN 303 645 V3.1.3 (2024).  ETSI+1

 For SSP, these considerations reinforce the need to address:

  This motivates SSP's adaptive-energy concept:

 **Context/risk → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

---

   The market context therefore requires privacy to be treated as an architectural property rather than solely as a database or user-interface issue.

 NIST's Privacy Framework provides a structured approach for managing privacy risk, while IoT cybersecurity guidance emphasizes that security capabilities should be considered at the device and system levels.

   **Normal operation → minimum necessary information**

---

 ### 4.6.6 Security and lifecycle management

   - secure device identity;
- authenticated communication;
- protected credentials;
- secure software updates;
- configuration security;
- access control;
- lifecycle management;
- vulnerability management.

 These are therefore not optional additions to the architecture. They form part of the system constraints already captured in Chapter 3.

---

 ## 4.7 Technology Alternatives Relevant to SSP

 Several technological alternatives can satisfy individual SSP functions.

 | Function | Candidate approaches | Main trade-offs |
| --- | --- | --- |
| Outdoor positioning | GNSS, assisted GNSS | Accuracy, availability, energy |
| Local proximity | BLE, other short-range radio | Range, energy, environmental sensitivity |
| Motion sensing | Accelerometer, gyroscope, sensor fusion | Information quality vs. processing/energy |
| Local connectivity | BLE, Wi-Fi | Range, infrastructure, energy |
| Wide-area connectivity | Cellular, LPWAN alternatives | Coverage, bandwidth, latency, energy, cost |
| Local processing | MCU, embedded processor, mobile/edge device | Compute capability vs. energy |
| Edge processing | Smartphone, gateway, local server | Connectivity, deployment complexity |
| Cloud processing | Public/private cloud infrastructure | Scalability, cost, connectivity dependency |
| Event detection | Rule-based logic, statistical methods, ML | Interpretability, adaptability, data requirements |
| Position/risk interpretation | Static geofencing, contextual/predictive analysis | Complexity vs. contextual capability |

At this stage, the table is deliberately a **technology landscape rather than a selection table**.

 The final selections should be made only after the architecture is defined and the alternatives can be evaluated against the requirements.

---

 ## 4.8 Security, Privacy and Regulatory Context

 SSP may operate in environments involving sensitive personal and location information. The precise legal obligations will depend on the deployment jurisdiction, application and organizational role.

 Nevertheless, the market and technology context establishes several general design principles.

 ### Security

 IoT cybersecurity should be considered from the device through the cloud service.

 NIST's IoT cybersecurity guidance identifies device capabilities and manufacturer-support activities that help organizations establish security requirements for IoT deployments.  NIST+1

 Relevant SSP implications include:

 - unique device identity;
- protected configuration;
- secure communications;
- controlled access;
- secure software updates;
- device-state awareness;
- lifecycle management.

 ### Privacy

---

 ## 4.8 Security, Privacy and Regulatory Context

 SSP may operate in environments involving sensitive personal and location information. The precise legal obligations will depend on the deployment jurisdiction, application and organizational role.

  ### Security

  NIST's IoT cybersecurity guidance identifies device capabilities and manufacturer-support activities that help organizations establish security requirements for IoT deployments.

 The NIST Privacy Framework provides a risk-management approach for identifying and managing privacy risks rather than treating privacy solely as a technical encryption problem.  NIST

 For SSP, privacy therefore affects:

 - what data is collected;
- where it is processed;
- what is transmitted;
- who can access it;
- how long it is retained;
- how events are audited.

 ### Regulatory context

 For deployments involving judicial monitoring, victim protection, schools or other sensitive environments, the final system would require a deployment-specific legal and regulatory assessment.

 The design project therefore does not assume that a technically functional SSP system is automatically suitable for operational deployment. Legal authorization, data-protection requirements, institutional responsibilities and deployment-specific certification would have to be addressed during product development.

---

 ## 4.9 Benchmarking Framework for SSP

 A meaningful comparison between SSP and existing approaches should not be based simply on the number of features provided.

 The systems should instead be compared according to architectural and operational capabilities.

 The proposed benchmark dimensions are:

 | Dimension | Questions |
| --- | --- |
| Sensing | Which physical/contextual signals are available? |
| Positioning | How is location obtained and how is uncertainty handled? |
| Proximity | Can local relative presence be detected? |
| Geofencing | Are inclusion/exclusion rules supported? |
| Motion intelligence | Is movement interpreted beyond raw sensing? |
| Event detection | How are relevant events generated? |
| Risk/context | Can multiple information sources influence event severity? |
| Edge processing | Can decisions be made locally? |
| Cloud processing | What centralized capabilities exist? |
| Communication resilience | What happens when connectivity is lost? |
| Energy management | Can monitoring intensity adapt to context? |
| Privacy | Can data collection/transmission be minimized? |
| Security | Are device, communication and lifecycle controls provided? |
| Alerting | How are events delivered to authorized users? |
| Scalability | Can the solution support larger deployments? |
| Fleet management | Can devices and configurations be managed centrally? |
| AI/analytics | Are predictive or learning-based capabilities supported? |
| Interoperability | Can the system exchange information with other platforms? |
| Operational usability | Does the system support real operational workflows? |

This framework will be used to structure the detailed benchmark of representative solutions as the project develops.

 Importantly, the benchmark should distinguish between:

 **Documented capability**

 and

 **SSP proposed capability**

 so that the project does not incorrectly imply that an existing system lacks a capability simply because it is not publicly documented.

---

 ## 4.10 Market Gap Relevant to SSP

 The market analysis identifies a number of capabilities that already exist independently:

 **Positioning**

 **Geofencing**

 **BLE/proximity**

 **Motion sensing**

 **Cellular communication**

 **Tamper detection**

 **Centralized monitoring**

 **Automated alerts**

 **Risk assessment**

 **Cloud information management**

 The proposed SSP opportunity therefore does not depend on claiming that these technologies are individually absent from the market.

 Instead, the project investigates their integration into a common architecture in which:

 - device sensing provides contextual information;
- local processing reduces unnecessary transmission;
- edge processing provides rapid local interpretation;
- cloud processing provides system-wide intelligence;
- communication behavior can adapt to event significance;
- energy consumption can adapt to operational state;
- privacy can influence data-processing location and transmission;
- communication failures can trigger defined local fallback behavior;
- centralized management can support scalable deployment.

 The proposed conceptual distinction is therefore:

 **Existing approach:**

 **Sense → Communicate → Central monitoring → Alert**

 **SSP investigation:**

 **Sense → Interpret → Assess → Predict → Select information → Communicate → Act → Learn**

 This should be understood as an **architectural research/design objective**, not as a claim that every existing commercial or institutional system follows the first model exclusively.

---

 ## 4.11 SSP Differentiation

 Based on the current context analysis, SSP differentiation should be defined at the system level.

 The project does not claim novelty for:

 - GNSS;
- BLE;
- cellular communication;
- accelerometers;
- gyroscopes;
- geofencing;
- cloud computing;
- machine learning;
- wearable monitoring.

 Instead, SSP proposes to investigate an integrated architecture in which these capabilities can interact according to explicit system policies.

 The principal areas of differentiation to be evaluated are:

 ### 1\. Distributed intelligence

 Processing can be distributed between Device, Edge and Cloud according to latency, energy, privacy, connectivity and computational requirements.

 ### 2\. Adaptive monitoring

 Sensing and communication intensity can change according to context, system state and operational significance.

 ### 3\. Context-aware event interpretation

 Position, motion, proximity, confidence and device state can be considered together rather than treating every raw event identically.

 ### 4\. Resilient operation

 Selected functions can continue locally during temporary communication or cloud disruption.

 ### 5\. Privacy-aware information flow

 The system can distinguish between information required locally and information that must be transmitted to other layers.

 ### 6\. Lifecycle-oriented security

 Security is considered from device identity and communication through software updates, configuration and cloud access.

 ### 7\. Scalable architecture

 The same conceptual architecture can support small deployments and larger device fleets without requiring a fundamental redesign.

 These characteristics constitute **design hypotheses to be engineered and evaluated**, rather than proven advantages at this stage.

---

 ## 4.12 Design Implications for SSP

 The market and technology analysis produces several implications for the next stage of the project.

 ### DI-01 — Multi-source sensing should be considered

 Position should not necessarily be treated as an isolated measurement. GNSS, motion, proximity and other contextual signals should be evaluated as potentially complementary information sources.

 ### DI-02 — Position uncertainty should influence decisions

 The architecture should be capable of distinguishing high-confidence positioning from uncertain positioning.

 ### DI-03 — Processing should not automatically be centralized

 Functions should be assigned to Device, Edge or Cloud according to measurable requirements.

 ### DI-04 — Communication should be policy-aware

 Not all data requires identical transmission priority or frequency.

 ### DI-05 — Connectivity loss must be explicitly handled

 The architecture should define local and edge fallback behavior before the communication technologies are selected.

 ### DI-06 — Energy management should be integrated with system logic

 Power management should not be treated as an isolated hardware function. Monitoring requirements and operational state should influence resource consumption.

 ### DI-07 — Privacy should influence architecture

 Data minimization and local processing should be considered when deciding what information crosses system boundaries.

 ### DI-08 — Security must extend to the device

 Device identity, secure configuration, protected communication and software-update mechanisms must be considered before hardware and software are finalized.

 ### DI-09 — AI requires measurable justification

 Machine learning should only be introduced where it provides a measurable benefit over an appropriate deterministic approach.

 ### DI-10 — Scalability should be designed from the beginning

 Device registration, event ingestion, storage, monitoring and cloud processing should be capable of scaling without redesigning the fundamental system structure.

---

 ## 4.13 Relationship Between Market Analysis and the SSP Requirements

 The market analysis provides additional justification for several requirements defined in Chapter 3.

 | Market/context observation | SSP requirement implication |
| --- | --- |
| Existing systems use GNSS and geofencing | Positioning and geographical monitoring remain core requirements |
| BLE is used for device association and proximity | Proximity monitoring should be supported |
| Existing systems incorporate contingency behavior | Communication-loss and local fallback requirements are necessary |
| Centralized risk-management platforms are established | SSP should support cloud integration and system-wide analysis |
| Positioning can vary with environmental conditions | Position confidence should be represented |
| Wearable devices have energy constraints | Adaptive energy management is required |
| Location information is sensitive | Data minimization and privacy-aware processing are required |
| IoT devices introduce lifecycle security requirements | Device identity, authentication and secure updates are required |
| Large operational systems require interoperability | SSP should provide structured APIs and integration mechanisms |
| Predictive processing is increasingly used in information systems | AI should be evaluated where it provides measurable benefit |

This confirms that the requirements of Chapter 3 are not arbitrary feature requests. They are grounded in the operational and technological context established by the existing landscape.

---

 ## 4.14 Limitations of the Market Analysis

 The analysis has several limitations that should be explicitly recognized.

 First, public documentation does not provide complete technical information for every commercial or institutional monitoring system. The absence of a publicly documented capability should therefore not be interpreted as proof that the capability does not exist.

 Second, operational systems are often governed by legal, institutional and security constraints that limit the amount of technical information that can be publicly disclosed.

 Third, the SSP project is a design study rather than a full commercial market-validation exercise. Detailed supplier pricing, procurement conditions, certification costs and contractual service conditions will therefore be addressed later where appropriate.

 Fourth, the technologies and standards relevant to IoT systems continue to evolve. Component and communication selections should consequently be validated against current technical documentation during the detailed engineering stages.

 Finally, the market analysis identifies **design opportunities**, not guaranteed performance improvements. Any claimed SSP advantage must ultimately be demonstrated through the quantitative requirements and validation methodology established in Chapters 3 and 15.

---

 ## 4.15 Chapter 4 Conclusion

 The market and technology landscape demonstrates that the principal building blocks required for SSP already exist.

 Operational electronic monitoring systems demonstrate the feasibility of combining wearable devices, BLE, GNSS, cellular communication, motion sensing, proximity detection, tamper monitoring and centralized alerts.  Violencia de Género

 Large-scale protection and risk-management platforms demonstrate the value of integrating information, risk assessment, monitoring and automated notification. VioGén 2, for example, has expanded interoperability, risk assessment capabilities, security and automated notifications within a broader institutional platform.  Ministerio del Interior

 ### DI-02 — Position uncertainty should influence decisions

 At the same time, IoT cybersecurity and privacy frameworks reinforce the need to consider device security, lifecycle management, data protection and privacy throughout the system rather than only at the cloud application layer.  NIST+1

 The resulting conclusion is therefore not that SSP must replace existing monitoring technologies. Rather, the project investigates whether these established technologies can be organized into a coherent architecture with:

 **Distributed intelligence**

 **Adaptive monitoring**

 **Context-aware event interpretation**

 **Resilient operation**

 **Privacy-aware information flow**

 **Security by design**

 **Scalable system management**

 The next chapter converts these findings and the requirements established in Chapter 3 into the **first explicit SSP engineering design: the overall IoT architecture**.

 The design progression is therefore:

 **Problem → Users and scenarios → Requirements → Market/context → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Validation**

 ### References

 **\[1\]** Ministerio del Interior, Gobierno de España, _Interior diseña un nuevo modelo de respuesta policial a la violencia de género_, 15 January 2025.  Official source

 **\[2\]** Delegación del Gobierno contra la Violencia de Género, Gobierno de España, _Dispositivos de control telemático de medidas y penas de alejamiento_.  Official source

 **\[3\]** Ministerio del Interior, Gobierno de España, _Sistema VioGén 2_.  Official source

 **\[4\]** National Institute of Justice, U.S. Department of Justice, _GPS Monitoring Technologies and Domestic Violence: An Evaluation Study_, 2012.  Official source

 **\[5\]** National Institute of Standards and Technology, _IoT Device Cybersecurity Capability Core Baseline_, NISTIR 8259A, 2020.  Official source

 **\[6\]** National Institute of Standards and Technology, _Privacy Framework_.  Official source

 **\[7\]** ETSI, _EN 303 645 V3.1.3 — Cyber Security for Consumer Internet of Things: Baseline Requirements_, 2024.  Official source
