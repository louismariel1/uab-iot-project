 ## 1\. Introduction

 ### 1.1 Definition of SmartSecurePerimeter

 SmartSecurePerimeter (SSP) is an efficient and secure IoT perimeter-monitoring solution designed to protect secure perimeters, sensitive environments such as schools, and victims who require protection from known offenders.

 SSP addresses common limitations of existing perimeter-monitoring solutions through the integrated use of intelligent device sensing, adaptive energy management, positioning and motion intelligence, predictive edge processing, privacy-aware communication, cloud-based intelligence and scalable operational management.

 The solution is designed to provide secure, energy-efficient, privacy-aware and resilient monitoring across three complementary layers: **Device, Edge and Cloud**. Its performance is evaluated using measurable technical, energy, security, privacy, performance and economic KPIs. A Proof of Concept (PoC) demonstrates the proposed architecture and its technical feasibility in representative real-world scenarios.

 ### 1.2 Motivation and Context

 The increasing requirements placed on electronic monitoring and perimeter-protection systems create a need for solutions that can combine sensing, communication, intelligence, security, privacy and energy management more effectively. Existing systems already provide important capabilities such as positioning, geofencing, communication, alert generation and centralized monitoring. However, these capabilities are not necessarily integrated into a single architecture in which processing, communication and resource consumption can adapt to the current context and risk level.

 The need for continued modernization is also reflected in public-sector protection systems. In Spain, the Ministry of the Interior has developed **VioGén 2** as a new technological platform for the comprehensive management of gender-based violence cases. The modernization introduced improvements including enhanced risk assessment, greater interoperability with institutional information systems, additional security measures and more advanced automated notifications. The Ministry explained that the evolution was intended to respond to changing operational and technological requirements and to provide a platform capable of further development \[1\].

 This context supports the broader motivation for SSP: to investigate how an integrated IoT architecture can combine established technologies with distributed intelligence and adaptive resource management to provide more efficient, secure, privacy-aware and resilient perimeter monitoring.

 ### 1.3 Existing Solutions and Current State

 Electronic monitoring, perimeter protection and location-based protection are established application areas for IoT and connected-device technologies. Existing solutions combine different combinations of positioning, wireless communication, motion sensing, proximity detection, geofencing, tamper detection, automated alerts and centralized monitoring. Their implementation varies according to the application, but the general operational principle is to detect a relevant condition, communicate the information to a monitoring system and initiate an appropriate response.

 A representative example is the Spanish telematic monitoring system used to enforce judicially imposed proximity restrictions in cases of gender-based and sexual violence. The system combines a wearable transmitter with a control device. The wearable transmitter communicates with the control device using Bluetooth Low Energy (BLE), while GNSS and cellular communication provide positioning and communication capabilities. The control device additionally incorporates technologies including GNSS, cellular connectivity, Wi-Fi scanning, an accelerometer, a gyroscope and proximity sensing \[2\].

 A simplified representation of the processing and communication chain is:

 **Monitored person → Wearable transmitter → BLE → Control device → Positioning / sensors / cellular communication → Monitoring centre → Alert / operational response**

 For proximity protection, the interaction can additionally be represented as:

 **Monitored person → Wearable device → Proximity detection → Protected-person device → Alert → Monitoring / protection response**

 This type of solution demonstrates that several capabilities relevant to SSP are already operationally feasible, including wearable sensing, BLE communication, GNSS positioning, cellular connectivity, motion sensing, proximity detection, tamper-related monitoring and centralized alerts \[2\].

 At the broader operational level, protection systems are also incorporating increasingly sophisticated information management and risk assessment. Spain's VioGén system integrates information from multiple institutions and supports risk assessment, monitoring, protection measures and automated notifications. VioGén 2 further develops these capabilities through additional risk indicators, improved risk-assessment procedures, greater interoperability and enhanced security and notification mechanisms \[3\].

 Its high-level operational chain can be represented as:

 **Case information → Data integration → Risk assessment → Risk level → Protection measures → Monitoring → Notification / intervention**

 These examples demonstrate that the individual technologies relevant to SSP are not themselves new. The intended contribution of SSP is instead the **integration and organization of these capabilities within a unified Device–Edge–Cloud architecture**, with explicit consideration of energy, privacy, security, resilience, performance and scalability.

 The resulting SSP information and decision chain can be summarized as:

 **Sensing → Local processing → Position / motion intelligence → Risk assessment → Adaptive communication → Edge prediction → Cloud intelligence → Alert / decision / action**

 A detailed benchmark of existing solutions and their capabilities will be developed later in the report. This benchmark will provide the basis for identifying specific technical gaps and defining the requirements that SSP must satisfy.

 ### 1.4 SSP Design Approach

 The fundamental design principle of SSP is to assign each function to the system layer where it can be performed most effectively while maintaining a coherent end-to-end architecture.

 At the **Device layer**, SSP combines positioning, motion sensing, local processing, tamper detection, secure communication and adaptive power management. The device is therefore intended not merely to collect and transmit data, but also to interpret relevant local information and determine which events require further processing or communication.

 At the **Edge layer**, SSP introduces an intermediate intelligence layer between the monitored devices and the cloud. The edge can combine information from devices, perform predictive geofencing and risk assessment, reduce unnecessary transmission of sensitive or repetitive information, and maintain selected monitoring and decision functions during temporary network or cloud disruption.

 At the **Cloud layer**, SSP provides system-wide capabilities for historical analysis, fleet management, model management, policy configuration, operational dashboards and scalable data processing. The cloud complements rather than replaces the intelligence available at the device and edge.

 The overall design philosophy can therefore be represented as:

 **Sense → Interpret → Assess → Predict → Decide → Communicate → Act → Learn**

 This architecture is intended to move perimeter monitoring from a predominantly reactive model toward a more adaptive system in which sensing, communication, energy consumption, privacy and security can respond to context and risk.

 ### 1.5 SSP Differentiation

 The individual technologies incorporated into SSP are not claimed to be new in isolation. Existing solutions already demonstrate capabilities such as multi-modal positioning, geofencing, tamper detection, power-management mechanisms, centralized monitoring and automated notification.

 The intended differentiation of SSP lies at the **system-architecture and integration level**. SSP combines intelligent device sensing, adaptive energy management, positioning and motion intelligence, predictive edge processing, privacy-aware communication and cloud intelligence within a coherent Device–Edge–Cloud architecture.

 The architecture also establishes explicit relationships between these functions. For example, positioning confidence can influence monitoring intensity; detected risk can influence sensing and communication policies; privacy requirements can influence what information is transmitted; and cloud intelligence can subsequently improve policies and models deployed at the edge and device.

 Thus, SSP is not dependent on claiming that each individual technology is novel. Its engineering contribution is the design and evaluation of an integrated system in which these technologies cooperate and their interactions are explicitly managed.

 The detailed market and technology analysis presented later in the report will benchmark SSP against representative existing solutions and establish more precisely the differences in functionality, architecture, performance objectives and operational model.

 ### 1.6 Intended Application Domains

 SSP is designed as a configurable perimeter-monitoring platform rather than as a solution restricted to a single application.

 Potential application domains include:

 - **Secure-perimeter protection:** monitoring defined exclusion or inclusion zones around sensitive facilities or restricted areas.
