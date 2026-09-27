# Chapter 7 — Communication Architecture and Connectivity Design

 ## 7.1 Communication Requirements

 The communication architecture of SSP is derived from the requirements established in Chapter 3 and the Device–Edge/Mobile–Cloud architecture defined in Chapter 5.

 Communication is not treated simply as a mechanism for transporting sensor data. It is part of the operational behavior of the protection system and must therefore support:

 - timely delivery of critical events;
- low-power operation;
- secure information exchange;
- differentiated communication priority;
- temporary connectivity loss;
- local operation during communication disruption;
- controlled transmission of sensitive information;
- scalable fleet operation;
- configuration and management;
- recovery following communication failure.

 The communication design must therefore satisfy different requirements at different system boundaries.

 The principal communication paths are:

```
┌──────────────────┐
│   SSP Device     │
└────────┬─────────┘
         │
         │ BLE
         ▼
┌──────────────────┐
│  Mobile / Edge   │
└────────┬─────────┘
         │
         │ Cellular / IP
         ▼
┌──────────────────┐
│      Cloud       │
└────────┬─────────┘
         │
         │ Secure Internet / API
         ▼
┌──────────────────┐
│ Authorized User  │
└──────────────────┘
```

 The communication architecture therefore contains three principal external communication domains:

 1. **Device ↔ Edge/Mobile**
2. **Edge/Mobile ↔ Cloud**
3. **Cloud ↔ Authorized User**

 Each domain has different requirements.

 For example, the Device ↔ Edge link is strongly constrained by energy consumption and local range, while the Edge/Mobile ↔ Cloud link must prioritize wide-area availability and operational resilience.

 This leads to the following design principle:

 > **A single communication technology should not be assumed to be optimal for every SSP communication layer.**

---

 ## 7.2 Device-Level Communication

 The SSP device contains sensors, processing resources, memory, power-management circuitry and communication interfaces.

 Communication at this level can be divided into two categories:

 ### Internal device communication

 Internal sensors and peripherals communicate with the MCU/SoC through appropriate low-power interfaces.

 Candidate interfaces include:

 - I²C;
- SPI;
- UART;
- GPIO;
- ADC interfaces where required.

 These interfaces are primarily hardware integration mechanisms rather than network technologies.

 The exact interfaces will be selected in Chapter 6 according to the selected sensors and MCU/SoC.

 ### External device communication

 The wearable SSP device requires an external communication mechanism to exchange information with the Mobile/Edge layer.

 The principal candidate is **Bluetooth Low Energy (BLE)**.

 BLE is particularly suitable because the Device ↔ Mobile/Edge connection is:

 - relatively short range;
- low bandwidth compared with wide-area communication;
- energy constrained;
- frequently associated with a nearby smartphone or gateway;
- suitable for intermittent transmission;
- capable of supporting bidirectional communication.

 The device should therefore avoid continuously transmitting raw sensor information whenever the same operational objective can be achieved through local processing and transmission of structured information.

 For example:

```
Raw accelerometer samples
        ↓
Local processing
        ↓
Movement state
        ↓
Relevant event
        ↓
BLE transmission
```

 This reduces both communication volume and energy consumption.

---

 # 7.3 Device → Edge Communication

 The Device → Edge/Mobile link is the first major communication boundary in SSP.

 The baseline architecture selects **BLE as the primary local wireless technology**.

```
┌───────────────────┐
│ SSP wearable      │
│                   │
│ Sensors           │
│ MCU/SoC           │
│ Local processing  │
└─────────┬─────────┘
          │
          │ BLE
          ▼
┌───────────────────┐
│ Mobile / Edge     │
│                   │
│ Gateway           │
│ Local intelligence│
│ Connectivity      │
└───────────────────┘
```

 The Mobile/Edge device acts as a communication gateway as well as a local processing platform.

 This provides several advantages.

 ### Energy

 The wearable does not need to maintain a continuous wide-area cellular connection for every routine sensor measurement.

 ### Processing

 The device can transmit processed information rather than all raw sensor streams.

 ### Connectivity

 The smartphone or Edge device can provide access to wide-area networks without requiring every function to be implemented directly on the wearable.

 ### User interaction

 The Mobile/Edge layer can also provide a local interface for authorized interaction, configuration and status information where appropriate.

 ### Resilience

 Temporary cloud or cellular failures do not necessarily prevent the Device and Mobile/Edge layers from continuing local operation.

 The BLE link should therefore be treated as an **important local communication channel**, but not as the sole basis for system protection.

