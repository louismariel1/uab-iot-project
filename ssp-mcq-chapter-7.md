# SSP Chapter 7 — includes the key concepts, explanations, worked answers, assessment questions, and model answers needed to test Answer-Included Study & Assessment
---

 # 7.1 Purpose of This Study Chapter

 Chapter 7 establishes how information moves through SSP:

 **Device → Edge/Mobile → Cloud → Authorized User**

 The central communication architecture is:

 **SSP Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ User**

 with Wi-Fi available to the Mobile/Edge layer where appropriate.

 The most important lesson is that SSP communication is **not simply a question of selecting the fastest wireless technology**.

 Communication decisions must balance:

 - range;
- latency;
- energy consumption;
- reliability;
- availability;
- security;
- mobility;
- infrastructure requirements;
- scalability;
- cost;
- resilience during communication failures.

 The chapter therefore treats communication as an **engineering subsystem of the overall cyber-physical architecture**.

---

 # 7.2 Core Communication Concept

 A useful way to understand SSP is to separate the communication system into four major links.

```
┌──────────────────┐
│   SSP Device     │
│                  │
│ Sensors / MCU    │
└────────┬─────────┘
         │
       BLE
         │
         ▼
┌──────────────────┐
│  Mobile / Edge   │
│                  │
│ Fusion / Risk    │
└────────┬─────────┘
         │
     Cellular/IP
         │
         ▼
┌──────────────────┐
│      Cloud       │
│                  │
│ Storage / Mgmt   │
└────────┬─────────┘
         │
    Secure Internet
         │
         ▼
┌──────────────────┐
│ Authorized User  │
└──────────────────┘
```

 Each link has a different engineering purpose.

 ### Answer

 - **Device → Edge:** low-power local communication.
- **Edge → Cloud:** wide-area network communication.
- **Cloud → User:** secure application-level communication.
- **Internal device interfaces:** communication between sensors, processor, storage, radios and security hardware.

 A major design principle is therefore:

 > **Different communication links should be optimized for different functions rather than forced to use one technology everywhere.**

---

 # 7.3 Communication Requirements

 The communication architecture derives its requirements from Chapters 3 and 5.

 | Requirement | SSP implication |
| --- | --- |
| Range | Device communication must cover the intended operating environment |
| Low latency | Critical events require priority transmission |
| Low energy | Wearable communication must avoid unnecessary radio activity |
| Reliability | Important events should have controlled delivery and retry mechanisms |
| Availability | Communication must tolerate temporary network disruption |
| Security | Device identity and data must be protected |
| Scalability | Many devices must communicate without redesigning the architecture |
| Mobility | Users and devices may move continuously |
| Cost | Radio hardware and network services must remain economically practical |
| Resilience | Local protection functions must continue during communication failures |

### Assessment Question

 **Q1. Why is communication energy particularly important for a wearable SSP device?**

 ### Answer

 A wearable device has limited battery capacity. Wireless communication can consume significant energy, particularly when radios are repeatedly activated, scanning continuously or transmitting over a wide-area network.

 Therefore, SSP should avoid unnecessary communication and use:

 - scheduled communication;
- event-driven transmission;
- data aggregation;
- priority-based transmission;
- local processing;
- low-power radio modes.

 The objective is not simply to minimize communication. It is to **minimize unnecessary communication while preserving required protection functions**.

---

 # 7.4 Range

 Range describes the physical distance over which a communication technology can maintain an operational connection.

 SSP has different range requirements at different architectural levels.

 ### Device → Edge

 Usually requires relatively short-range communication.

 ### Edge → Cloud

 Requires wide-area connectivity.

 ### Cloud → User

 Uses Internet/application connectivity rather than a local radio link.

 The distinction can be represented as:

```
Short range
Device ───────── Edge

                 │

             Wide area
                 │
                 ▼

              Cloud
                 │
                 │
              Internet
                 │
                 ▼
               User
```

 ### Assessment Question

 **Q2. Why would using cellular communication directly from every wearable device potentially be less attractive than using BLE to a Mobile/Edge device?**

 ### Answer

 Direct cellular communication can provide wide-area connectivity but may increase:

 - device energy consumption;
- hardware complexity;
- antenna requirements;
- module cost;
- network-service requirements;
- thermal and mechanical constraints.

 BLE allows the wearable to use a lower-power local link while the Mobile/Edge device provides the more demanding wide-area connection.

 This is one reason the Chapter 7 baseline uses:

 **Device ↔ BLE ↔ Mobile/Edge**

 rather than making direct cellular connectivity mandatory for every wearable.

---

 # 7.5 Latency

 Latency is the time between information becoming available and the corresponding information reaching the required processing or response point.

 SSP should requirements without providing meaningful benefit if SSP primarily transmits distinguish between:

 ### Local latency

```
Sensor
 ↓
MCU
 ↓
Local event
```

 ### Edge latency

```
Device
 ↓
BLE
 ↓
Edge
 ↓
Risk assessment
```

 ### Cloud latency

```
Device
 ↓
Edge
 ↓
Cellular/IP
 ↓
Cloud
 ↓
Application
```

 For a critical event, the system should avoid unnecessary processing stages.

 ### Assessment Question

 **Q3. Why should critical-event communication be evaluated separately from routine status communication?**

 ### Answer

 Routine status information can often tolerate some delay.

 A critical event may require rapid operational response.

 If both types of information use exactly the same communication priority, routine traffic could compete with time-sensitive information.

 SSP therefore establishes communication classes such as:

 - routine;
- contextual;
- elevated;
- critical.

 Critical information receives higher communication priority.

---

 # 7.6 Bandwidth

 Bandwidth represents the amount of information that can be transferred over a communication channel.

 SSP does not generally require continuous transmission of large raw sensor datasets.

 Instead, local processing can transform raw information into structured events.

 For example:

```
Raw acceleration samples
        ↓
Local processing
        ↓
Motion state
        ↓
Structured event
```

 Instead of sending:

```
Thousands of raw measurements
```

 SSP may send:

