 # Chapter 7. SSP Communication Architecture - Plan
 
 ## 7.1 Communication requirements

 Translate Chapter 3 requirements and Chapter 5 architectural decisions into communication-specific requirements:

 - range
- latency
- bandwidth
- energy
- reliability
- availability
- security
- scalability
- cost
- fallback operation

 ## 7.2 Device-level communication

 Define communication occurring within or immediately around the SSP device:

 - sensor/MCU interfaces
- internal interfaces
- local wireless interfaces
- distinction between sensor buses and external communications

 ## 7.3 Device → Edge communication

 This is the most important link for the wearable architecture.

 We will evaluate:

 - BLE
- Wi-Fi
- direct cellular
- other short-range options

 The architectural decision will be based on the Chapter 5 assumption that the **Mobile/Edge layer is an important local intelligence and connectivity point**.

 ## 7.4 Edge → Cloud communication

 Define the wide-area communication path:

 - cellular as the primary candidate
- IP connectivity
- secure application-layer communication
- event prioritization
- intermittent connectivity behavior

 ## 7.5 Cloud → User communication

 Define how operators receive:

 - status
- events
- alerts
- acknowledgements
- configuration changes

 This will primarily be an application/API communication problem rather than a new radio technology decision.

 ## 7.6 BLE / Wi-Fi / cellular / LoRa / other candidates

 Provide the technology landscape and explain why each candidate is or is not appropriate.

 ### 7.7 WBAN / WPAN / WLAN / LPWAN considerations

 Map the technologies to networking categories and explain the implications for SSP.

 ### 7.8 Protocol comparison

 Compare candidates against:

 - range
- bandwidth
- latency
- energy
- infrastructure
- reliability
- security
- cost
- mobility

 ## 7.9 Selected communication architecture

 Freeze the communication design.

 The proposed baseline is:

 **SSP Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ User**

 with Wi-Fi available to the Mobile/Edge layer where appropriate, but **not as the fundamental protection link**.

 ## 7.10 Security

 Define communication security principles:

 - mutual/device authentication
- encryption
- integrity
- credential/key management
- replay protection
- secure provisioning
- application/API security

 ## 7.11 Communication failure modes

 Define what happens when:

 - BLE is lost
- cellular connectivity is lost
- cloud connectivity is lost
- Mobile/Edge fails
- communication quality degrades
- communication is restored

 The key principle will be:

 > **Communication failure must degrade communication capability before it degrades protection capability.**

 # Chapter 7. SSP Communication Architecture

 ## 7.1 Purpose of the Communication Design

 Chapter 5 established the SSP Device–Edge/Mobile–Cloud architecture, while Chapter 6 translated that architecture into the physical and electronic capabilities of the SSP device.

 The purpose of this chapter is to define how information shall move between those architectural layers.

 The communication architecture must therefore answer:

 > **How should SSP devices, Edge/Mobile systems, Cloud services and authorized users exchange information so that the system requirements can be satisfied with appropriate latency, energy consumption, reliability, security and resilience?**

 Communication is not treated as an isolated networking problem.

 Within SSP, communication directly affects:

 - battery autonomy;
- event latency;
- local decision capability;
- privacy;
- reliability;
- scalability;
- security;
- operational continuity;
- total system cost.

 The communication design progression is therefore:

 **Requirements → Communication constraints → Technology candidates → Network roles → Protocol architecture → Security → Failure behavior → Selected communication baseline → Verification**

 The principal communication architecture selected in this chapter is:

 **SSP Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ Authorized User**

 Wi-Fi may be used by the Mobile/Edge layer where appropriate, but it is not established as the fundamental protection link between the wearable SSP device and the wider system.

---

 # 7.2 Communication Design Objectives

 The SSP communication architecture shall satisfy the following objectives.

 ### CO-01 — Appropriate range

 Communication technologies shall provide sufficient coverage for their intended architectural role.

 ### CO-02 — Appropriate latency

 Critical events shall be capable of reaching the next required processing or response layer within the latency limits established by the system requirements.

 ### CO-03 — Energy efficiency

 Communication shall consume energy proportionally to operational need and shall not unnecessarily reduce device autonomy.

 ### CO-04 — Reliability

 The architecture shall provide defined behavior during packet loss, link interruption, degraded connectivity and network failure.

 ### CO-05 — Security

 Communication shall provide appropriate authentication, confidentiality, integrity and protection against unauthorized access.

 ### CO-06 — Scalability

 The communication architecture shall support progression from a small proof-of-concept deployment to larger multi-device deployments.

 ### CO-07 — Data minimization

 Only information required by the receiving layer should normally cross a communication boundary.

 ### CO-08 — Prioritization

 Critical information shall receive higher communication priority than routine information.

 ### CO-09 — Mobility support

 The communication architecture shall accommodate movement of wearable devices and changes in local connectivity.

 ### CO-10 — Interoperability

 The architecture should use established communication standards and interfaces where practical to reduce unnecessary technological dependence.

 ### CO-11 — Resilience

 Temporary communication failure shall result in controlled degradation and buffering rather than immediate loss of protection functionality.

 ### CO-12 — Maintainability

 Communication mechanisms shall support configuration, diagnostics, updates and lifecycle management.

 These objectives translate the requirements from Chapters 3–6 into communication-specific engineering constraints.

---

 # 7.3 Communication Requirements

 The principal communication requirements can be summarized as follows.

 | Requirement | SSP implication |
| --- | --- |
| Short-range device interaction | Low-power local wireless communication is required |
| Device–Edge connectivity | Wearable must communicate with Mobile/Edge |
| Wide-area operation | Mobile/Edge requires wide-area IP connectivity |
| Critical-event delivery | Priority communication path required |
| Battery autonomy | Communication duty cycle must be controlled |
| Connectivity disruption | Local buffering and fallback required |
| Privacy | Raw data should not automatically be transmitted |
| Security | Authenticated and protected communication required |
| Fleet operation | Communication architecture must scale |
| Remote management | Configuration and status communication required |
| Event synchronization | Store-and-forward behavior required |
| Mobility | Architecture must tolerate changing network conditions |
| Operational monitoring | Status and health messages required |
| Cloud integration | Standard IP/application interfaces required |

These requirements do not imply that one technology should provide every communication function.

 The architecture deliberately separates local, wide-area and application-level communication roles.

---

 # 7.4 Communication Architecture Boundaries

 SSP contains four principal communication boundaries.

 ### Boundary A — Internal Device Communication

 This includes communication between:

 - sensors;
- MCU/SoC;
- GNSS subsystem;
- storage;
- security hardware;
- radios;
- power-management components.

 These interfaces are primarily hardware and embedded-system interfaces.

 ### Boundary B — Device ↔ Edge/Mobile

 This is the principal local wireless communication path for the wearable architecture.

 Its primary purpose is to connect the constrained SSP device with a more capable local processing platform.

 ### Boundary C — Edge/Mobile ↔ Cloud

 This provides wide-area communication between the local intelligence layer and centralized SSP services.

 ### Boundary D — Cloud ↔ Authorized User/System

 This provides application-level access to:

 - alerts;
- events;
- dashboards;
- configuration;
- reports;
- acknowledgements;
- management functions.

 The communication technologies appropriate to each boundary are not necessarily the same.

---

 # 7.5 Communication Architecture Overview

 The initial communication architecture is:

```
                         ┌───────────────────────┐
                         │         CLOUD         │
                         │                       │
                         │ APIs • Storage        │
                         │ Analytics • Policies │
                         │ Fleet Management      │
                         └───────────▲───────────┘
                                     │
                              Secure IP / API
                                     │
                              Cellular / Wi-Fi
                                     │
                         ┌───────────┴───────────┐
                         │     MOBILE / EDGE     │
                         │                       │
                         │ Fusion • Risk         │
                         │ Prediction • Events   │
                         │ Local Storage         │
                         │ Communication Control │
                         └───────────▲───────────┘
                                     │
                                  BLE
                                     │
                  ┌──────────────────┼──────────────────┐
                  │                  │                  │
            ┌─────┴─────┐      ┌─────┴─────┐      ┌─────┴─────┐
            │  SSP       │      │  SSP       │      │  SSP       │
            │ Device 1   │      │ Device 2   │      │ Device N   │
            │            │      │            │      │            │
            │ Sensors    │      │ Sensors    │      │ Sensors    │
            │ MCU        │      │ MCU        │      │ MCU        │
            │ Local      │      │ Local      │      │ Local      │
            │ Events     │      │ Events     │      │ Events     │
            └────────────┘      └────────────┘      └────────────┘

                                     │
                                     ▼
                            Secure Internet/API
                                     │
                                     ▼
                              Authorized User
```

 The architecture separates:

 **local device communication**

 from

 **wide-area communication**

 from

 **application-level communication**.

 This separation is essential because the requirements of a wearable-to-phone link are substantially different from those of a cloud service.

---

 # 7.6 Device-Level Communication

 Before selecting external communication technologies, SSP must distinguish internal hardware communication from external network communication.

 Typical internal interfaces include:

 - I²C;
- SPI;
- UART;
- GPIO;
- ADC;
- USB where required;
- proprietary or component-specific interfaces.

 These interfaces may connect:

```
GNSS ─────┐
IMU ──────┤
Storage ──┤
Security ─┼──► MCU/SoC
Radio ────┤
Power ────┘
```

 The internal buses are not considered substitutes for external communication technologies.

 For example:

 - I²C is an internal peripheral bus;
- SPI is generally an internal high-speed peripheral interface;
- UART can connect internal modules;
- BLE is an external wireless communication technology;
- cellular provides wide-area connectivity.

 This distinction prevents the architecture from mixing hardware interfaces with network interfaces.

---

 # 7.7 Internal Communication Design Principle

 The internal communication architecture should follow the same general SSP principle as the external architecture:

 > **Transfer only the information required by the receiving subsystem.**

 For example, the MCU may receive raw accelerometer samples from an IMU, but the Edge layer may receive only:

 - motion state;
- movement event;
- confidence;
- timestamp;
- relevant context.

 This creates a hierarchy:

```
Raw sensor measurements
          ↓
Embedded processing
          ↓
Structured device information
          ↓
Local wireless communication
          ↓
Edge interpretation
```

 This reduces unnecessary communication volume and provides an important privacy and energy benefit.

---

 # 7.8 Device → Edge Communication

 The Device–Edge link is one of the most important communication decisions in SSP.

 The wearable device is:

 - energy constrained;
- physically mobile;
- computationally limited;
- expected to operate near an authorized Mobile/Edge platform in some deployment scenarios.

 The Edge/Mobile platform, by comparison, can generally provide:

 - greater processing capability;
- larger energy reserves;
- more storage;
- user-interface capability;
- wider-area network access;
- local data aggregation.

 The Device–Edge link should therefore prioritize:

 - low energy consumption;
- local connectivity;
- adequate range;
- low latency;
- secure association;
- mobility;
- simple deployment;
- efficient event transmission.

 Candidate technologies include:

 - BLE;
- Wi-Fi;
- direct cellular;
- other short-range technologies.

---

 # 7.9 BLE as the Primary Device–Edge Candidate

 Bluetooth Low Energy (BLE) is the principal candidate for the Device–Edge link.

 Its architectural role is appropriate because it is designed for low-power short-range communication and can support interaction between a constrained device and a nearby capable platform.

 Potential SSP uses include:

 - device discovery;
- device association;
- authentication support;
- status reporting;
- event transmission;
- proximity information;
- configuration;
- diagnostics;
- firmware-update support where appropriately secured.

 A conceptual BLE relationship is:

```
SSP Device
    │
    │ BLE
    ▼
Mobile / Edge
    │
    ├── Local processing
    ├── Risk assessment
    ├── Storage
    └── Wide-area communication
```

 The architectural benefit is that the wearable does not need to continuously maintain a high-power wide-area communication session merely to remain locally connected to the Edge.

---

 # 7.10 BLE Operating Modes

 BLE communication should not be treated as a single fixed behavior.

 SSP may distinguish between several operational modes.

 ### Mode A — Association

 The device establishes a relationship with an authorized Mobile/Edge platform.

 ### Mode B — Periodic status

 The device periodically communicates:

 - battery status;
- health information;
- device state;
- selected position or motion information.

 ### Mode C — Event-driven communication

 The device transmits information when a relevant event occurs.

 ### Mode D — Elevated monitoring

 The communication frequency or information content increases because risk or operational significance has increased.

 ### Mode E — Critical communication

 High-priority events are transmitted as rapidly as practical through the available path.

 ### Mode F — Recovery

 The device attempts to re-establish a lost relationship.

 This mode-based approach supports SSP's adaptive-monitoring architecture.

---

 # 7.11 Why Wi-Fi Is Not the Fundamental Wearable Protection Link

 Wi-Fi provides substantially greater data throughput than is normally required for SSP event communication.

 However, higher throughput does not automatically make a technology more appropriate for a wearable protection system.

 Potential limitations include:

 - comparatively greater energy requirements;
- dependence on suitable local infrastructure;
- less convenient wearable deployment;
- configuration complexity;
- variable availability outside established coverage areas.

 Wi-Fi remains useful for the Mobile/Edge layer.

 For example:

```
SSP Device
    │
   BLE
    │
Mobile / Edge
    │
  Wi-Fi
    │
Internet
    │
Cloud
```

 This can be useful when the authorized Mobile/Edge platform has access to a trusted Wi-Fi network.

 However, Wi-Fi is not selected as the fundamental Device–Edge protection link.

 The baseline remains:

 **Device → BLE → Mobile/Edge**

---

 # 7.12 Direct Cellular Communication

 Direct cellular connectivity from the SSP device is technically possible and may be useful in deployments where no suitable Mobile/Edge platform is continuously available.

 Potential benefits include:

 - independent wide-area operation;
- reduced dependence on a nearby smartphone;
- broad geographic coverage depending on network availability;
- autonomous remote communication.

 Potential disadvantages include:

 - increased hardware complexity;
- greater power consumption;
- additional antenna requirements;
- increased module cost;
- SIM/eSIM or equivalent provisioning requirements;
- greater certification complexity;
- potentially more difficult wearable integration.

 Direct cellular therefore remains a valid deployment option rather than the baseline local communication mechanism.

 The architecture can support it where autonomous wide-area operation is a specific requirement.

---

 # 7.13 Other Short-Range Technologies

 Other local technologies may be considered depending on the deployment environment.

 Examples include:

 - IEEE 802.15.4-based technologies;
- Zigbee-class networks;
- proprietary sub-GHz links;
- Wi-Fi;
- NFC for very short-range provisioning or interaction.

 These technologies can provide useful capabilities in specific scenarios.

 However, SSP requires a technology that balances:

 **energy + mobility + ecosystem support + device integration + security + sufficient range + practical deployment**

 rather than maximizing a single metric.

 The baseline architecture therefore uses BLE for the principal Device–Edge relationship while preserving the possibility of alternative local technologies for future deployment-specific variants.

---

 # 7.14 Edge → Cloud Communication

 The Edge–Cloud link has different requirements from the Device–Edge link.

 The Edge may communicate with the Cloud using:

 - cellular;
- Wi-Fi;
- Ethernet;
- another IP-capable network.

 The principal requirement is not the selection of one radio technology.

 Instead, the architecture requires:

 > **Secure IP connectivity capable of carrying prioritized SSP application data.**

 The conceptual path is:

```
SSP Device
    │
   BLE
    │
    ▼
Mobile / Edge
    │
    ├── Cellular
    ├── Wi-Fi
    └── Other IP connectivity
             │
             ▼
          Internet
             │
             ▼
           Cloud
```

 The Edge should therefore hide the details of the underlying access network from the higher SSP application layer wherever practical.

---

 # 7.15 Cellular as the Primary Wide-Area Candidate

 Cellular communication is the principal wide-area candidate for SSP.

 Its suitability arises from its ability to provide:

 - geographically distributed coverage;