- **Sensitive environments:** protecting locations such as schools and other environments where rapid detection of defined proximity or perimeter events may be required.
- **Victim protection:** monitoring protection zones associated with a person at risk and generating appropriate alerts when a monitored individual approaches or enters a restricted zone.
- **Community and judicial monitoring:** supporting authorized monitoring scenarios involving individuals subject to legally defined geographic restrictions.

 The same underlying architecture can support these applications by adapting policies, geofences, risk thresholds, notification rules and operational workflows rather than redesigning the complete IoT platform.

 ### 1.7 Design Philosophy

 SSP follows four fundamental design principles.

 **1\. Distributed intelligence.**\
 Processing should take place at the device, edge or cloud according to latency, energy, privacy, connectivity and computational requirements.

 **2\. Adaptive monitoring.**\
 The system should be capable of adapting sensing, processing and communication behavior according to context, risk and system state rather than operating with identical resource requirements under all conditions.

 **3\. Security and privacy by design.**\
 Security and privacy should be considered throughout sensing, processing, communication, storage, access control and system management rather than being added only at the application layer.

 **4\. Measurable engineering.**\
 Major design decisions and proposed improvements should be supported by measurable KPIs covering positioning, detection, prediction, latency, energy consumption, battery autonomy, communication, privacy, security, availability, scalability and cost.

 These principles provide the foundation for the subsequent SSP design. The following chapters translate them into detailed requirements, system architecture, hardware and communication design, embedded and cloud software, intelligence functions, PoC implementation, validation, scalability and economic analysis.

 ### References

 **\[1\]** Ministerio del Interior, Gobierno de España, _Interior diseña un nuevo modelo de respuesta policial a la violencia de género_, 15 January 2025.  Official source

 **\[2\]** Delegación del Gobierno contra la Violencia de Género, Gobierno de España, _Dispositivos de control telemático de medidas y penas de alejamiento_.  Official source

 **\[3\]** Ministerio del Interior, Gobierno de España, _Sistema VioGén 2_.  Official source

 This version gives Chapter 1 a clearer progression:

 **Definition → Motivation → Existing State → Design Approach → Differentiation → Applications → Design Philosophy**

 It also avoids prematurely making a strong “SSP is the first” market claim. That claim, if warranted, can be addressed later after we complete the systematic benchmark in the market/context analysis.