```
Device ID
Timestamp
Motion state
Position
Position confidence
Event type
Severity
```

 This is a major architectural advantage.

 ### Assessment Question

 **Q4. Does SSP need maximum possible bandwidth?**

 ### Answer

 No.

 The objective is **sufficient bandwidth for the operational information being transmitted**.

 Higher bandwidth can increase hardware, infrastructure or energy requirements without providing meaningful benefit if SSP primarily transmits compact structured events.

 Bandwidth requirements should therefore be derived from:

 - event frequency;
- payload size;
- number of devices;
- synchronization requirements;
- diagnostic traffic;
- software/model updates.

---

 # 7.7 Energy

 Communication energy can be considered approximately as:

 $$
E_{comm}=P_{radio}\times t_{active}
$$

 where:

 - $E_{comm}$ = communication energy;
- $P_{radio}$ = radio power;
- $t_{active}$ = active communication time.

 This simple relationship demonstrates why communication optimization can involve both:

 - reducing radio power;
- reducing radio active time.

 For example, transmitting a compact event may reduce energy compared with continuously transmitting raw measurements.

---

 # 7.8 Communication Duty Cycle

 A radio does not necessarily need to remain active continuously.

 A simplified model is:

 $$
D=\frac{t_{active}}{T}
$$

 where:

 - $D$ = duty cycle;
- $t_{active}$ = active radio time;
- $T$ = observation period.

 Lower duty cycle generally provides opportunities for lower average energy consumption, although the actual result depends on the technology and operating mode.

 ### Example

 Suppose a BLE subsystem is active for 2 seconds every 60 seconds.

 $$
D=\frac{2}{60}=0.0333
$$

 Therefore:

 $$
D\approx3.33\%
$$

 This is very different from keeping the radio continuously active.

 ### Assessment Question

 **Q5. Why might continuous proximity scanning be undesirable on a battery-powered wearable?**

 ### Answer

 Continuous scanning increases radio activity and therefore energy consumption.

 SSP should instead determine whether:

 - periodic discovery;
- event-triggered scanning;
- scheduled scanning;
- adaptive scanning;

 can provide sufficient operational information with lower energy consumption.

---

 # 7.9 Reliability

 Reliability describes the ability of communication to successfully deliver information when required.

 A communication architecture should not assume:

 > "If the radio is available, every message will always arrive."

 Real systems experience:

 - interference;
- fading;
- obstruction;
- congestion;
- mobility;
- temporary network loss;
- device failure;
- gateway failure.

 SSP therefore needs communication mechanisms such as:

 - acknowledgement where appropriate;
- retry;
- buffering;
- sequence numbers;
- timestamps;
- duplicate detection;
- synchronization;
- prioritization.

---

 # 7.10 Availability

 Availability asks whether the communication service is accessible when required.

 This is different from reliability.

 A system can have a reliable communication protocol but still experience low availability if the underlying network is unavailable.

 For example:

```
Reliable protocol
        +
No cellular coverage
        ↓
Communication unavailable
```

 SSP therefore separates communication availability from local protection capability.

---

 # 7.11 BLE

 Bluetooth Low Energy (BLE) is a principal candidate for the Device → Edge/Mobile connection.

 Its architectural advantages include:

 - relatively low power consumption;
- widespread support in mobile devices;
- suitability for short-range communication;
- device discovery and association mechanisms;
- support for proximity-related applications;
- mature ecosystem.

 Its limitations include:

 - relatively short communication range compared with cellular;
- dependence on the Mobile/Edge device for wider-area connectivity in the baseline architecture;
- radio-environment sensitivity;
- limitations compared with technologies designed specifically for long-range communication.

 ### Assessment Question

 **Q6. What is the principal role of BLE in the SSP baseline architecture?**

 ### Answer

 BLE provides the primary local wireless communication path between the SSP wearable/device and the Mobile/Edge layer.

 It can support:

 - device association;
- local status;
- event transmission;
- proximity information;
- configuration;
- diagnostics.

---

 # 7.12 Wi-Fi

 Wi-Fi provides substantially greater local network capability than BLE and is widely available in many environments.

 However, SSP does not use Wi-Fi as the fundamental wearable protection link.

 Wi-Fi can be useful for the **Mobile/Edge layer**, particularly when the Edge device has access to local infrastructure.

 For example:

```
SSP Device
    │
   BLE
    │
    ▼
Mobile / Edge
    │
  Wi-Fi
    │
    ▼
Local network / Internet
    │
    ▼
Cloud
```

 This can be useful in environments where Wi-Fi is available.

 However, a wearable should not necessarily depend on Wi-Fi infrastructure for fundamental protection because:

 - coverage may be incomplete;
- the user may move outside coverage;
- Wi-Fi association consumes resources;
- infrastructure configuration may vary;
- public or uncontrolled networks introduce additional security considerations.

 ### Assessment Question

 **Q7. Is Wi-Fi rejected completely by SSP?**

 ### Answer

 No.

 Wi-Fi is available as an option for the Mobile/Edge layer where appropriate.

 The important architectural decision is that **Wi-Fi is not the fundamental protection link for the wearable**.

---

 # 7.13 Cellular

 Cellular communication is the primary candidate for the Edge → Cloud wide-area connection.

 Its principal advantages include:

 - broad geographic coverage;
- mobility support;
- IP connectivity;
- mature infrastructure;
- suitability for mobile systems.

 Potential disadvantages include:

 - subscription/service cost;
- energy consumption;
- dependence on network availability;
- modem and antenna requirements;
- regional coverage variation;
- certification and regulatory requirements.

 In the baseline architecture, cellular connectivity is primarily associated with the Mobile/Edge layer.

---

 # 7.14 Direct Cellular on the SSP Device

 Direct cellular communication remains technically possible.

 The Mobile/Edge layer is more significant because it may remove local predictive processing and the primary local communication Edge has greater computational, energy and physical resources than the wearable and can therefore act as the wide-area communication gateway where the system will define how the Device and Edge actually process, represent, prioritize and architecture should not imply that direct cellular is universally unsuitable.

 It may become appropriate when:

 - the device must operate independently of a smartphone;