- IP connectivity;
- mobility support;
- wide-area operation;
- integration with existing network infrastructure.

 The final cellular technology shall be selected according to the target deployment environment and requirements established in later engineering analysis.

 The architecture therefore does not freeze a particular cellular generation or module at this stage.

 Instead, it freezes the role:

 **Cellular/IP = primary candidate for Edge-to-Cloud wide-area connectivity.**

---

 # 7.16 IP-Based Edge–Cloud Communication

 Once the Edge has access to an IP network, SSP can use secure application-level protocols.

 The application architecture should support:

 - event upload;
- status synchronization;
- configuration retrieval;
- policy updates;
- acknowledgement;
- device-health reporting;
- fleet management;
- model-management communication.

 Conceptually:

```
Edge
 │
 ├── Authentication
 ├── Encryption
 ├── Event serialization
 ├── Priority handling
 └── Retry/buffering
 │
 ▼
Secure IP connection
 │
 ▼
Cloud API
```

 The communication protocol shall be selected according to:

 - message semantics;
- reliability requirements;
- overhead;
- connection model;
- implementation complexity;
- scalability;
- security.

 The exact protocol choice is therefore an implementation decision within the architectural constraints established here.

---

 # 7.17 Cloud → User Communication

 Cloud-to-user communication is primarily an application and API problem rather than a new radio-network problem.

 Authorized users may access SSP through:

 - web dashboards;
- mobile applications;
- authorized APIs;
- notification services.

 The communication path is:

```
Cloud
  │
  ├── Secure API
  ├── Dashboard
  ├── Alert service
  └── Management interface
          │
          ▼
Authorized User
```

 The user-facing layer may provide:

 - device status;
- current operational state;
- events;
- severity;
- confidence;
- acknowledgements;
- historical information;
- configuration;
- system health.

 User access shall be subject to authentication and authorization.

---

 # 7.18 Communication Data Classes

 SSP shall classify transmitted information according to operational importance.

 | Class | Example | Priority | Typical behavior |
| --- | --- | --- | --- |
| Routine | Battery, health, periodic status | Low | Scheduled |
| Contextual | Position/motion summary | Medium | Policy-controlled |
| Elevated | Approach, proximity, abnormal movement | High | Increased priority |
| Critical | Confirmed protection event | Highest | Immediate priority |

The classification determines:

 - transmission timing;
- retry behavior;
- buffering;
- communication resources;
- acknowledgement requirements;
- retention priority.

 This ensures that a routine status message cannot unnecessarily compete with a critical event.

---

 # 7.19 Communication Prioritization

 The communication subsystem shall implement a policy-based priority mechanism.

 A conceptual queue is:

```
                 ┌──────────────┐
Routine ────────►│              │
Context ────────►│ Communication│
Elevated ───────►│   Priority   │
Critical ───────►│    Queue     │
                 └──────┬───────┘
                        │
                 Highest priority
                        │
                        ▼
                 Available link
```

 During normal conditions, routine messages may be transmitted periodically.

 During an elevated condition, event-related information should move ahead of routine traffic.

 During a critical event, the communication system should prioritize:

 1. event detection;
2. event context;
3. event delivery;
4. acknowledgement where required.

 This supports the critical-event path established in Chapter 5.

---

 # 7.20 Communication and Data Minimization

 Communication architecture must also support the privacy architecture.

 The system should avoid a design in which:

```
Every sensor
     ↓
Raw data
     ↓
Continuous transmission
     ↓
Cloud
```

 Instead, the preferred flow is:

```
Raw sensing
     ↓
Local processing
     ↓
Relevant information
     ↓
Privacy policy
     ↓
Communication
     ↓
Edge / Cloud
```

 For example, continuous raw accelerometer samples may not be required by the Cloud for routine monitoring.

 The Edge may instead receive:

 - movement state;
- confidence;
- relevant event;
- timestamp.

 Additional data can be transmitted during elevated or critical conditions where authorized and operationally necessary.

 This reduces:

 - communication energy;
- bandwidth usage;
- storage requirements;
- unnecessary data exposure.

---

 # 7.21 Communication Reliability Model

 Communication reliability shall be treated as a system property rather than simply as a radio specification.

 The architecture must consider:

 - packet loss;
- connection loss;
- temporary network unavailability;
- interference;
- congestion;
- device movement;
- gateway failure;
- cloud service disruption.

 A successful communication architecture must therefore define what happens when communication fails.

 The desired behavior is:

```
Communication available
          │
          ▼
Normal operation
          │
     degradation
          │
          ▼
Fallback mode
          │
     local operation
          │
          ▼
Buffered events
          │
      recovery
          │
          ▼
Synchronization
```

---

 # 7.22 BLE Failure

 If the Device loses its BLE connection to the Mobile/Edge layer, the device shall not immediately stop monitoring.

 The device should:

 1. detect the loss;
2. maintain selected local sensing;
3. continue critical local event generation;
4. buffer relevant events;
5. periodically or policy-dependently attempt reconnection;
6. increase communication activity only as justified by the recovery policy.

 If a direct wide-area communication mechanism is present in a deployment variant, the device may use that mechanism as a fallback.

 Otherwise, the device remains locally autonomous until the Edge relationship is restored.

 The key architectural principle is:

 > **Loss of BLE connectivity reduces information exchange before it eliminates local protection functions.**

---

 # 7.23 Cellular Failure

 If the Edge loses cellular connectivity:

```
Edge
 │
 X Cellular
 │
 ▼
Local operation
```

 The Edge should continue:

 - local event processing;
- local risk assessment;
- local storage;
- local device communication;
- priority classification.

 Events intended for the Cloud should be retained until communication becomes available again.

 The Edge may use another IP connection, such as Wi-Fi, when available and authorized.

 This creates a layered fallback:

 **Cellular → alternative IP path → local storage**

 where the deployment supports the relevant alternatives.

---

 # 7.24 Cloud Connectivity Failure

 Cloud unavailability shall not automatically disable the Device or Edge.

 During a Cloud outage:

 - Device operation continues;
- Device–Edge communication continues where available;
- Edge assessment continues;
- local events are stored;
- critical local decisions remain possible;
- synchronization occurs after recovery.

 The architecture therefore distinguishes:

 **Cloud service availability**

 from

 **operational monitoring availability**.

 This is one of the most important resilience properties of SSP.

---

 # 7.25 Mobile/Edge Failure

 The Mobile/Edge layer is a potentially important point of concentration.

 Its failure may result from:

 - battery depletion;
- application failure;
- operating-system failure;
- hardware failure;
- user disabling communication;
- physical separation from the device.

 The architecture should therefore provide controlled behavior.

 At minimum:

```
Edge unavailable
      ↓
Device detects communication loss
      ↓
Local monitoring continues
      ↓
Events buffered
      ↓
Edge returns
      ↓
Synchronization
```

 For autonomous deployments, direct wide-area communication may be added to reduce dependence on the Mobile/Edge platform.

 This is a deployment-specific extension rather than a change to the fundamental SSP architecture.

---

 # 7.26 Communication Quality Degradation

 Communication quality should not be represented simply as:

 **Connected / Disconnected**

 Instead, SSP should be capable of recognizing intermediate conditions such as:

 - reduced signal quality;
- increased packet loss;
- repeated retransmissions;
- high latency;
- intermittent connection;
- unstable association.

 This information can feed the adaptive control loop.

 For example:

```
Communication quality decreases
            ↓
Transmission becomes less efficient
            ↓
Communication policy adapts
            ↓
Routine traffic reduced
            ↓
Critical traffic retained
```

 This prevents the system from wasting energy repeatedly transmitting low-priority information over a poor link.

---

 # 7.27 Communication Recovery

 Recovery shall be treated as a controlled synchronization process.

 After connectivity is restored:

```
Connection restored
       ↓
Authenticate
       ↓
Verify communication state
       ↓
Synchronize critical events
       ↓
Synchronize elevated events
       ↓
Synchronize routine information
       ↓
Confirm consistency
       ↓
Return to normal operation
```

 The ordering is important.

 Critical events should not remain blocked behind large quantities of routine historical data.

 The synchronization mechanism should therefore support prioritization.