---

 ## 7.4 Edge → Cloud Communication

 The Edge/Mobile layer provides the bridge between local SSP operation and centralized cloud services.

 The baseline architecture uses **cellular/IP connectivity** as the primary wide-area communication mechanism for the Mobile/Edge layer.

```
SSP Device
    │
   BLE
    │
    ▼
Mobile / Edge
    │
    │ Cellular / IP
    ▼
Cloud
```

 The use of cellular connectivity at this layer provides wide-area mobility without requiring the SSP deployment to depend on a specific local Wi-Fi infrastructure.

 The Mobile/Edge layer can therefore operate across different environments while using the available cellular network for cloud connectivity.

 The communication pattern should be policy-driven rather than equivalent for all data.

 For example:

 | Information | Communication priority |
| --- | --- |
| Routine device status | Normal |
| Battery warning | Elevated |
| Connectivity degradation | Elevated |
| Geofence approach | High |
| High-risk event | Critical |
| Tamper event | Critical |
| Configuration update | Controlled |
| Historical bulk data | Low/background |

This supports the adaptive communication requirement defined in Chapter 3.

---

 ## 7.5 Cloud → User Communication

 The final communication boundary connects the cloud platform to authorized users.

 The principal users are protection operators, administrators and other authorized personnel defined in Chapter 2.

 The communication path is:

```
Cloud
  │
  ├── HTTPS/API
  │
  ├── Real-time event channel
  │
  └── Notification services
          │
          ▼
     Authorized User
```

 The cloud should not expose the underlying device communication mechanisms directly to the operator.

 Instead, the cloud provides an abstraction layer that presents:

 - current device status;
- location information;
- risk state;
- event history;
- alerts;
- connectivity status;
- battery status;
- configuration state.

 This separation is important because it prevents the operational interface from becoming tightly coupled to the underlying communication technology.

 A protection operator therefore interacts with the **SSP service**, not directly with BLE, cellular or device-specific protocols.

---

 # 7.6 BLE / Wi-Fi / Cellular / LoRa / Other Candidates

 Several communication technologies could theoretically participate in SSP.

 They are not equivalent because they operate at different ranges, consume different amounts of energy and require different infrastructure.

 ## BLE

 BLE is the principal candidate for the Device → Mobile/Edge connection.

 Its main advantages are:

 - low power consumption;
- short-range operation;
- broad smartphone support;
- suitable data rates for SSP event/status information;
- mature ecosystem;
- relatively low implementation complexity.

 Its principal limitation is range. BLE is therefore not selected as the primary wide-area communication mechanism.

 ### SSP decision

 **BLE → selected for Device ↔ Mobile/Edge communication.**

---

 ## Wi-Fi

 Wi-Fi provides substantially higher bandwidth than required for most SSP wearable data.

 Its advantages include:

 - high data throughput;
- widespread infrastructure;
- IP connectivity;
- convenient development and testing.

 However, continuous Wi-Fi operation is generally less attractive for a battery-powered wearable than BLE.

 Wi-Fi also assumes the availability of suitable local infrastructure.

 ### SSP decision

 **Wi-Fi → optional Mobile/Edge connectivity and development/offload mechanism, but not the primary wearable protection link.**

 This distinction is important.

 Wi-Fi may be useful for the smartphone or Edge gateway without requiring the wearable itself to depend on Wi-Fi.

---

 ## Cellular

 Cellular communication provides the principal wide-area connectivity mechanism.

 Its advantages include:

 - broad geographic coverage;
- mobility;
- direct Internet connectivity;
- no dependence on customer Wi-Fi infrastructure;
- suitability for geographically distributed deployments.

 Its disadvantages include:

 - energy consumption;
- subscription/connectivity costs;
- variable coverage;
- dependence on network infrastructure;
- additional communication hardware where implemented directly on the device.

 ### SSP decision

 **Cellular/IP → selected as the primary Edge/Mobile → Cloud connectivity mechanism.**

 The precise cellular technology should be selected during detailed hardware and deployment engineering based on the required coverage, latency, availability, power consumption and commercial conditions.