- the deployment requires autonomous wide-area connectivity;
- the additional battery capacity is acceptable;
- network coverage is adequate;
- hardware cost is justified.

 The engineering decision should therefore depend on deployment requirements.

 ### Assessment Question

 **Q8. What is the principal architectural trade-off of direct cellular on the wearable?**

 ### Answer

 It provides greater communication independence but can increase:

 - power consumption;
- hardware complexity;
- physical size;
- cost;
- antenna requirements;
- thermal requirements.

 Therefore it is a deployment-dependent option rather than the fundamental baseline assumption.

---

 # 7.15 LoRa and LPWAN Technologies

 Long-range, low-power technologies such as LoRa-based systems can be attractive for certain IoT deployments.

 Their advantages may include:

 - long communication range;
- low-power operation;
- suitability for small data payloads;
- potential usefulness in dedicated deployments.

 However, they generally depend on appropriate gateway infrastructure and are not inherently equivalent to cellular connectivity.

 For SSP, their suitability depends strongly on the deployment environment.

 They may be considered when:

 - the deployment controls its own infrastructure;
- data volume is low;
- latency requirements are compatible;
- geographic coverage can be guaranteed.

 They become less attractive when SSP requires ubiquitous mobile connectivity without dedicated infrastructure.

---

 # 7.16 Technology Landscape

 A conceptual comparison is:

 | Technology | Typical role in SSP | Range | Energy | Bandwidth | Infrastructure |
| --- | --- | --- | --- | --- | --- |
| BLE | Device → Edge | Short | Low | Moderate | Mobile/Edge device |
| Wi-Fi | Edge connectivity | Local | Moderate | High | Wi-Fi infrastructure |
| Cellular | Edge → Cloud | Wide-area | Higher | High | Operator network |
| LoRa/LPWAN | Specialized deployments | Long | Low | Low | Gateways/network |
| Direct cellular | Autonomous device | Wide-area | Higher | High | Operator network |

These values are qualitative architectural comparisons rather than final engineering measurements.

 Actual performance depends on:

 - implementation;
- environment;
- configuration;
- network conditions;
- antenna;
- duty cycle;
- protocol behavior.

---

 # 7.17 WBAN, WPAN, WLAN and LPWAN

 Communication technologies can also be understood through networking categories.

 ### WBAN — Wireless Body Area Network

 Designed for communication around or on the human body.

 SSP can potentially use WBAN concepts for wearable sensing.

 ### WPAN — Wireless Personal Area Network

 Covers short-range personal communication.

 BLE fits naturally into this category.

 ### WLAN — Wireless Local Area Network

 Provides local network connectivity.

 Wi-Fi is the principal example.

 ### LPWAN — Low-Power Wide-Area Network

 Designed for long-range, low-power communication with relatively small data volumes.

 LoRa-based systems are an example.

 ### Cellular WAN

 Provides wide-area mobile connectivity through operator infrastructure.

 The SSP baseline uses cellular primarily at the Edge → Cloud boundary.

---

 # 7.18 Assessment: Network Category Mapping

 **Q9. Classify the following technologies:**

 1. BLE
2. Wi-Fi
3. LoRa-based LPWAN
4. Cellular

 ### Answer

 1. **BLE:** primarily WPAN/short-range personal communication.
2. **Wi-Fi:** WLAN.
3. **LoRa-based systems:** LPWAN.
4. **Cellular:** wide-area mobile network.

 The important lesson is that these technologies solve different networking problems.

---

 # 7.19 Protocol Layers

 SSP communication should not be described only in terms of radio technologies.

 A complete communication architecture includes several layers.

 A simplified model is:

```
Application
    │
Message / Event format
    │
Security
    │
Transport
    │
IP networking
    │
Link / Radio
    │
Physical environment
```

 For example, the Edge may communicate with the Cloud through:

```
SSP Event
   ↓
Application protocol/API
   ↓
Secure transport
   ↓
IP
   ↓
Cellular or Wi-Fi
```

 This distinction is important because **radio technology and application protocol are different design decisions**.

---

 # 7.20 Device Internal Communication

 Not all SSP communication is wireless.

 The device itself contains several internal communication paths.

 Examples include:

 - MCU ↔ IMU;
- MCU ↔ GNSS;
- MCU ↔ secure element;
- MCU ↔ storage;
- MCU ↔ radio;
- power-management IC ↔ MCU.

 Potential buses include:

 - I²C;
- SPI;
- UART;
- GPIO;
- USB where required.

 These interfaces are hardware communication interfaces rather than external networking technologies.

 ### Assessment Question

 **Q10. Why should sensor buses not be confused with Device → Edge communication?**

 ### Answer

 Sensor buses connect components **inside the device**.

 Device → Edge communication transfers information **between separate computing systems**.

 For example:

```
IMU ──SPI──► MCU ──BLE──► Smartphone
```

 SPI is an internal hardware interface.

 BLE is an external wireless communication interface.

---

 # 7.21 Device → Edge Communication

 This is one of the most important communication links in SSP.

 The baseline architecture is:

```
SSP Device
    │
    │ BLE
    ▼
Mobile / Edge
```

 The Device should transmit information such as:

 - device status;
- selected position information;
- motion state;
- proximity information;
- structured events;
- battery state;
- tamper events;
- configuration responses.

 It does not need to continuously transmit every raw sensor measurement.

---

 # 7.22 Device → Edge Communication Modes

 Several operating modes can be defined.

 ### Association mode

 Used when a device establishes a relationship with an authorized Edge device.

 ### Periodic status mode

 Used for routine health and status reporting.

 ### Event-driven mode

 Used when an important event occurs.

 ### Elevated monitoring mode

 Used when SSP increases information exchange because risk or uncertainty has increased.

 ### Critical mode

 Used for urgent event transmission.

 This can be represented as:

```
Normal
  │
  ▼
Periodic communication
  │
  │ Event
  ▼
Elevated communication
  │
  │ Critical event
  ▼
Priority communication
```