---

 # 7.28 Store-and-Forward Architecture

 Local storage provides the foundation for communication resilience.

 The architecture is:

```
Event generated
      ↓
Classified
      ↓
Stored locally
      ↓
Transmission attempted
      │
      ├── Success → Mark synchronized
      │
      └── Failure → Retain
                       │
                       ▼
                 Retry according
                 to policy
```

 Stored information should include sufficient metadata to support:

 - event identification;
- timestamp ordering;
- transmission status;
- integrity checking;
- synchronization;
- duplicate detection.

 This avoids uncontrolled event duplication when communication is restored.

---

 # 7.29 Communication Acknowledgement

 Not all messages require the same acknowledgement behavior.

 A possible conceptual policy is:

 | Message type | Acknowledgement requirement |
| --- | --- |
| Routine status | Optional or batched |
| Contextual information | Policy-dependent |
| Elevated event | Recommended |
| Critical event | Required where operationally appropriate |
| Configuration update | Required |
| Security update | Required |
| Firmware update | Required |

Acknowledgement confirms communication delivery or processing at a defined layer.

 It should not automatically be interpreted as proof that the physical-world event itself has been resolved.

 This distinction is important when defining operational semantics.

---

 # 7.30 Duplicate Detection and Idempotency

 Communication retries can create duplicate messages.

 For example:

```
Event generated
     ↓
Transmit
     ↓
Cloud receives
     ↓
Acknowledgement lost
     ↓
Device retries
     ↓
Cloud receives same event again
```

 The architecture should therefore provide a mechanism for identifying repeated events.

 A structured event identifier may include:

 - device identity;
- event sequence number;
- timestamp;
- event identifier.

 The receiving system should be capable of recognizing duplicates and processing them safely.

 This becomes especially important during offline synchronization.

---

 # 7.31 Communication Security Architecture

 Security shall apply to every communication boundary.

 The initial security chain is:

```
Device
   │
   │ Authenticated + Protected
   ▼
Edge
   │
   │ Authenticated + Protected
   ▼
Cloud
   │
   │ Authenticated + Authorized
   ▼
User
```

 The communication architecture shall provide, as appropriate:

 - mutual authentication;
- confidentiality;
- integrity;
- replay protection;
- credential protection;
- secure provisioning;
- authorization;
- secure session establishment;
- auditability.

 Security shall not depend solely on the assumption that the network itself is trusted.

---

 # 7.32 Device Authentication

 Each SSP device shall possess a unique identity.

 The identity should be associated with:

 - device registration;
- cryptographic credentials;
- deployment state;
- firmware version;
- security state;
- authorized configuration.

 The Edge should be able to determine whether a connecting device is:

 - registered;
- authorized;
- revoked;
- unknown;
- operating with an unacceptable security state.

 This supports the trust architecture established in Chapters 5 and 6.

---

 # 7.33 Mutual Authentication

 Where technically appropriate, SSP should use mutual authentication.

 Conceptually:

```
Device ──────► Proves device identity
Device ◄────── Proves Edge identity
       │
       ▼
Authenticated session
       │
       ▼
Protected communication
```

 This reduces the risk of an unauthorized system impersonating an Edge platform or an unauthorized device entering the SSP network.

 The exact authentication protocol will be selected during detailed security engineering.

---

 # 7.34 Encryption and Integrity

 Communication confidentiality protects information from unauthorized observation.

 Communication integrity protects against unauthorized modification.

 Both are required because SSP information may include:

 - position;
- device identity;
- operational state;
- security state;
- event information;
- configuration;
- management commands.

 The architecture therefore requires protection against:

 - passive interception;
- message modification;
- unauthorized injection;
- replay;
- session hijacking.

 The exact cryptographic algorithms and protocols are deferred to the security implementation chapter.

---

 # 7.35 Replay Protection

 A previously valid SSP message should not be accepted as a new event simply because it has been retransmitted.

 Replay protection may use mechanisms such as:

 - sequence numbers;
- timestamps;
- nonces;
- session identifiers;
- freshness windows.

 For example:

```
Event #105
   ↓
Accepted

Event #105 repeated
   ↓
Detected as duplicate/replay
   ↓
Rejected or ignored
```

 This is particularly important for critical events and configuration messages.

---

 # 7.36 Secure Provisioning

 Security begins before normal operation.

 The device lifecycle should include:

```
Manufacture / Prototype
        ↓
Identity creation
        ↓
Credential provisioning
        ↓
Device registration
        ↓
Deployment authorization
        ↓
Operational use
        ↓
Maintenance / update
        ↓
Revocation / retirement
```

 Provisioning procedures should ensure that credentials are not exposed unnecessarily during manufacturing, deployment or maintenance.

 This is also important for fleet scalability.

---

 # 7.37 Key and Credential Management

 Communication security requires lifecycle management of credentials.

 The system should support:

 - credential creation;
- secure storage;
- rotation where required;
- revocation;
- replacement;
- recovery procedures;
- device retirement.

 The secure hardware capabilities identified in Chapter 6 provide a potential foundation for protected credential storage.

 Cloud management should maintain the authoritative association between device identity and deployment state.

---

 # 7.38 Application and API Security

 Even when the underlying communication link is encrypted, the application layer must enforce authorization.

 The Cloud API should therefore distinguish between:

 - device communication;
- Edge communication;
- operator access;
- administrative functions;
- configuration changes;
- model management.

 An authenticated user should not automatically receive administrative authority.

 Likewise, an authenticated device should not automatically have access to unrelated device records.

 This follows the least-privilege principle established by the SSP security architecture.

---

 # 7.39 Communication Technology Landscape

 SSP must consider several communication technologies.

 The principal candidates are:

 - BLE;
- Wi-Fi;
- cellular;
- LoRa/LoRaWAN-class LPWAN;
- IEEE 802.15.4-class local networks;
- other proprietary or specialized technologies.

 They serve different purposes.

 A useful conceptual classification is:

 | Technology | Primary networking role | SSP relevance |
| --- | --- | --- |
| BLE | WPAN/local | High |
| Wi-Fi | WLAN | High at Edge |
| Cellular | WWAN | High |
| LoRaWAN | LPWAN | Scenario-dependent |
| IEEE 802.15.4 | WPAN/local mesh | Scenario-dependent |
| NFC | Very short range | Limited/specialized |

The architecture should therefore avoid treating these technologies as direct substitutes in every context.

---

 # 7.40 BLE Assessment

 BLE provides characteristics relevant to the Device–Edge relationship.

 ### Advantages

 - low-power operation;
- widespread support in mobile platforms;
- suitable for short-range communication;
- suitable for event/status messages;
- practical device association;
- mature ecosystem;
- useful proximity information.

 ### Limitations

 - limited range compared with wide-area technologies;
- dependence on a nearby capable Edge/Mobile platform;
- performance affected by environment and body placement;
- not intended as a direct wide-area network.

 ### SSP role

 **Primary candidate for Device ↔ Mobile/Edge.**

---

 # 7.41 Wi-Fi Assessment

 Wi-Fi provides:

 - high throughput;
- IP connectivity;
- broad availability in many fixed environments;
- mature infrastructure.

 However, for the wearable Device–Edge link it can introduce:

 - higher energy consumption;
- infrastructure dependency;
- greater connection-management complexity;
- limited usefulness outside Wi-Fi coverage.

 ### SSP role

 **Useful primarily as an Edge/Mobile → Internet connectivity option.**

 It may also be used for development, diagnostics or deployment-specific configurations.

---

 # 7.42 Cellular Assessment

 Cellular provides:

 - wide-area coverage;
- mobility;
- direct Internet/IP connectivity;
- independence from local Wi-Fi infrastructure.

 Potential disadvantages include:

 - power consumption;
- hardware complexity;
- subscription/network costs;
- antenna requirements;
- certification;
- provisioning complexity.

 ### SSP role

 **Primary candidate for Edge/Mobile → Cloud wide-area connectivity.**

 It may also support direct Device → Cloud communication in autonomous deployment variants.