---

 ## LoRa / LPWAN

 LPWAN technologies such as LoRaWAN can provide:

 - long range;
- relatively low energy consumption;
- small-message communication.

 They can therefore be attractive for low-rate telemetry.

 However, SSP is not simply a periodic telemetry system.

 Critical events may require:

 - bidirectional communication;
- timely delivery;
- broad geographic mobility;
- reliable infrastructure availability;
- integration with a mobile Edge layer.

 A private LoRaWAN deployment would additionally introduce gateway infrastructure and coverage-management requirements.

 ### SSP decision

 **LPWAN → not selected as the baseline communication mechanism for the primary SSP architecture.**

 It remains a possible alternative for specific fixed or infrastructure-supported deployments.

---

 # 7.7 WBAN / WPAN / WLAN / LPWAN Considerations

 The SSP communication architecture can be understood using several networking categories.

 ### WBAN

 A wearable-body-area network could be relevant when several physiological or wearable sensors are integrated around the monitored person.

 The initial SSP architecture does not require a complex multi-sensor WBAN.

 The wearable device instead acts as an integrated sensing node.

 ### WPAN

 The Device ↔ Mobile/Edge relationship is primarily a short-range personal-area communication problem.

 BLE is therefore the principal technology in this domain.

 ### WLAN

 Wi-Fi belongs primarily to the local-area networking domain.

 It may provide connectivity for the Mobile/Edge device where infrastructure is available but is not the fundamental wearable communication mechanism.

 ### LPWAN

 LPWAN can support low-data-rate distributed telemetry but is not selected as the baseline for SSP because the system requires more flexible mobile connectivity and bidirectional operational communication.

 ### WAN / Cellular

 Cellular connectivity provides the principal wide-area link between the Mobile/Edge layer and Cloud.

 The resulting hierarchy is therefore:

```
Wearable / WPAN
       │
      BLE
       │
       ▼
 Mobile / Edge
       │
 Cellular / WAN
       │
       ▼
     Cloud
       │
 Internet / API
       │
       ▼
 Authorized User
```

---

 # 7.8 Protocol Comparison

 The principal alternatives can be compared against the SSP requirements.

 | Technology | Range | Bandwidth | Energy suitability | Mobility | Infrastructure dependence | SSP role |
| --- | --- | --- | --- | --- | --- | --- |
| BLE | Short | Low/medium | High | Good locally | Low | **Primary Device ↔ Edge** |
| Wi-Fi | Local | High | Medium/low for wearable | Limited by infrastructure | High | Optional Edge connectivity |
| Cellular | Wide | Medium/high depending on technology | Medium | High | Operator network | **Primary Edge ↔ Cloud** |
| LoRaWAN | Wide | Low | High | Deployment dependent | Gateway/network required | Alternative for selected deployments |
| Ethernet | Local/fixed | High | Not suitable for wearable | Very low | Physical infrastructure | Fixed infrastructure only |
| NFC | Very short | Very low | Very high | Very limited | Low | Provisioning/identification possibilities |

The selection is therefore not based on a single parameter.

 The decision must consider the combined requirement:

 > **Range + bandwidth + latency \+ energy + mobility + infrastructure \+ reliability + security \+ cost**

 For the baseline SSP deployment, this leads to:

 **BLE for local wearable connectivity + cellular/IP for wide-area connectivity.**

---

 # 7.9 Selected Communication Architecture

 The baseline SSP communication architecture is therefore frozen as:

```
                         ┌───────────────────┐
                         │ Authorized User   │
                         │ Operator/Admin    │
                         └─────────▲─────────┘
                                   │
                            HTTPS / API /
                         real-time events
                                   │
                         ┌─────────┴─────────┐
                         │      Cloud        │
                         │                  │
                         │ Event processing │
                         │ Storage          │
                         │ Analytics        │
                         │ Management       │
                         └─────────▲─────────┘
                                   │
                            Cellular / IP
                                   │
                         ┌─────────┴─────────┐
                         │   Mobile / Edge   │
                         │                  │
                         │ Local processing │
                         │ Gateway          │
                         │ Buffering        │
                         │ Risk assessment  │
                         └─────────▲─────────┘
                                   │
                                  BLE
                                   │
                         ┌─────────┴─────────┐
                         │    SSP Device     │
                         │                  │
                         │ Sensors          │
                         │ MCU/SoC          │
                         │ Local decisions  │
                         │ Power management │
                         └───────────────────┘
```

 The resulting communication chain is:

 > **Device → BLE → Mobile/Edge → Cellular/IP → Cloud → Secure API → Authorized User**

 This is the baseline communication architecture for the remainder of the project.

 The architecture deliberately separates **local communication** from **wide-area communication**.

 This separation permits each communication layer to be optimized for its actual purpose.

---

 ## 7.10 Security

 Communication security is an end-to-end requirement.

 The architecture shall protect communication against:

 - unauthorized device participation;
- unauthorized users;
- interception;
- message modification;
- replay;
- credential theft;
- unauthorized configuration;
- compromised communication endpoints.

 ### Device ↔ Mobile/Edge

 The BLE connection shall use authenticated pairing and appropriate link-layer security.

 Application-level authorization should additionally ensure that possession of a BLE connection does not automatically imply permission to access SSP functions.

 ### Mobile/Edge ↔ Cloud

 The wide-area connection shall use authenticated and encrypted IP communication.

 The Edge/Mobile device should authenticate itself to the SSP backend using credentials appropriate to the deployment model.

 ### Cloud ↔ User

 User communication shall use secure application protocols and authenticated user sessions.

 Authorization must be enforced independently of authentication.

 For example:

```
Authentication
      ↓
Who is the user/device?
      ↓
Authorization
      ↓
What may this user/device do?
      ↓
Data access
```

 This is particularly important because SSP handles sensitive location and operational information.

---

 # 7.11 Communication Failure Modes

 Communication failures are expected engineering conditions and must therefore have defined behavior.

 ## 7.11.1 BLE connection loss

 If the Device loses its BLE connection to the Mobile/Edge layer:

```
BLE loss
   ↓
Device detects communication failure
   ↓
Local monitoring continues
   ↓
Events buffered locally where appropriate
   ↓
Reconnection attempted
   ↓
Connection restored
   ↓
Relevant information synchronized
```

 The exact fallback behavior depends on the final hardware configuration.

 The important architectural principle is that loss of BLE should not automatically terminate local sensing or event detection.

---

 ## 7.11.2 Cellular connectivity loss

 If the Mobile/Edge layer loses cellular connectivity:

```
Cellular loss
      ↓
Connectivity degradation detected
      ↓
Local/Edge functions continue
      ↓
Critical information retained
      ↓
Reconnection attempts
      ↓
Connectivity restored
      ↓
Buffered information synchronized
```

 Communication priority becomes important in this situation.

 Critical information should be preserved preferentially over routine telemetry.

---

 ## 7.11.3 Cloud service interruption

 A temporary cloud outage should not necessarily disable Device or Mobile/Edge monitoring.

 The system should continue locally for as long as the available resources and operational policy permit.

```
Cloud unavailable
       ↓
Edge continues local operation
       ↓
Events retained
       ↓
Cloud availability restored
       ↓
Synchronization
       ↓
Normal operation
```

 This directly implements the resilience requirement from Chapter 3.

---

 ## 7.11.4 Degraded communication quality

 Communication quality may degrade without completely failing.

 The system should therefore distinguish between:

 - normal connectivity;
- degraded connectivity;
- intermittent connectivity;
- unavailable connectivity.

 This information can influence:

 - transmission frequency;
- message prioritization;
- local buffering;
- monitoring intensity;
- retry behavior.

---

 ## 7.11.5 Communication recovery

 Recovery should not simply restart normal communication without checking the state of the system.

 After recovery, SSP should:

 1. authenticate the connection;
2. determine the last successfully synchronized state;
3. transmit prioritized buffered information;
4. resolve duplicate messages where necessary;
5. update cloud state;
6. return to normal communication policy.

 This is particularly important for event integrity and auditability.

---

 # 7.12 Communication Prioritization and Adaptive Operation

 Communication in SSP is deliberately **policy-aware**.

 The system should not treat all information equally.

 A conceptual policy is:

```
                 Operational state
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
        Normal        Elevated       Critical
          │              │              │
          ▼              ▼              ▼
      Low-rate        Increased       Immediate
      telemetry       reporting       reporting
          │              │              │
          ▼              ▼              ▼
       Energy         Higher          Highest
       optimized      priority        priority
```

 This provides an important connection between Chapters 7 and 11.

 Communication behavior contributes directly to energy consumption.

 Therefore:

 > **Communication policy is part of SSP energy management, not merely a networking decision.**

 Similarly, communication priority is connected to the risk-assessment architecture.

 A critical event should not be delayed simply because the system is operating in a low-power state.

---

 # 7.13 Communication Architecture Decision Summary

 The communication decisions established in this chapter are summarized below.

 | Decision | Selection | Rationale |
| --- | --- | --- |
| Device → Edge | **BLE** | Low energy, short-range, smartphone/Edge compatibility |
| Edge → Cloud | **Cellular/IP** | Wide-area mobility and infrastructure independence |
| Edge local connectivity | **Wi-Fi optional** | Useful where available, but not fundamental to protection |
| Cloud → User | **Secure Internet/API communication** | Decouples users from device-level technologies |
| Primary LPWAN | **Not baseline** | Less appropriate for the mobile, bidirectional baseline architecture |
| Raw-data transmission | **Minimized** | Energy, bandwidth and privacy |
| Critical-event communication | **High priority** | Operational latency |
| Temporary communication loss | **Local/Edge fallback** | Resilience |
| Recovery | **Buffered synchronization** | Event preservation |
| Security | **End-to-end authenticated/encrypted communication** | Protection of sensitive information |

The resulting architecture can therefore be summarized as:

 > **BLE provides the low-power local Device ↔ Edge connection, while cellular/IP provides the wide-area Edge ↔ Cloud connection. Secure application-layer communication connects the Cloud to authorized users.**

---

 # 7.14 Relationship to Previous Chapters

 Chapter 7 does not introduce these decisions independently.

 The design chain is:

```
Chapter 3
Requirements
     ↓
Chapter 4
Technology/context analysis
     ↓
Chapter 5
Device–Edge/Mobile–Cloud architecture
     ↓
Chapter 6
Hardware constraints
     ↓
Chapter 7
Communication selection
```

 Several earlier requirements directly influence the communication design.

 | Earlier decision/requirement | Communication consequence |
| --- | --- |
| Distributed Device–Edge–Cloud architecture | Multiple communication boundaries are required |
| Low-power wearable | BLE preferred for local device communication |
| Mobile/Edge intelligence | Device does not need to transmit all raw data |
| Wide-area monitoring | Cellular/IP required for baseline deployment |
| Privacy-aware processing | Minimize transmitted information |
| Adaptive monitoring | Communication frequency can change with state |
| Critical-event response | Priority communication required |
| Connectivity resilience | Local buffering and fallback required |
| Security by design | Authenticated and encrypted communication |
| Scalability | Cloud-facing communication must support fleet growth |

This maintains the traceability principle established in Chapter 3:

 > **Requirement → Architecture decision → Communication technology → KPI → Validation**

---

 # 7.15 Chapter 7 Conclusion

 The SSP communication architecture is based on the principle that different communication layers have different engineering objectives.

 The resulting baseline is:

 **SSP Device → BLE → Mobile/Edge → Cellular/IP → Cloud → Secure API → Authorized User**

 BLE is used for low-power local communication between the wearable device and the Mobile/Edge layer. Cellular/IP provides the primary wide-area connection between the Mobile/Edge layer and the Cloud. Wi-Fi remains an optional connectivity mechanism for the Mobile/Edge environment rather than a fundamental dependency of the wearable protection function.

 The architecture also establishes several important operational principles:

 - communication is policy-aware;
- information is transmitted according to operational necessity;
- critical events receive higher communication priority;
- local and Edge processing reduce unnecessary communication;
- temporary communication loss does not automatically terminate monitoring;
- important events can be buffered and synchronized after recovery;
- security applies across all communication boundaries.

 The communication design therefore supports the broader SSP principle:

 > **Sense locally → interpret locally where appropriate → communicate according to operational significance → analyze centrally where beneficial → inform authorized users securely.**