---

 # 7.23 Edge → Cloud Communication

 The Edge → Cloud link is primarily a wide-area IP communication problem.

 The baseline architecture is:

```
Mobile / Edge
      │
      │ Cellular/IP
      ▼
    Cloud
```

 The communication system should support:

 - event synchronization;
- device status;
- configuration;
- policy updates;
- diagnostics;
- historical synchronization;
- software/model management where appropriate.

---

 # 7.24 Intermittent Connectivity

 Connectivity should not be assumed to be permanent.

 For example:

```
Edge
 │
 ├── Connected → Synchronize normally
 │
 └── Disconnected
          │
          ▼
     Local buffering
          │
          ▼
     Connectivity restored
          │
          ▼
       Resynchronize
```

 This requires:

 - local storage;
- timestamps;
- sequence identifiers;
- synchronization logic;
- duplicate handling;
- retry policies.

---

 # 7.25 Cloud → User Communication

 The Cloud → User interface is primarily an application/API problem.

 Operators may receive:

 - status;
- alerts;
- events;
- historical information;
- acknowledgements;
- device-health information;
- configuration information.

 The communication chain may be:

```
Cloud
  │
  ▼
Secure API / Application
  │
  ├── Web dashboard
  ├── Mobile application
  └── Authorized integration
```

 The user-facing system must enforce authentication and authorization.

---

 # 7.26 Communication Prioritization

 SSP divides information into conceptual communication classes.

 | Class | Example | Priority |
| --- | --- | --- |
| Routine | Battery/status | Normal |
| Contextual | Position/motion summary | Policy controlled |
| Elevated | Approach/proximity condition | High |
| Critical | Confirmed protection event | Highest |

The purpose is not simply to transmit critical information faster.

 It also helps control:

 - radio activation;
- network usage;
- battery consumption;
- congestion;
- cloud processing;
- operator attention.

---

 # 7.27 Example Communication Scenario

 Consider an SSP device approaching a protected boundary.

 ### Step 1 — Device sensing

 The device detects:

 - movement;
- position;
- position confidence.

 ### Step 2 — Device → Edge

 The relevant information is transmitted over BLE.

 ### Step 3 — Edge interpretation

 The Edge combines:

 - position;
- confidence;
- movement;
- geofence;
- context.

 ### Step 4 — Risk assessment

 The Edge estimates whether the trajectory indicates likely boundary interaction.

 ### Step 5 — Communication escalation

 The Edge increases communication priority if required.

 ### Step 6 — Cloud

 The event is synchronized with the Cloud.

 ### Step 7 — User

 An authorized operator receives the relevant alert.

 The complete chain is:

```
Sense
 ↓
Interpret
 ↓
BLE
 ↓
Edge
 ↓
Predict
 ↓
Assess
 ↓
Cellular/IP
 ↓
Cloud
 ↓
Secure API
 ↓
Authorized User
```

---

 # 7.28 Communication Security

 Communication security is an architectural requirement rather than an optional feature.

 The principal security properties are:

 ### Authentication

 Determine whether a communicating entity is authorized.

 ### Confidentiality

 Prevent unauthorized parties from reading protected information.

 ### Integrity

 Detect unauthorized modification.

 ### Replay protection

 Prevent old valid messages from being maliciously reused as if they were current.

 ### Authorization

 Determine what an authenticated entity is permitted to do.

 ### Key management

 Control creation, storage, rotation, revocation and lifecycle of cryptographic credentials.

---

 # 7.29 Mutual Authentication

 The SSP architecture should establish trust between communicating layers.

 Conceptually:

```
Device
  │
  │ Authenticate
  ▼
Edge
  │
  │ Authenticate
  ▼
Cloud
  │
  │ Authenticate
  ▼
Authorized User
```

 The exact protocol may vary by implementation.

 The architectural principle remains:

 > **Identity must be established before sensitive communication or management operations are trusted.**

---

 # 7.30 Encryption

 Sensitive communication should use appropriate cryptographic protection.

 For example:

```
Application data
       ↓
Encrypted transport
       ↓
Network
```

 Encryption protects confidentiality, but encryption alone does not guarantee that the communicating party is authorized.

 Therefore:

 **Encryption + authentication \+ authorization + integrity**

 must be considered together.

---

 # 7.31 Replay Protection

 Suppose an attacker captures an old valid event:

```
Event at 10:00
```

 and retransmits it later.

 If SSP accepts it as a new event, the system could incorrectly interpret historical information as current.

 Therefore event messages should use mechanisms such as:

 - timestamps;
- sequence numbers;
- nonces;
- freshness checks;
- authenticated message protection.

 ### Assessment Question

 **Q11. Why is encryption alone insufficient for SSP communication security?**

 ### Answer

 Encryption protects confidentiality but does not by itself establish:

 - who sent the message;
- whether the message was modified;
- whether the message is fresh;
- whether the sender is authorized to perform the requested action.

 SSP therefore requires a broader security architecture.

---

 # 7.32 Secure Provisioning

 A device must receive its identity and credentials in a controlled manner.

 A conceptual provisioning process is:

```
Manufacturing / Enrollment
          ↓
Secure identity
          ↓
Device registration
          ↓
Credential association
          ↓
Authorized deployment
```

 Provisioning should avoid uncontrolled distribution of shared credentials.

 Each device should have an identity that can be associated with:

 - device registration;
- configuration;
- software version;
- security state;
- deployment status.

---

 # 7.33 Key Lifecycle

 Cryptographic keys are not permanent assets that can simply be created once and ignored.

 A complete lifecycle includes:

```
Generate
   ↓
Provision
   ↓
Use
   ↓
Monitor
   ↓
Rotate / renew
   ↓
Revoke if necessary
   ↓
Retire
```

 This becomes particularly important in a fleet containing many devices.

---

 # 7.34 Communication Failure Model

 SSP explicitly considers communication failures.

 Important failure cases include:

 1. BLE loss.
2. Cellular loss.
3. Cloud connectivity loss.
4. Mobile/Edge failure.
5. Communication degradation.
6. Recovery after failure.

 The central principle is:

 > **Communication failure must degrade communication capability before it degrades protection capability.**

 This is one of the most important assessment statements in Chapter 7.