---

 # 7.43 LoRa/LPWAN Assessment

 LPWAN technologies can provide:

 - long communication range;
- low-power operation;
- relatively small messages;
- infrastructure suitable for some fixed or regional deployments.

 However, SSP's requirements can include:

 - mobility;
- event latency;
- bidirectional communication;
- integration with Mobile/Edge;
- potentially richer contextual information.

 These characteristics may not always align with the principal wearable architecture.

 LPWAN can nevertheless be relevant to specific deployments involving:

 - fixed infrastructure;
- remote areas;
- low-rate telemetry;
- dedicated local gateways.

 ### SSP role

 **Scenario-dependent rather than baseline.**

---

 # 7.44 IEEE 802.15.4-Class Technologies

 IEEE 802.15.4-based technologies can provide low-power local networking and may support multi-node deployments.

 Potential benefits include:

 - low-power operation;
- local networking;
- mesh-oriented configurations;
- suitability for some sensor networks.

 Potential disadvantages for SSP include:

 - less direct integration with common smartphones;
- additional gateway requirements;
- increased network-management complexity;
- less straightforward wearable deployment.

 ### SSP role

 **Potential alternative for specialized deployments, not the baseline Mobile/Edge link.**

---

 # 7.45 NFC and Very Short-Range Communication

 NFC has extremely limited range but can be useful for:

 - provisioning;
- device pairing assistance;
- maintenance;
- identification;
- deliberate close-contact interactions.

 It should not be considered the primary SSP event-communication mechanism.

 ### SSP role

 **Specialized provisioning and service function.**

---

 # 7.46 WBAN Considerations

 A Wireless Body Area Network (WBAN) focuses on communication around or on the human body.

 For SSP, WBAN concepts are relevant when multiple sensors are distributed across the user.

 Potential characteristics include:

 - very short range;
- low-power operation;
- wearable sensor integration;
- body-centric communication.

 However, SSP's baseline device architecture currently treats the principal wearable as an integrated sensing and processing node.

 Therefore, a full multi-sensor WBAN is not required by the baseline architecture.

 If future deployments use distributed body sensors, a WBAN-style architecture may become appropriate.

---

 # 7.47 WPAN Considerations

 A Wireless Personal Area Network (WPAN) is highly relevant to SSP.

 The Device ↔ Mobile/Edge link can be considered a personal/local-area relationship.

 BLE is therefore a natural candidate for the WPAN role.

 Conceptually:

```
Wearable Device
       │
     WPAN
       │
       ▼
Mobile / Edge
```

 This is one of the principal reasons BLE is selected as the baseline local communication technology.

---

 # 7.48 WLAN Considerations

 WLAN technologies such as Wi-Fi are most relevant to the Edge's connection to local network infrastructure.

 For example:

```
Device
  │
 BLE
  │
Edge
  │
 Wi-Fi
  │
Router / Internet
  │
Cloud
```

 This architecture separates the wearable's low-power local link from the higher-throughput IP network.

 The distinction is important because the optimal technology for the wearable is not necessarily the optimal technology for the Edge.

---

 # 7.49 WWAN Considerations

 Wide-area cellular communication corresponds to the WWAN role.

 A representative SSP path is:

```
Device
   │
  BLE
   │
Mobile / Edge
   │
Cellular
   │
Internet
   │
Cloud
```

 This provides geographic mobility without requiring the wearable itself to continuously operate a wide-area radio.

 It also centralizes wide-area communication management at the Edge, where more energy and computational resources may be available.

---

 # 7.50 LPWAN Considerations

 LPWAN technologies provide another architectural option for low-rate wide-area telemetry.

 They may be useful when:

 - data volumes are small;
- latency requirements are moderate;
- coverage is available;
- gateway infrastructure can be deployed;
- energy efficiency is highly important.

 However, they should not automatically replace cellular because SSP's communication requirements include:

 - mobility;
- critical-event delivery;
- secure bidirectional management;
- flexible IP connectivity.

 LPWAN therefore remains a scenario-specific alternative.

---

 # 7.51 Communication Technology Comparison

 The following comparison is qualitative at the architecture stage.

 | Criterion | BLE | Wi-Fi | Cellular | LPWAN | 802.15.4-class |
| --- | --- | --- | --- | --- | --- |
| Short-range suitability | High | High | Low | Low | High |
| Wide-area suitability | Low | Low–medium | High | High | Low–medium |
| Wearable energy suitability | High | Medium–low | Medium–low | High | High |
| Smartphone integration | High | High | Limited as device-to-phone link | Low | Low |
| Bandwidth | Low–medium | High | Medium–high | Low | Low–medium |
| Mobility | High | Medium | High | Medium | Medium |
| Infrastructure dependency | Low locally | High | Network dependent | Gateway dependent | Gateway/mesh dependent |
| Proximity information | High | Medium | Low | Low | Medium |
| SSP Device–Edge role | Strong | Possible | Alternative | Weak | Alternative |
| SSP Edge–Cloud role | Weak | Strong | Strong | Possible | Weak |
| Security capability | Strong with appropriate configuration | Strong with appropriate configuration | Strong with appropriate configuration | Strong with appropriate configuration | Strong with appropriate configuration |
| Typical SSP architectural role | Local wearable link | Edge Internet access | Wide-area link | Specialized telemetry | Specialized local network |

The table is an architectural comparison rather than a claim that one technology is universally superior.

 Actual performance must be measured in the intended deployment environment.

---

 # 7.52 Communication Selection Criteria

 The final technology selection should be based on weighted engineering criteria.

 A representative evaluation framework is:

 | Criterion | Importance to SSP |
| --- | --- |
| Energy consumption | Very high |
| Reliability | Very high |
| Security | Very high |
| Latency | High |
| Mobility | High |
| Coverage | High |
| Smartphone/Edge integration | High |
| Infrastructure requirements | Medium–high |
| Cost | Medium–high |
| Bandwidth | Medium |
| Deployment complexity | Medium–high |
| Scalability | High |

The weighting should ultimately be derived from the system requirements and target deployment scenario.

 This prevents communication technology from being selected simply because it has the highest bandwidth or longest nominal range.

---

 # 7.53 Selected Communication Architecture

 The baseline SSP communication architecture is now selected as:

 > **SSP Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ Authorized User**

 with:

 **Wi-Fi available to the Mobile/Edge layer where appropriate.**

 The principal architectural roles are therefore:

 | Link | Baseline technology/approach | Status |
| --- | --- | --- |
| Internal sensors ↔ MCU | I²C/SPI/UART/GPIO as appropriate | Selected conceptually |
| Device ↔ Mobile/Edge | BLE | Selected baseline |
| Mobile/Edge ↔ Internet | Cellular/IP | Selected primary candidate |
| Mobile/Edge ↔ Internet alternative | Wi-Fi/IP | Supported option |
| Cloud ↔ User | Secure Internet/API | Selected |
| Direct Device ↔ WAN | Cellular or other option | Deployment-dependent |
| Specialized fixed deployments | LPWAN/802.15.4 options | Open |

This freezes the architectural communication direction without freezing every implementation parameter.

---

 # 7.54 Why BLE Is the Baseline Device–Edge Link

 The selection of BLE follows directly from the architecture.

 The SSP Device requires:

 - low energy consumption;
- local interaction;
- wearable compatibility;
- proximity capability;
- mobile-platform integration;
- event-oriented communication.

 The Mobile/Edge layer provides:

 - additional processing;
- storage;
- user interaction;
- wide-area communication.

 BLE therefore creates an effective division:

```
Device
Low energy + local sensing
        │
       BLE
        │
        ▼
Edge
Higher computation + storage + WAN
```

 This reduces the need for the wearable to carry the full burden of wide-area networking.

---

 # 7.55 Why Cellular Is the Baseline Wide-Area Link

 Cellular is selected as the primary wide-area candidate because the Edge requires communication beyond local wireless range.

 The Edge may be:

 - mobile;