---

 # 7.35 BLE Failure

 Suppose the wearable loses BLE connectivity.

 The device should not immediately become functionally useless.

 Instead:

```
BLE loss
  ↓
Detect failure
  ↓
Continue local monitoring
  ↓
Store relevant events
  ↓
Attempt reconnection
  ↓
Restore communication
  ↓
Synchronize
```

 The exact behavior depends on the deployment.

 The key architectural principle is local continuity.

---

 # 7.36 Cellular Failure

 If the Edge loses cellular connectivity:

```
Cellular loss
     ↓
Edge remains operational
     ↓
Local events retained
     ↓
Local protection continues
     ↓
Retry / alternate connectivity
     ↓
Connectivity restored
     ↓
Synchronize
```

 Wi-Fi may provide an alternative path where available.

 However, Wi-Fi should not automatically be assumed to be available.

---

 # 7.37 Cloud Failure

 A Cloud outage should not automatically stop Device or Edge monitoring.

 For example:

```
Cloud unavailable
       ↓
Edge continues
       ↓
Local event assessment continues
       ↓
Events buffered
       ↓
Cloud restored
       ↓
Synchronization
```

 This demonstrates the importance of separating:

 **Operational authority**

 from

 **Operational continuity**.

---

 # 7.38 Mobile/Edge Failure

 The failure of the Mobile/Edge layer is more significant because it may remove local predictive processing and the primary local communication bridge.

 The system should therefore define deployment-specific fallback behavior.

 Possible options include:

 - Device local operation;
- local event buffering;
- alternate authorized Edge;
- direct wide-area communication where hardware supports it;
- degraded monitoring mode.

 The correct solution depends on the hardware and deployment scenario.

---

 # 7.39 Communication Degradation

 Communication does not always fail completely.

 It can gradually degrade.

 Examples include:

 - weak signal;
- increased packet loss;
- high latency;
- repeated retries;
- intermittent association.

 SSP should distinguish:

```
Good
 ↓
Degraded
 ↓
Poor
 ↓
Unavailable
```

 The system can then adapt its communication policy.

 For example:

 - reduce non-critical traffic;
- prioritize important events;
- increase local buffering;
- change retry behavior;
- postpone routine synchronization.

---

 # 7.40 Recovery and Synchronization

 When communication is restored, SSP should not simply transmit everything blindly.

 A controlled synchronization process should determine:

 - what events remain unsynchronized;
- which events are highest priority;
- whether duplicates exist;
- whether timestamps are valid;
- whether data retention limits have been reached.

 Conceptually:

```
Connectivity restored
        ↓
Identify unsynchronized data
        ↓
Prioritize
        ↓
Transmit
        ↓
Verify delivery
        ↓
Mark synchronized
```

---

 # 7.41 Communication Architecture Baseline

 The selected baseline architecture is:

```
┌───────────────────┐
│    SSP Device     │
│                   │
│ Sensors + MCU     │
└─────────┬─────────┘
          │
         BLE
          │
          ▼
┌───────────────────┐
│   Mobile / Edge   │
│                   │
│ Fusion + Risk     │
└─────────┬─────────┘
          │
     Cellular/IP
          │
          ▼
┌───────────────────┐
│       Cloud       │
│                   │
│ Management + Data │
└─────────┬─────────┘
          │
    Secure Internet
          │
          ▼
┌───────────────────┐
│ Authorized User   │
└───────────────────┘
```

 Wi-Fi can be used by the Mobile/Edge layer when suitable infrastructure is available.

 It is not the fundamental protection link for the wearable.

---

 # 7.42 Why BLE \+ Mobile/Edge?

 This architecture provides a useful division of responsibilities.

 ### Wearable

 Optimized for:

 - low energy;
- sensing;
- local processing;
- local event generation.

 ### Mobile/Edge

 Optimized for:

 - richer processing;
- sensor fusion;
- predictive assessment;
- wide-area connectivity;
- local resilience.

 ### Cloud

 Optimized for:

 - fleet management;
- historical analysis;
- centralized policies;
- storage;
- dashboards;
- large-scale processing.

 This division follows the architectural principle:

 > **Place each function at the lowest practical layer capable of satisfying its requirements.**

---

 # 7.43 Communication Decision Table

 | Decision | Status |
| --- | --- |
| BLE for Device → Mobile/Edge | **Selected baseline** |
| Wi-Fi for Mobile/Edge connectivity | **Available where appropriate** |
| Cellular/IP for Edge → Cloud | **Selected baseline** |
| Secure Internet/API for Cloud → User | **Selected baseline** |
| Direct cellular on wearable | **Deployment-dependent option** |
| LoRa/LPWAN | **Specialized/deployment-dependent option** |
| Raw continuous sensor transmission | **Not baseline** |
| Structured event transmission | **Selected** |
| Communication prioritization | **Selected** |
| Local buffering | **Selected** |
| Authentication | **Selected** |
| Encryption/integrity protection | **Selected** |
| Replay protection | **Required design principle** |
| Secure provisioning | **Selected** |

---

 # 7.44 Communication-to-Requirement Traceability

 | Chapter 3 requirement | Chapter 7 response |
| --- | --- |
| Low latency | Local/Edge processing and priority communication |
| Low energy | BLE, duty cycling, local processing |
| Reliable events | Buffering, retry, acknowledgement/synchronization |
| Communication resilience | Local fallback and offline operation |
| Position/motion information | Structured Device → Edge data |
| Adaptive monitoring | Policy-based communication intensity |
| Privacy | Data minimization and local processing |
| Security | Authentication, encryption, integrity |
| Scalability | Edge aggregation and Cloud architecture |
| Mobility | Cellular connectivity at Edge |
| Fleet management | Secure Cloud communication |
| Critical alerts | Priority event path |

---

 # 7.45 Communication KPIs

 Chapter 7 introduces measurable communication KPIs.

 ### Latency

 $$