- geographically distributed;
- disconnected from fixed infrastructure;
- used in environments where Wi-Fi is unavailable.

 Cellular provides a practical general-purpose wide-area mechanism.

 The exact cellular technology remains a later engineering selection based on:

 - geographic deployment;
- network availability;
- energy;
- cost;
- module lifecycle;
- regulatory requirements.

---

 # 7.56 Why Wi-Fi Remains Available

 The selection of cellular as the primary wide-area candidate does not imply that Wi-Fi should be excluded.

 Wi-Fi can be valuable when:

 - the Edge operates indoors;
- a trusted network is available;
- high data volume is required;
- software updates or diagnostics are being performed;
- development environments are being used.

 The Edge communication abstraction should therefore permit:

```
Cellular
   OR
Wi-Fi
   OR
Other authorized IP network
```

 without changing the SSP application-level event model.

---

 # 7.57 Communication Abstraction Layer

 To prevent hardware-specific communication decisions from spreading throughout the software architecture, SSP should introduce a communication abstraction.

 Conceptually:

```
              SSP Application
                     │
             Communication API
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
         BLE       Cellular     Wi-Fi
          │          │           │
          └──────────┼───────────┘
                     ▼
                Network stack
```

 This permits future communication technologies to be introduced without redesigning the complete application layer.

 It also supports prototype-to-product evolution.

---

 # 7.58 Communication Session Management

 Communication sessions should be managed according to operational state.

 A session may involve:

 1. discovery;
2. authentication;
3. secure connection establishment;
4. data exchange;
5. acknowledgement;
6. session maintenance;
7. controlled termination;
8. recovery/reconnection.

 For low-power Device–Edge communication, sessions should avoid unnecessary persistent high-duty-cycle activity.

 The communication manager should instead coordinate with the SSP operating-state machine.

---

 # 7.59 Communication and Adaptive Monitoring

 The communication architecture forms part of the adaptive control loop established in Chapter 5.

 The relationship is:

```
Risk state
    ↓
Monitoring policy
    ↓
Communication policy
    ↓
Data priority
    ↓
Transmission behavior
    ↓
Energy consumption
```

 For example:

 ### Normal state

 - low communication frequency;
- periodic health/status;
- limited contextual data.

 ### Elevated state

 - more frequent updates;
- higher event priority;
- increased contextual information.

 ### Critical state

 - immediate event transmission;
- retries;
- acknowledgement;
- high-priority synchronization.

 This makes communication an active part of SSP system behavior.

---

 # 7.60 Communication and Energy

 Communication is a major contributor to device energy consumption.

 A simplified model is:

 **E\_comm = Σ(E\_tx \+ E\_rx + E\_connection + E\_retry)**

 The actual energy depends on:

 - transmit power;
- connection duration;
- packet size;
- number of packets;
- retransmissions;
- scanning;
- connection establishment;
- radio sleep behavior.

 The architecture therefore seeks to reduce unnecessary communication through:

 - local processing;
- event-driven transmission;
- batching of routine data;
- priority queues;
- adaptive connection behavior;
- buffering during poor connectivity.

---

 # 7.61 Communication and Latency

 Communication latency is not a single quantity.

 SSP should distinguish:

 **Detection latency**

 from

 **Device–Edge latency**

 from

 **Edge processing latency**

 from

 **Edge–Cloud latency**

 from

 **User notification latency**.

 The critical path can therefore be represented as:

```
Physical event
      ↓
Local detection
      ↓
BLE transfer
      ↓
Edge assessment
      ↓
WAN transfer
      ↓
Cloud processing
      ↓
User notification
```

 However, Chapter 5 established that critical operational functions should not depend unnecessarily on the full path.

 The architecture therefore allows:

```
Physical event
      ↓
Local detection
      ↓
Edge assessment
      ↓
Immediate local/Edge action
```

 while Cloud synchronization can occur in parallel where appropriate.

---

 # 7.62 Communication and Scalability

 A scalable communication architecture must avoid requiring every device to maintain independent high-volume communication with the Cloud.

 The baseline architecture instead uses the Edge as an aggregation point.

 For example:

```
Device 1 ──┐
Device 2 ──┤
Device 3 ──┼──► Mobile / Edge ───► Cloud
Device N ──┘
```

 The Edge can therefore:

 - aggregate events;
- filter redundant information;
- perform local correlation;
- prioritize traffic;
- batch routine messages;
- reduce duplicate transmissions.

 This can improve scalability while reducing communication overhead.

---

 # 7.63 Multi-Device Event Correlation

 The Edge layer can combine information from multiple devices.

 For example:

```
Device A ──┐
Device B ──┼──► Edge correlation
Device C ──┘
                │
                ▼
         Combined context
                │
                ▼
          Risk assessment
```

 This is particularly useful where operational significance depends on relative position or simultaneous events.

 The communication architecture therefore supports not only device-to-system communication but also multi-device contextual intelligence.

---

 # 7.64 Communication and Privacy

 The communication architecture implements privacy by reducing unnecessary data movement.

 A useful design principle is:

 > **Data should not cross an architectural boundary merely because the system is technically capable of transmitting it.**

 The transmission decision should instead consider:

 - operational necessity;
- sensitivity;
- retention requirements;
- processing location;
- security;
- energy;
- regulatory/privacy constraints.

 This supports the data-minimization architecture established in Chapters 3 and 5.

---

 # 7.65 Communication Monitoring

 The communication subsystem shall monitor its own condition.

 Potential metrics include:

 - signal quality;
- connection state;
- packet loss;
- retransmission count;
- latency;
- connection duration;
- data volume;
- authentication failures;
- synchronization status.

 These metrics can be used by the Edge and Cloud for:

 - diagnostics;
- maintenance;
- optimization;
- failure detection;
- fleet management.

---

 # 7.66 Communication Diagnostics

 A communication diagnostic record may contain:

```
Timestamp
Device ID
Interface
Connection state
Signal quality
Packet statistics
Retry count
Latency
Failure code
Recovery status
```

 Diagnostic information should itself be subject to data-minimization and retention policies.

 Routine diagnostic information should not consume disproportionate communication or storage resources.

---

 # 7.67 Communication Failure-State Model

 The communication state machine can be represented as:

```
             ┌──────────────┐
             │ DISCONNECTED │
             └──────┬───────┘
                    │
              Discovery
                    ▼
             ┌──────────────┐
             │  CONNECTING  │
             └──────┬───────┘
                    │
               Success
                    ▼
             ┌──────────────┐
             │  CONNECTED   │
             └──────┬───────┘
                    │
                Degradation
                    ▼
             ┌──────────────┐
             │   DEGRADED   │
             └──────┬───────┘
                    │
             Failure threshold
                    ▼
             ┌──────────────┐
             │  OFFLINE     │
             └──────┬───────┘
                    │
              Recovery
                    ▼
             Synchronization
                    │
                    ▼
                CONNECTED
```

 The exact thresholds belong to later software and communication testing.

---

 # 7.68 Critical-Event Communication Path

 The critical communication path is:

```
Physical event
      ↓
Device detection
      ↓
Priority event created
      ↓
BLE transmission
      ↓
Edge validation
      ↓
Risk/severity assessment
      ↓
Priority WAN communication
      ↓
Cloud / authorized alert path
      ↓
Acknowledgement
```

 The architecture shall ensure that routine communication cannot unnecessarily block this path.

 Where the Edge can make an operational decision locally, that decision should not wait for Cloud confirmation.

---

 # 7.69 Normal Communication Path

 The normal information path is:

```
Sensor
  ↓
Device processing
  ↓
Structured status/event
  ↓
BLE
  ↓
Edge
  ↓
Aggregation/filtering
  ↓
Cellular/Wi-Fi
  ↓
Cloud
  ↓
Storage/analytics/dashboard
```

 This path is optimized for:

 - efficiency;
- aggregation;
- historical analysis;
- fleet management.

 It is distinct from the critical-event path.

---

 # 7.70 Communication Policy Example

 A conceptual communication policy is:

 | Operational condition | Device behavior | Edge behavior | WAN behavior |
| --- | --- | --- | --- |
| Normal | Periodic status | Aggregate/filter | Batched/periodic |
| Elevated | Increased event reporting | Increased assessment | Higher priority |
| Critical | Immediate event | Immediate processing | Priority delivery |
| BLE unavailable | Local monitoring | — | Optional direct path |
| WAN unavailable | Local buffering | Local operation | Store-and-forward |
| Cloud unavailable | Continue | Continue | Queue and retry |
| Low battery | Reduce non-critical traffic | Prioritize important data | Policy-dependent |

This table links communication behavior directly to the adaptive SSP architecture.

---

 # 7.71 Communication Configuration

 Communication parameters should be remotely configurable where security and reliability permit.

 Potential parameters include:

 - reporting intervals;
- retry limits;
- event priorities;
- connection timeout;
- synchronization policy;
- diagnostic frequency;
- communication fallback policy.

 Configuration updates must be:

 - authenticated;
- authorized;
- integrity protected;
- version controlled;
- auditable.

 A faulty configuration must not be allowed to disable essential protection functionality without appropriate safeguards.

---

 # 7.72 Firmware and Communication Updates

 The communication architecture must support future evolution.

 Updates may be required for:

 - radio firmware;
- communication protocols;
- security credentials;
- application software;
- device configuration.

 Updates should use a controlled lifecycle:

```
Update created
      ↓
Authenticated
      ↓
Integrity verified
      ↓
Compatibility checked
      ↓
Installed
      ↓
Validated
      ↓
Activated
```

 Rollback mechanisms should be considered for critical software updates.

 This connects the communication architecture to the secure lifecycle requirements of Chapter 6.

---

 # 7.73 Communication Cost

 Communication cost has two major dimensions.

 ### Financial cost

 Potential costs include:

 - cellular subscriptions;
- data usage;
- gateway infrastructure;
- Cloud communication services;
- SIM/eSIM management;
- certification;
- maintenance.

 ### Resource cost

 Communication also consumes:

 - energy;
- bandwidth;
- storage;
- processing;
- operational attention.

 The architecture therefore seeks to minimize unnecessary communication without reducing required protection performance.

---

 # 7.74 Communication Architecture Traceability

 The initial traceability is:

 | Requirement | Communication response | Verification |
| --- | --- | --- |
| Local Device–Edge communication | BLE baseline | Range/latency test |
| Wide-area connectivity | Cellular/IP | Coverage/connectivity test |
| Edge Internet alternative | Wi-Fi/IP | Network-fallback test |
| Critical-event delivery | Priority communication | Critical-path latency test |
| Battery autonomy | Adaptive communication | Energy-per-mode test |
| Connectivity resilience | Buffer/retry/synchronization | Outage test |
| Privacy | Local filtering/data minimization | Data-flow audit |
| Device authentication | Secure device identity | Authentication test |
| Confidentiality | Encrypted communication | Security test |
| Integrity | Integrity protection | Message-modification test |
| Replay protection | Sequence/freshness mechanisms | Replay test |
| Scalability | Edge aggregation | Multi-device load test |
| Fleet management | Secure Cloud/API communication | Management test |
| Mobility | BLE + cellular architecture | Mobility test |

This traceability will be expanded as concrete protocols and technologies are selected.

---

 # 7.75 Communication Architecture Decisions

 The principal decisions of this chapter are:

 | ID | Communication decision | Status |
| --- | --- | --- |
| CD-01 | Separate Device, Edge and Cloud communication roles | **Selected** |
| CD-02 | BLE as baseline Device–Edge technology | **Selected** |
| CD-03 | Wi-Fi available as an Edge/IP connectivity option | **Selected** |
| CD-04 | Cellular/IP as primary wide-area candidate | **Selected** |
| CD-05 | Secure Internet/API for Cloud–User communication | **Selected** |
| CD-06 | Policy-based communication prioritization | **Selected** |
| CD-07 | Store-and-forward during connectivity loss | **Selected** |
| CD-08 | Critical traffic separated from routine traffic | **Selected** |
| CD-09 | Communication security across all trust boundaries | **Selected** |
| CD-10 | Device identity and authenticated communication | **Selected** |
| CD-11 | Replay/duplicate protection | **Selected conceptually** |
| CD-12 | Data-minimizing communication | **Selected** |
| CD-13 | Communication abstraction layer | **Selected conceptually** |
| CD-14 | Direct cellular Device connectivity | **Deployment-dependent** |
| CD-15 | LPWAN | **Scenario-dependent** |
| CD-16 | IEEE 802.15.4-class alternative | **Scenario-dependent** |
| CD-17 | Specific BLE profile | **Open** |
| CD-18 | Specific cellular technology/module | **Open** |
| CD-19 | Specific application protocol | **Open for detailed design** |
| CD-20 | Specific cryptographic protocol suite | **Open for security design** |

This distinction preserves the separation between architectural decisions and implementation decisions.

---

 # 7.76 Communication Risks and Engineering Questions

 Several communication questions remain open.

 ### CR-01 — BLE range

 What practical Device–Edge range can be achieved with the selected wearable enclosure and body placement?

 ### CR-02 — BLE reliability

 How reliably can events be delivered under movement, obstruction and interference?

 ### CR-03 — Cellular coverage

 Does the selected deployment environment provide adequate wide-area coverage?

 ### CR-04 — Communication energy

 What proportion of the device energy budget is consumed by BLE scanning, connection maintenance and event transmission?

 ### CR-05 — Edge availability

 How often can the Mobile/Edge platform be expected to be unavailable or separated from the device?

 ### CR-06 — Critical-event latency

 What end-to-end latency can be achieved from physical event to authorized notification?

 ### CR-07 — Offline retention

 How much event data must be retained during communication outages?

 ### CR-08 — Synchronization

 How should events be ordered and deduplicated after recovery?

 ### CR-09 — Security overhead

 What energy, latency and memory overhead is introduced by secure communication?

 ### CR-10 — Scalability

 How many devices can one Edge platform support under the intended workload?

 These questions will be addressed experimentally and analytically in subsequent chapters.

---

 # 7.77 Communication KPIs

 The communication architecture introduces the following measurable KPIs.

 ## Range

 - effective BLE range;
- reliable communication distance;
- connectivity probability versus distance.

 ## Latency

 - Device–Edge latency;
- Edge processing latency;
- Edge–Cloud latency;
- critical alert latency;
- synchronization latency.

 ## Reliability

 - packet delivery rate;
- event delivery success rate;
- connection recovery rate;
- synchronization success rate.

 ## Energy

 - energy per transmitted event;
- energy per received event;
- energy per connection;
- communication energy per operating mode;
- daily communication energy.

 ## Availability

 - BLE availability;
- WAN availability;
- Cloud communication availability;
- effective end-to-end availability.

 ## Security

 - authentication success;
- unauthorized-device rejection;
- replay rejection;
- message-integrity verification;
- credential-protection effectiveness.

 ## Scalability

 - devices per Edge;
- events per second;
- queue depth;
- synchronization throughput;
- Cloud API response time.

 ## Data efficiency

 - bytes per event;
- raw-data reduction;
- routine versus critical traffic volume.

 These KPIs will be used to determine whether the selected architecture provides measurable engineering benefit.

---

 # 7.78 Communication Test Strategy

 The communication architecture shall eventually be validated through controlled tests.

 ### Test Group A — Device–Edge

 Measure:

 - discovery time;
- connection time;
- range;
- packet loss;
- latency;
- energy consumption.

 ### Test Group B — Edge–Cloud

 Measure:

 - connection establishment;
- throughput;
- latency;
- outage behavior;
- recovery;
- synchronization.

 ### Test Group C — Critical events

 Measure:

 - event generation;
- priority transmission;
- end-to-end latency;
- delivery success;
- acknowledgement.

 ### Test Group D — Security

 Test:

 - unauthorized device;
- unauthorized Edge;
- modified message;
- replayed message;
- invalid credential;
- expired credential.

 ### Test Group E — Scalability

 Evaluate:

 - multiple devices;