L_{total}=L_{device}+L_{local}+L_{network}+L_{cloud}+L_{application}
$$

 The exact model will be refined during validation.

 ### Reliability

 Possible measures include:

 - successful delivery rate;
- packet loss;
- retry count;
- synchronization success.

 ### Availability

 Possible measures include:

 - communication availability;
- time unavailable;
- recovery time.

 ### Energy

 Possible measures include:

 - energy/event;
- average radio current;
- peak radio current;
- energy per transmitted byte.

 ### Data efficiency

 Possible measures include:

 - bytes/event;
- raw-data reduction;
- routine traffic volume;
- critical-event payload size.

---

 # 7.46 Worked KPI Example

 Assume:

 - 100 bytes/event;
- 60 events/day;
- 10 devices.

 Daily payload before protocol overhead:

 $$
100\times60\times10=60,000\text{ bytes/day}
$$

 Therefore:

 $$
60,000\text{ bytes}\approx58.6\text{ KiB/day}
$$

 This is a simplified payload calculation.

 Actual network traffic will be larger because of:

 - protocol headers;
- encryption/authentication overhead;
- acknowledgements;
- retries;
- synchronization;
- diagnostics.

 ### Lesson

 Payload volume should not be confused with total network traffic.

---

 # 7.47 Assessment — Short Questions

 ## Q12. What is the fundamental Device → Edge technology in the SSP baseline?

 ### Answer

 **BLE.**

---

 ## Q13. What is the primary wide-area technology candidate for Edge → Cloud?

 ### Answer

 **Cellular/IP.**

---

 ## Q14. What role does Wi-Fi play?

 ### Answer

 Wi-Fi can provide connectivity to the Mobile/Edge layer where appropriate, but it is **not the fundamental protection link for the wearable**.

---

 ## Q15. Why is local buffering required?

 ### Answer

 To preserve relevant events and operational information during temporary communication disruption so that information can be synchronized after connectivity is restored.

---

 ## Q16. Why should SSP avoid continuously transmitting raw sensor data?

 ### Answer

 Because local processing can reduce:

 - communication energy;
- bandwidth;
- privacy exposure;
- network traffic;
- cloud-processing requirements.

---

 ## Q17. What happens when BLE is lost?

 ### Answer

 The device should continue appropriate local monitoring, retain relevant events, attempt reconnection and synchronize information after communication is restored.

---

 ## Q18. What happens when Cloud connectivity is lost?

 ### Answer

 Device/Edge protection functions should continue according to their capabilities, important events should be buffered, and synchronization should occur after recovery.

---

 ## Q19. What does communication prioritization achieve?

 ### Answer

 It allows routine, contextual, elevated and critical information to receive different communication treatment according to operational importance.

---

 ## Q20. Why is authentication required?

 ### Answer

 To establish that the communicating device, Edge system, Cloud service or user is an authorized entity.

---

 # 7.48 Assessment — Multiple Choice

 ### Question 1

 Which architecture represents the SSP baseline?

 A. Device → Wi-Fi → Cloud\
 B. Device → BLE → Mobile/Edge → Cellular/IP → Cloud\
 C. Device → LoRa → User\
 D. Device → Cellular only → User

 ### Answer

 **B. Device → BLE → Mobile/Edge → Cellular/IP → Cloud**

---

 ### Question 2

 Which technology is most closely associated with the SSP Device → Mobile/Edge link?

 A. Cellular\
 B. BLE\
 C. Satellite\
 D. Ethernet

 ### Answer

 **B. BLE**

---

 ### Question 3

 Why is local processing useful?

 A. It guarantees unlimited battery life.\
 B. It removes the need for all communication.\
 C. It can reduce latency, energy use, privacy exposure and cloud dependency.\
 D. It eliminates the need for security.

 ### Answer

 **C. It can reduce latency, energy use, privacy exposure and cloud dependency.**

---

 ### Question 4

 Which is an example of LPWAN?

 A. BLE\
 B. Wi-Fi\
 C. LoRa-based networking\
 D. USB

 ### Answer

 **C. LoRa-based networking**

---

 ### Question 5

 Which communication characteristic is most directly related to battery consumption?

 A. Energy/duty cycle\
 B. User interface design\
 C. Cloud dashboard colour\
 D. Database schema

 ### Answer

 **A. Energy/duty cycle**

---

 ### Question 6

 What should happen after temporary connectivity loss?

 A. All monitoring must stop.\
 B. All stored data must be deleted.\
 C. Local/Edge operation continues where possible and information is synchronized after recovery.\
 D. The device must immediately shut down.

 ### Answer

 **C. Local/Edge operation continues where possible and information is synchronized after recovery.**

---

 # 7.49 Assessment — Scenario Question 1

 ### Scenario

 An SSP wearable is being used in an area where the user's smartphone temporarily loses Internet connectivity.

 What should happen?

 ### Model Answer

 The wearable should continue its appropriate local monitoring functions.

 The Mobile/Edge layer should continue local assessment where possible.

 Relevant events should be retained locally until Cloud connectivity is restored.

 After recovery:

```
Connectivity restored
       ↓
Unsynchronized events identified
       ↓
Events prioritized
       ↓
Events transmitted
       ↓
Cloud synchronization
```

 The loss of Internet connectivity should therefore primarily affect **communication and synchronization**, rather than immediately eliminating local protection functions.

---

 # 7.50 Assessment — Scenario Question 2

 ### Scenario

 A designer proposes continuously transmitting accelerometer data from every SSP wearable to the Cloud.

 Is this consistent with the SSP architecture?

 ### Model Answer

 Not as the default architecture.

 Chapter 5 established that raw sensor information should not automatically become system-wide information.

 A better architecture is:

```
Accelerometer
      ↓
Device processing
      ↓
Motion interpretation
      ↓
Relevant event/context
      ↓
BLE
      ↓
Edge
```

 Raw data could still be transmitted selectively when there is a justified engineering, diagnostic or operational requirement.

 The correct principle is:

 > **Transmit the minimum information required for the operational function.**

---

 # 7.51 Assessment — Scenario Question 3

 ### Scenario

 A deployment has no reliable Wi-Fi infrastructure but has good cellular coverage.

 Can SSP operate?

 ### Model Answer

 Yes, assuming the selected Mobile/Edge hardware has suitable cellular connectivity.

 The baseline architecture does not require Wi-Fi as the fundamental wide-area communication mechanism.

 The intended path is:

```
Device
 ↓
BLE
 ↓
Mobile/Edge
 ↓
Cellular/IP
 ↓
Cloud
```

 Wi-Fi is an optional connectivity path for the Edge layer rather than a mandatory protection dependency.

---

 # 7.52 Assessment — Scenario Question 4

 ### Scenario

 BLE connectivity between a wearable and smartphone becomes intermittent.

 What should SSP do?

 ### Model Answer

 The system should detect degraded communication and adapt rather than immediately treating the device as completely failed.

 Possible behavior includes:

 - continue local sensing;
- maintain local event generation;
- increase or adjust reconnection attempts according to policy;
- buffer important events;
- reduce non-critical traffic;
- restore normal communication when BLE becomes stable;
- synchronize buffered information.

 This is an example of **graceful degradation**.

---

 # 7.53 Assessment — Scenario Question 5

 ### Scenario

 A critical event and a routine battery-status message are generated at approximately the same time.

 Should they have identical communication priority?

 ### Answer

 No.

 The critical event should receive higher priority.

 A conceptual policy is:

```
Critical event
      ↓
Highest priority
      ↓
Immediate transmission where possible

Routine status
      ↓
Normal priority
      ↓
Scheduled transmission
```

 This protects communication resources for information with greater operational significance.

---

 # 7.54 Assessment — Design Question

 ### Question

 Design a communication architecture for an SSP wearable and justify your choices.

 ### Model Answer

 A suitable baseline is:

```
Wearable SSP Device
        │
       BLE
        │
        ▼
Mobile / Edge
        │
   Cellular/IP
        │
        ▼
Cloud
        │
 Secure API/Internet
        │
        ▼
Authorized User
```

 BLE is used for the local wearable-to-Edge link because the wearable benefits from relatively low-power short-range communication and mobile-device interoperability.

 The Mobile/Edge layer performs contextual processing and acts as the bridge to the wide-area network.

 Cellular/IP is used for wide-area communication because mobility and geographic coverage are important.

 Wi-Fi can supplement the Edge layer where appropriate.

 The Cloud provides centralized management, storage and analytics.

 Security must be applied across each trust boundary using authenticated communication, encryption, integrity protection and appropriate credential management.

 Local buffering provides resilience during temporary connectivity loss.

 Communication prioritization ensures that critical events receive higher priority than routine status traffic.

---

 # 7.55 Assessment — Explain the Key Architectural Principle

 ### Question

 Explain:

 > **Communication failure must degrade communication capability before it degrades protection capability.**

 ### Model Answer

 The principle means that a temporary network failure should not automatically disable local monitoring and decision functions.

 For example, if Cloud connectivity fails:

```
Cloud communication
       ↓
Unavailable
```

 does not necessarily mean:

```
Device monitoring
       ↓
Unavailable
```

 Instead:

```
Cloud unavailable
       ↓
Edge continues
       ↓
Local processing continues
       ↓
Events retained
       ↓
Cloud restored
       ↓
Synchronization
```

 This principle is enabled by:

 - local processing;
- local storage;
- defined operating states;
- Edge autonomy;
- communication retry;
- synchronization mechanisms.

---

 # 7.56 Assessment — Compare Technologies

 ### Question

 Compare BLE, Wi-Fi, cellular and LoRa-based LPWAN for SSP.

 ### Model Answer

 | Criterion | BLE | Wi-Fi | Cellular | LoRa/LPWAN |
| --- | --- | --- | --- | --- |
| Primary SSP role | Device → Edge | Edge connectivity | Edge → Cloud | Specialized deployments |
| Range | Short | Local | Wide | Long |
| Power suitability for wearable | Good | Less suitable for continuous baseline use | Higher consumption | Potentially good |
| Bandwidth | Moderate | High | High | Low |
| Infrastructure | Edge device | Wi-Fi infrastructure | Operator network | Gateway/network |
| Mobility | Good locally | Local mobility | Excellent | Deployment-dependent |
| Baseline SSP role | Selected | Optional Edge path | Selected | Not baseline |

The conclusion is not that one technology is universally superior.

 Rather, each technology is matched to the communication problem it is designed to solve.

---

 # 7.57 Assessment — Security Question

 ### Question

 A developer proposes using encryption but no device authentication because "the data is encrypted."

 Is this sufficient?

 ### Answer

 No.

 Encryption protects confidentiality, but SSP also requires:

 - device authentication;
- integrity protection;
- authorization;
- replay protection;
- credential management;
- secure provisioning.

 The security architecture must protect both:

 **the information**

 and

 **the identity and authority of the communicating entity**.

---

 # 7.58 Assessment — Advanced Engineering Question

 ### Question

 Why is communication architecture closely connected to the SSP energy architecture?

 ### Model Answer

 Communication requires energy.

 The amount of energy depends on factors such as:

 - radio technology;
- transmission power;
- active time;
- connection establishment;
- packet volume;
- retry frequency;
- scanning;
- duty cycle;
- network conditions.

 Therefore:

 $$
E_{total}
=
E_{sensing}
+
E_{processing}
+
E_{positioning}
+
E_{communication}
+
E_{storage}
+
E_{security}
+
E_{idle}
$$

 Communication architecture affects $E_{communication}$, which directly affects battery autonomy.

 This is why communication cannot be designed independently of the energy architecture.

---

 # 7.59 Advanced Assessment — Critical Event Path

 ### Question

 Construct the SSP critical communication path.

 ### Answer

```
Physical observation
        ↓
Device sensing
        ↓
Local event detection
        ↓
Priority BLE transmission
        ↓
Edge confirmation/context
        ↓
Risk/severity assessment
        ↓
Priority Cellular/IP communication
        ↓
Cloud
        ↓
Secure application/API
        ↓
Authorized user/operational system
```

 The critical path should be evaluated separately from routine status traffic.

 Important measurements include:

 - event detection latency;