- simultaneous events;
- high event rates;
- Edge resource consumption;
- Cloud response.

 ### Test Group F — Energy

 Measure:

 - BLE scanning;
- BLE connection;
- event transmission;
- retries;
- communication during elevated mode;
- communication during critical mode.

 This provides a direct path from architecture to experimental validation.

---

 # 7.79 Communication Architecture and Later Chapters

 Chapter 7 establishes the communication framework required by the remaining system design.

 ### Chapter 8 — Embedded Software

 Will determine:

 - communication state machines;
- drivers;
- event queues;
- retry logic;
- synchronization;
- power-aware communication behavior.

 ### Data Architecture

 Will determine:

 - event schema;
- serialization;
- message metadata;
- storage format;
- retention.

 ### Intelligence/AI

 Will determine:

 - information required by predictive algorithms;
- confidence propagation;
- Edge data requirements;
- model update communication.

 ### Energy and Performance

 Will quantify:

 - communication energy;
- latency;
- duty cycles;
- autonomy.

 ### Cloud Architecture

 Will determine:

 - APIs;
- ingestion services;
- message processing;
- fleet management;
- storage.

 ### Security Architecture

 Will determine:

 - cryptographic protocols;
- identity management;
- credential lifecycle;
- secure API design.

 Thus the communication architecture serves as the interface between hardware and higher-level software/system design.

---

 # 7.80 First SSP Communication Baseline

 At the completion of this chapter operating states, event processing, power management, communication control, local, the SSP communication baseline can be represented as:

```
                    AUTHORIZED USER
                           ▲
                           │
                    Secure API/Internet
                           │
                           ▼
                     ┌───────────┐
                     │   CLOUD   │
                     └─────▲─────┘
                           │
                     Secure IP/WAN
                           │
                 Cellular / Wi-Fi
                           │
                           ▼
                 ┌────────────────┐
                 │ MOBILE / EDGE  │
                 │                │
                 │ Fusion         │
                 │ Risk           │
                 │ Prediction     │
                 │ Storage        │
                 │ Prioritization │
                 └───────▲────────┘
                         │
                        BLE
                         │
          ┌──────────────┼──────────────┐
          │              │              │
      ┌───┴───┐      ┌───┴───┐      ┌───┴───┐
      │Device1│      │Device2│      │DeviceN│
      └───────┘      └───────┘      └───────┘

                    Local buffering
                    Local processing
                    Adaptive priority
                    Secure identity
```

 The resulting architecture can be summarized as:

 **BLE provides the local wearable communication relationship.**

 **Mobile/Edge provides local intelligence and communication aggregation.**

 **Cellular/IP provides the principal wide-area path.**

 **Wi-Fi provides an alternative Edge IP path where available.**

 **Cloud/API communication provides centralized management and user access.**

 **Local storage and fallback behavior preserve operational continuity during communication disruption.**

---

 # 7.81 Communication Design Baseline

 The communication architecture can therefore be stated as the following engineering baseline:

 > **SSP shall use a low-power local wireless connection, with BLE as the baseline Device–Edge technology, to connect wearable SSP devices to an authorized Mobile/Edge platform. The Mobile/Edge platform shall provide local processing, event aggregation and communication management. Cellular/IP shall serve as the primary candidate for wide-area Edge–Cloud communication, with Wi-Fi available as an alternative IP access mechanism where appropriate. Cloud-to-user interaction shall occur through authenticated and authorized Internet/API interfaces. Communication shall be prioritized according to event significance and shall support secure operation, buffering, retry, synchronization and degraded operation during connectivity loss.**

 This baseline provides enough architectural specificity to support subsequent software and system engineering while leaving component-level choices open.

---

 # 7.82 Chapter 7 Assessment — What Has Been Established

 The main engineering conclusions of this chapter are:

 ### 1\. SSP requires multiple communication technologies

 No single communication technology satisfies all SSP requirements equally well.

 The architecture therefore separates:

 - local wearable communication;
- wide-area communication;
- application-level communication.

 ### 2\. BLE is the baseline local Device–Edge technology

 BLE is selected because the wearable requires low-power local connectivity and practical interaction with a Mobile/Edge platform.

 ### 3\. Cellular/IP is the primary wide-area architecture

 Cellular is selected as the principal candidate for Edge-to-Cloud connectivity because the Edge may operate across geographically distributed environments.

 ### 4\. Wi-Fi is complementary

 Wi-Fi remains useful for the Edge's Internet connection and development/deployment scenarios but is not the fundamental wearable protection link.

 ### 5\. Communication is adaptive

 Communication frequency and priority shall change according to operational significance.

 ### 6\. Communication is security-sensitive

 Every architectural boundary requires authentication, integrity and appropriate confidentiality.

 ### 7\. Communication failure is expected

 SSP shall explicitly support:

 - buffering;
- retry;
- reconnection;
- synchronization;
- local operation.

 ### 8\. Critical events receive priority

 Critical information shall not be delayed unnecessarily by routine traffic.

 ### 9\. Communication supports privacy

 Local interpretation and data filtering reduce unnecessary transmission of raw information.

 ### 10\. Communication decisions remain measurable

 Range, latency, reliability, energy, security, scalability and recovery shall be experimentally evaluated.

---

 # 7.83 Key Engineering Principle

 The most important communication principle established by this chapter is:

 > **Communication failure must degrade communication capability before it degrades protection capability.**

 This principle has several practical consequences.

 If BLE fails:

 **local monitoring continues.**

 If cellular fails:

 **Edge processing continues and events are buffered.**

 If Cloud connectivity fails:

 **local and Edge functions continue.**

 If communication quality deteriorates:

 **routine traffic may be reduced while critical information remains prioritized.**

 If connectivity returns:

 **stored information is synchronized according to priority and integrity rules.**

 This converts communication resilience from an optional feature into a fundamental architectural property.

---

 # 7.84 Chapter 7 Conclusion

 Chapter 7 establishes the SSP communication architecture required to connect the Device, Edge/Mobile, Cloud and authorized-user layers.

 The baseline architecture is:

 **SSP Device → BLE → Mobile/Edge → Cellular/IP → Cloud → Secure Internet/API → Authorized User**

 with Wi-Fi available to the Mobile/Edge layer where appropriate.

 The Device–Edge link is designed around low-power local communication and therefore uses BLE as the baseline technology.

 The Edge–Cloud link is designed around secure wide-area IP communication, with cellular as the primary candidate and Wi-Fi as an alternative where suitable infrastructure exists.

 The architecture deliberately avoids making the wearable depend on continuous direct wide-area communication for every operational function.

 Instead, the Mobile/Edge layer provides:

 - aggregation;
- local processing;
- predictive assessment;
- communication prioritization;
- local storage;
- resilience.

 The communication architecture also establishes:

 - event prioritization;
- data minimization;
- secure device identity;
- authenticated communication;
- encryption and integrity;
- replay protection;
- store-and-forward behavior;
- recovery and synchronization;
- communication-state monitoring;
- scalability through Edge aggregation.

 The resulting design is therefore not simply:

 **Device → Internet → Cloud**

 but:

 **Sense locally → communicate efficiently → interpret locally → communicate according to priority → manage centrally.**

 This is consistent with the fundamental SSP architecture established in Chapter 5 and the hardware capabilities defined in Chapter 6.

 The detailed technologies and implementation parameters remain subject to subsequent engineering validation, particularly:

 - exact BLE configuration;
- selected cellular technology;
- radio modules;
- antenna implementation;
- application-layer protocol;
- message serialization;
- security protocol suite;
- communication energy profile;
- connection and retry parameters.

 The resulting design progression is now:

 **Requirements → Context → System Architecture → Hardware → Communication → Embedded Software → Data Architecture → Intelligence/AI → Energy & Performance → Cloud → PoC → Economic Analysis → Validation**

 The next chapter can therefore define the **SSP Embedded Software Architecture**, translating the Device hardware and communication architecture into firmware structure, operating states, event processing, power management, communication control, local decision logic and secure software lifecycle management.

---

 