- BLE transmission latency;
- Edge processing latency;
- wide-area transmission latency;
- Cloud processing latency;
- user-notification latency;
- total end-to-end latency.

---

 # 7.60 Advanced Assessment — Data Minimization

 ### Question

 Why is communication architecture also a privacy architecture?

 ### Model Answer

 Every transmitted item creates an information-flow boundary.

 If raw data is transmitted unnecessarily, more information becomes exposed to:

 - communication networks;
- Edge systems;
- Cloud infrastructure;
- storage systems;
- authorized users and services.

 Local processing allows SSP to transform raw information into the minimum operational information required.

 For example:

```
Raw sensor information
        ↓
Local processing
        ↓
Relevant context
        ↓
Privacy filtering
        ↓
Structured event
        ↓
Communication
```

 Therefore communication design directly influences privacy exposure.

---

 # 7.61 Study Summary

 The most important concepts from Chapter 7 are:

 1. **SSP uses a layered communication architecture.**
    **Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure API ↔ User**
2. **BLE is the baseline Device → Mobile/Edge technology.**
3. **Cellular/IP is the baseline Edge → Cloud wide-area path.**
4. **Wi-Fi can supplement the Mobile/Edge layer but is not the fundamental wearable protection link.**
5. **Direct cellular on the wearable remains a deployment-dependent option.**
6. **LoRa/LPWAN can be relevant to specialized deployments but is not the baseline communication architecture.**
7. **Communication should be policy-driven rather than continuous by default.**
8. **Critical information receives higher priority than routine information.**
9. **Local processing reduces unnecessary communication.**
10. **Local buffering enables operation during temporary connectivity loss.**
11. **Security includes authentication, confidentiality, integrity, authorization and replay protection.**
12. **Communication failures should cause graceful degradation rather than immediate loss of protection capability.**
13. **Communication architecture directly affects energy consumption.**
14. **Communication architecture also influences privacy because it determines what information crosses system boundaries.**
15. **Radio technology and application protocols are separate engineering decisions.**

---

 # 7.62 Chapter 7 Master Assessment

 ### Question 1

 What is the baseline SSP communication architecture?

 ### Answer

 **Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ Authorized User**

 with Wi-Fi available to the Mobile/Edge layer where appropriate.

---

 ### Question 2

 Why is BLE appropriate for the Device → Edge link?

 ### Answer

 Because it provides a relatively low-power short-range communication mechanism suitable for wearable-to-mobile/Edge interaction.

---

 ### Question 3

 Why is Wi-Fi not the fundamental protection link?

 ### Answer

 Because wearable operation should not depend on continuous Wi-Fi infrastructure availability, and Wi-Fi can impose greater energy and infrastructure requirements than are desirable for the baseline wearable link.

---

 ### Question 4

 Why is cellular primarily associated with the Edge layer?

 ### Answer

 The Edge has greater computational, energy and physical resources than the wearable and can therefore act as the wide-area communication gateway.

---

 ### Question 5

 When might direct cellular on the wearable be justified?

 ### Answer

 When autonomous wide-area operation is required and the additional energy, hardware, antenna, cost and physical requirements are acceptable.

---

 ### Question 6

 Why is local buffering essential?

 ### Answer

 It preserves important information during temporary communication loss and enables synchronization after recovery.

---

 ### Question 7

 What happens when Cloud connectivity is lost?

 ### Answer

 Device and Edge functions continue according to their capabilities, important information is retained, and synchronization occurs after connectivity is restored.

---

 ### Question 8

 What is communication prioritization?

 ### Answer

 It is the policy of treating information differently according to operational significance, such as routine, contextual, elevated and critical information.

---

 ### Question 9

 Why should raw sensor data not automatically be transmitted?

 ### Answer

 Because local processing can reduce energy consumption, bandwidth requirements, privacy exposure and unnecessary Cloud processing.

---

 ### Question 10

 What are the principal communication security requirements?

 ### Answer

 - authentication;
- confidentiality;
- integrity;
- authorization;
- replay protection;
- secure provisioning;
- credential/key management.

---

 ### Question 11

 What is the most important resilience principle of Chapter 7?

 ### Answer

 > **Communication failure must degrade communication capability before it degrades protection capability.**

---

 ### Question 12

 What is the relationship between communication and energy?

 ### Answer

 More radio activity generally increases energy consumption. Therefore communication frequency, payload size, radio technology, duty cycle, retries and operating state must be included in the SSP energy model.

---

 # 7.63 Final Chapter 7 Learning Outcome

 After completing this chapter and assessment, the SSP communication architecture should be understood as a **distributed, secure, adaptive and resilient communication system**, rather than simply a collection of wireless technologies.

 The baseline engineering design is:

```
                     ┌─────────────────┐
                     │      CLOUD      │
                     │                 │
                     │ Storage         │
                     │ Management      │
                     │ Analytics       │
                     └────────┬────────┘
                              │
                         Cellular/IP
                              │
                              ▼
                     ┌─────────────────┐
                     │  MOBILE / EDGE  │
                     │                 │
                     │ Fusion          │
                     │ Risk            │
                     │ Prediction      │
                     │ Resilience      │
                     └────────┬────────┘
                              │
                             BLE
                              │
                              ▼
                     ┌─────────────────┐
                     │   SSP DEVICE    │
                     │                 │
                     │ Position        │
                     │ Motion          │
                     │ Local logic     │
                     │ Events          │
                     │ Power           │
                     └─────────────────┘
```

 The architectural philosophy can be summarized as:

 > **Use low-power local communication where the device is constrained, wide-area connectivity where mobility and geographic coverage require it, secure application communication for system-wide interaction, and local buffering and processing whenever communication cannot be assumed to be continuously available.**

 This chapter therefore completes the communication layer of the SSP engineering baseline and provides the foundation for the subsequent **embedded software and data architecture**, where the system will define how the Device and Edge actually process, represent, prioritize and manage the information transported by this communication architecture.
