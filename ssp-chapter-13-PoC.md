# Chapter 13 — PoC

 ## Chapter 13 plan

 Chapter 13 should **not redesign SSP** and should not introduce new architectural decisions. Its purpose is to demonstrate that the fundamental IoT concept defined in Chapters 5–12 can be implemented and exercised in a laboratory environment.

 The chapter will therefore follow this logic:

 **Real SSP design → PoC abstraction → Laboratory implementation → Demonstration → Limitations → Traceability back to SSP**

 The planned sections are:

 1. **13.1 PoC objectives** — define exactly what the laboratory demonstration must prove.
2. **13.2 Functions to demonstrate** — identify the minimum end-to-end SSP functions selected for demonstration.
3. **13.3 PoC architecture** — show the laboratory Device → Mobile/Edge → Cloud → User chain.
4. **13.4 Hardware substitution strategy** — explicitly distinguish production SSP hardware from laboratory substitutes.
5. **13.5 Device implementation** — describe the MCU/SoC, sensors, firmware and local event generation.
6. **13.6 BLE communication** — demonstrate the Device → Mobile/Edge link.
7. **13.7 Mobile/Edge implementation** — demonstrate acquisition, local processing and forwarding.
8. **13.8 Cloud integration** — demonstrate transmission to the backend, storage and event processing.
9. **13.9 Demonstration scenario** — define a reproducible end-to-end operational scenario.
10. **13.10 PoC limitations** — identify what the laboratory implementation does not prove.
11. **13.11 Mapping between real system and laboratory implementation** — provide explicit traceability between the proposed product and the PoC.

 A key principle throughout the chapter will be:

 > **The PoC validates the architecture and selected technical mechanisms; it does not validate the complete commercial SSP product.**

---

 # 13\. Proof of Concept

 ## 13.1 PoC Objectives

 The purpose of the SmartSecurePerimeter (SSP) Proof of Concept is to demonstrate that the principal technical chain defined by the real-world SSP architecture can operate end-to-end using laboratory-accessible hardware and software.

 The PoC therefore focuses on demonstrating the following chain:

 **Device sensing → Local processing → BLE communication → Mobile/Edge processing → Cloud communication → Cloud processing/storage → User notification**

 The PoC is not intended to reproduce every capability of the complete SSP product. In particular, it is not expected to reproduce the final industrial enclosure, production-grade wearable electronics, certified positioning subsystem, commercial cellular subsystem, production cloud infrastructure, security certification or complete AI capability.

 The PoC has five principal objectives:

 1. Demonstrate acquisition of sensor information by an embedded device.
2. Demonstrate local interpretation of sensor information and generation of an SSP-relevant event.
3. Demonstrate reliable transfer of device information through BLE to a mobile/edge node.
4. Demonstrate forwarding of structured information from the mobile/edge node to the cloud.
5. Demonstrate cloud-side storage, processing and presentation of the resulting information.

 The resulting demonstration should provide evidence that the fundamental SSP Device → Edge/Mobile → Cloud → User architecture is technically realizable.

 ### PoC success criterion

 At the highest level, the PoC is successful if a defined physical or simulated event at the device can produce a corresponding structured event at the user interface through the complete communication and processing chain.

 The intended demonstration is therefore:

 **Physical event → Sensor data → Device event → BLE packet → Mobile/Edge event → Cloud event → User-visible result**

---

 ## 13.2 Functions to Demonstrate

 The PoC should demonstrate a deliberately selected subset of the complete SSP functionality.

 | SSP function | PoC implementation | Demonstration objective |
| --- | --- | --- |
| Sensor acquisition | Laboratory sensor connected to MCU/SoC | Demonstrate physical data acquisition |
| Device processing | Embedded firmware | Demonstrate local filtering/event detection |
| Device identity | Configured device identifier | Associate data with a simulated SSP device |
| BLE communication | MCU/SoC → Android device | Demonstrate local wireless communication |
| Edge/mobile acquisition | Android application | Receive and interpret device data |
| Structured data | JSON or equivalent message structure | Demonstrate interoperable data exchange |
| Cloud communication | HTTPS/API connection | Transfer events beyond the local device |
| Cloud storage | Backend database | Persist device/event information |
| Event processing | Backend logic | Demonstrate server-side interpretation |
| User interface | Web/mobile dashboard | Present status and events |
| Alert representation | Dashboard notification | Demonstrate operational response |
| Communication interruption | Controlled disconnect | Demonstrate basic failure detection |
| Recovery | BLE reconnection and/or data resynchronization | Demonstrate recovery behavior |

The PoC should prioritize the **end-to-end chain** rather than attempting to maximize the number of sensors or algorithms implemented.

 This is important because an extensive isolated sensor demonstration would provide less architectural evidence than a smaller but complete Device → Edge → Cloud → User demonstration.

---

 ## 13.3 PoC Architecture

 The laboratory PoC will use a simplified representation of the SSP architecture established in Chapter 5.

```
┌───────────────────────────────┐
│        SSP DEVICE PoC         │
│                               │
│  Sensor(s)                    │
│      ↓                        │
│  MCU / SoC                    │
│      ↓                        │
│  Local processing             │
│      ↓                        │
│  BLE                          │
└───────────────┬───────────────┘
                │
                │ BLE
                ▼
┌───────────────────────────────┐
│       MOBILE / EDGE PoC       │
│                               │
│  Android application          │
│      ↓                        │
│  BLE acquisition              │
│      ↓                        │
│  Validation / filtering       │
│      ↓                        │
│  JSON/API message             │
└───────────────┬───────────────┘
                │
                │ HTTPS / API
                ▼
┌───────────────────────────────┐
│          CLOUD PoC            │
│                               │
│  API endpoint                 │
│      ↓                        │
│  Backend processing           │
│      ↓                        │
│  Database                     │
│      ↓                        │
│  Event service                │
└───────────────┬───────────────┘
                │
                │ Web/API
                ▼
┌───────────────────────────────┐
│        USER INTERFACE         │
│                               │
│  Status                       │
│  Device information           │
│  Events                       │
│  Alerts                       │
└───────────────────────────────┘
```

 This architecture intentionally mirrors the full SSP architecture while reducing the physical implementation to the components necessary for demonstration.

 The laboratory implementation therefore remains traceable to the real system:

 **Device → Edge/Mobile → Cloud → User**

 rather than becoming a separate IoT project.

---

 ## 13.4 Hardware Substitution Strategy

 The distinction between the real SSP system and the laboratory PoC is essential.

 The real-world design described in Chapters 5–12 assumes that SSP will be developed with sufficient engineering resources to support a dedicated wearable device, production-grade electronics, appropriate positioning and communication capabilities, secure lifecycle management and an operational cloud environment.

 The laboratory environment may not provide all of these components.

 Consequently, the PoC uses **functional substitutes** rather than attempting to reproduce the final product physically.

 ### Proposed substitution strategy

 | Real SSP component | Laboratory PoC substitute | Reason |
| --- | --- | --- |
| Dedicated SSP wearable | Laboratory MCU/SoC development board | Demonstrates embedded processing |
| Production inertial sensor | Available IMU/accelerometer | Demonstrates motion acquisition |
| Production GNSS subsystem | Simulated or available position input where necessary | Avoids making laboratory hardware define the product |
| Production cellular modem | Android smartphone network connection | Demonstrates wide-area/cloud connectivity |
| Dedicated edge gateway | Android smartphone | Provides BLE + network connectivity |
| Production cloud platform | Laboratory/development cloud backend | Demonstrates API and storage chain |
| Production dashboard | Development web/mobile interface | Demonstrates user interaction |
| Production security infrastructure | Development security mechanisms | Demonstrates architectural security principles at PoC level |

This approach preserves the distinction established in the project structure:

 > **The laboratory implementation is an implementation of the SSP concept, not the specification of the final SSP product.**

 ### Why the Android device is particularly useful

 The Android device can act simultaneously as:

 - BLE central;
- edge-processing node;
- temporary local data store;
- wide-area communication gateway;
- development user interface.

 This allows the PoC to reproduce several functions of the real Edge/Mobile layer without requiring a dedicated gateway during the laboratory phase.

---

 ## 13.5 Device Implementation

 The device PoC consists of an MCU/SoC connected to one or more sensors relevant to SSP.

 The minimum implementation should include:

 - MCU/SoC;
- inertial sensor or equivalent measurable input;
- BLE capability;
- firmware;
- device identifier;
- basic local processing;
- event-generation logic;
- local status information.

 The embedded software should follow the processing sequence:

 **Acquire → Filter → Interpret → Package → Transmit**

 For example:

 1. The sensor generates a measurement.
2. The MCU samples the measurement.
3. Basic filtering removes clearly invalid or excessively noisy readings.
4. The firmware determines whether a defined demonstration condition has occurred.
5. The firmware creates a structured event.
6. The event is transmitted through BLE.

 A simplified event representation could contain:

```
{
  "device_id": "SSP-POC-001",
  "timestamp": "...",
  "event_type": "MOTION_EVENT",
  "sensor_value": 123,
  "event_state": "ACTIVE"
}
```

 The exact implementation format may change during development, but the principle should remain consistent with the data model established in Chapter 9.

 ### Local processing

 The PoC should demonstrate at least one meaningful operation locally.

 Examples include:

 - threshold detection;
- motion-state classification;
- signal filtering;
- event debouncing;
- basic anomaly detection;
- sensor validity checking.

 This provides evidence for the architectural principle established in Chapters 5 and 10 that information should not necessarily be transmitted as completely raw data.

---

 ## 13.6 BLE Communication

 BLE provides the principal Device → Mobile/Edge communication path for the laboratory PoC.

 The device acts as the BLE peripheral and exposes an SSP-related service.

 The Android application acts as the BLE central.

 The communication sequence is:

```
MCU/SoC
   │
   │ BLE advertising
   ▼
Android application
   │
   │ BLE connection
   ▼
SSP service discovery
   │
   │ characteristic subscription/read
   ▼
Sensor/event data
```

 The PoC should demonstrate:

 - device discovery;
- connection establishment;
- service discovery;
- data reception;
- device identification;
- connection-loss detection;
- reconnection.

 Where practical, BLE characteristics should distinguish between different classes of information, for example:

 - device status;
- sensor measurements;
- event notifications;
- configuration information.

 The PoC does not need to reproduce every BLE service required by the final product. It must demonstrate the communication principle and its integration with the remainder of the architecture.

---

 ## 13.7 Mobile/Edge Implementation

 The Android application represents the laboratory implementation of the SSP Edge/Mobile layer.

 Its responsibilities are intentionally broader than simply displaying BLE data.

 The application should:

 1. discover the SSP PoC device;
2. establish a BLE connection;
3. receive sensor/event information;
4. validate the received message;
5. attach or verify contextual information where required;
6. determine whether an event requires cloud transmission;
7. construct a structured API message;
8. transmit the message to the cloud;
9. provide local status information;
10. detect and represent communication failures.

 The resulting processing chain is:

 **BLE reception → Validation → Context processing → Event prioritization → JSON/API message → Cloud**

 This demonstrates one of the central architectural concepts of SSP: the mobile/edge layer is not merely a communication bridge but can perform useful local processing.

 ### Local operation during cloud disconnection

 Where practical, the application should temporarily retain events when the cloud connection is unavailable.

 A simplified sequence is:

```
Event received
      ↓
Cloud available?
  ┌───┴────┐
 YES       NO
  ↓         ↓
Transmit   Store locally
  ↓         ↓
Confirm    Retry later
```

 This provides a laboratory demonstration of the resilience principles defined in Chapters 5 and 7.

---

 ## 13.8 Cloud Integration

 The cloud PoC provides the server-side part of the SSP architecture.

 The minimum cloud implementation should provide:

 - an API endpoint;
- authentication appropriate to the development environment;
- event reception;
- message validation;
- device/event identification;
- database storage;
- event processing;
- retrieval of current status;
- retrieval of historical events.

 A typical data path is:

```
Android
   │
   │ HTTPS
   ▼
API Gateway / Backend
   │
   ├── Validate
   │
   ├── Authenticate
   │
   ├── Process
   │
   └── Store
          │
          ▼
       Database
          │
          ▼
       Dashboard
```

 The PoC backend should use the same conceptual data flow defined in Chapter 9:

 **Generated → Acquired → Processed → Transmitted → Stored → Analyzed → Presented → Acted upon**

 The implementation technology may be selected according to laboratory availability and development efficiency, provided that it does not contradict the real SSP architecture.

---

 ## 13.9 Demonstration Scenario

 A single reproducible scenario should be used as the primary PoC demonstration.

 ### Scenario: SSP perimeter-event demonstration

 The demonstration begins with an SSP PoC device operating in its normal monitoring state.

 The sequence is:

 1. The MCU/SoC starts and initializes its sensor and BLE subsystem.
2. The device advertises its SSP identity.
3. The Android application discovers and connects to the device.
4. The device begins transmitting sensor information.
5. The Android application receives and validates the information.
6. A defined physical or simulated condition is introduced.
7. The embedded firmware identifies the condition.
8. An SSP event is generated.
9. The event is transmitted through BLE.
10. The Android application receives the event.
11. The application packages the event into a structured API message.
12. The message is transmitted to the cloud.
13. The backend authenticates and validates the message.
14. The event is stored.
15. The backend updates the operational state.
16. The user interface displays the event.
17. The operator can identify the affected device and event.
18. A communication interruption is introduced.
19. The system detects the interruption.
20. Connectivity is restored.
21. The system reconnects and resumes normal operation.

 The demonstration therefore exercises the complete chain:

 **Device → BLE → Mobile/Edge → Internet → Cloud → User**

 and, where implemented:

 **Failure → Local handling → Recovery**

 ### Demonstration evidence

 The PoC should capture evidence at each major stage, such as:

 - device sensor output;
- BLE connection state;
- Android received message;
- API request;
- backend log;
- database record;
- dashboard event;
- communication failure/recovery state.

 This evidence will later support Chapter 15 validation.

---

 ## 13.10 PoC Limitations

 The PoC must explicitly state what it does **not** demonstrate.

 ### 13.10.1 Production hardware limitations

 The laboratory MCU/SoC and sensors are development components and do not represent the final mechanical, electrical or environmental design of the SSP wearable.

 The PoC therefore does not validate:

 - production enclosure;
- waterproofing;
- tamper resistance;
- long-term mechanical durability;
- wearable comfort;
- manufacturing tolerances;
- production battery performance.

 ### 13.10.2 Positioning limitations

 If GNSS or other positioning hardware is simulated or simplified, the PoC does not establish the final positioning performance of SSP.

 Position accuracy, indoor operation, urban canyon behavior and multi-constellation performance must be validated with the production positioning architecture.

 ### 13.10.3 Communication limitations

 The use of a smartphone as the laboratory wide-area gateway means that the PoC does not establish the performance of the final cellular or alternative wide-area communication subsystem.

 The following remain production-engineering questions:

 - cellular coverage;
- modem energy consumption;
- antenna performance;
- network roaming;
- carrier dependency;
- communication cost;
- large-scale network behavior.

 ### 13.10.4 Security limitations

 Development credentials, laboratory infrastructure and simplified authentication mechanisms cannot be treated as equivalent to the final security architecture.

 Production SSP would require formal security engineering, key management, secure provisioning, secure boot/update mechanisms where applicable, penetration testing and lifecycle security processes.

 ### 13.10.5 AI limitations

 A PoC may initially use deterministic rules rather than a trained AI model.

 This is acceptable because Chapter 10 defines AI as a function that must demonstrate measurable value rather than a mandatory feature added solely for completeness.

 Where AI is included in the PoC, the demonstration should establish the processing chain but should not be interpreted as sufficient evidence of production-level model performance.

 ### 13.10.6 Scalability limitations

 A laboratory backend may contain only a small number of devices and events.

 Consequently, the PoC does not prove:

 - production fleet scalability;
- database scaling;
- cloud availability targets;
- large-scale event ingestion;
- multi-region deployment;
- production disaster recovery.

 These issues remain part of the cloud engineering and validation activities defined elsewhere in the project.

---

 ## 13.11 Mapping Between Real System and Laboratory Implementation

 The relationship between the complete SSP system and the laboratory PoC should remain explicit.

 | Real SSP architecture | Real-system implementation | Laboratory PoC |
| --- | --- | --- |
| SSP wearable | Dedicated production wearable device | MCU/SoC development board |
| Position sensing | Production GNSS/multi-source positioning | Simulated or laboratory position input where required |
| Motion sensing | Production IMU | Laboratory accelerometer/IMU |
| Local processing | Production embedded firmware | MCU firmware |
| Device communication | Production BLE subsystem | MCU BLE |
| Edge/Mobile | Dedicated or supported mobile/edge application | Android application |
| Wide-area communication | Production cellular/other WAN | Smartphone network connection |
| Cloud API | Production API platform | Development API |
| Event processing | Production event/risk services | Simplified backend logic |
| Database | Production managed database architecture | Development database |
| AI | Production validated model(s) | Optional simplified model/rule implementation |
| User interface | Operational dashboard | Development dashboard |
| Device security | Production security architecture | Development-level security mechanisms |
| Fleet management | Production device-management platform | Limited PoC device management |

This table is important because it prevents a common design error: treating the laboratory implementation as though it were the final system specification.

 ### Architectural traceability

 The PoC maps directly to the frozen SSP architecture:

 | SSP layer | Demonstrated PoC function |
| --- | --- |
| **Device** | Sensor acquisition, local processing, BLE |
| **Edge/Mobile** | Data acquisition, validation, contextual processing, forwarding |
| **Cloud** | API, event processing, storage |
| **User** | Dashboard and event visualization |
| **Control/feedback** | Configuration/reconnection where implemented |

The resulting chain is:

 **Device → Edge/Mobile → Cloud → User**

 with selected feedback and recovery paths.

---

 ## 13.12 PoC Requirements Traceability

 The PoC should demonstrate selected requirements from Chapter 3 rather than attempting to validate every requirement.

 | Requirement category | PoC evidence |
| --- | --- |
| Sensor acquisition | Sensor values captured by MCU |
| Local processing | Device-generated event |
| BLE communication | Successful Device → Android transfer |
| Mobile processing | Android parsing and processing |
| Cloud connectivity | Successful API transmission |
| Data integrity | Valid structured event received by backend |
| Data storage | Event stored in database |
| Event processing | Backend generates operational state |
| User notification | Event displayed in dashboard |
| Communication resilience | Disconnect/reconnect demonstration |
| Local buffering | Event retained during temporary outage, where implemented |
| Device identification | Unique PoC device identifier |
| Security | Authenticated or protected development communication |
| End-to-end operation | Complete event journey from device to user |

The quantitative performance requirements themselves remain subject to the formal testing and validation process in Chapter 15.

 This distinction is important:

 > **The PoC demonstrates feasibility; Chapter 15 determines whether the defined performance requirements are actually satisfied.**

---

 ## 13.13 PoC Acceptance Criteria

 The PoC should use clear engineering acceptance criteria.

 At minimum:

 1. The device shall acquire a defined sensor input.
2. The device shall establish BLE communication with the Android application.
3. The Android application shall correctly receive a valid device message.
4. The Android application shall convert the information into the defined structured representation.
5. The cloud API shall accept the message.
6. The backend shall validate and store the event.
7. The user interface shall display the resulting event.
8. A defined communication interruption shall be detectable.
9. The system shall recover after communication is restored.
10. Evidence shall be collected for each stage of the end-to-end chain.

 The exact quantitative thresholds should be taken from the applicable requirements in Chapter 3 rather than invented independently in the PoC chapter.

---

 ## 13.14 Relationship to the Complete SSP Design

 The PoC does not modify the architectural decisions already established.

 The design hierarchy remains:

 **Chapter 3 — Requirements**

 ↓

 **Chapter 4 — Market and context evidence**

 ↓

 **Chapter 5 — IoT architecture**

 ↓

 **Chapter 6 — Hardware**

 ↓

 **Chapter 7 — Communication**

 ↓

 **Chapter 8 — Software**

 ↓

 **Chapter 9 — Data Flow**

 ↓

 **Chapter 10 — AI / EdgeAI**

 ↓

 **Chapter 11 — Energy / Performance**

 ↓

 **Chapter 12 — Cloud Architecture**

 ↓

 **Chapter 13 — PoC**

 The PoC therefore represents an **implementation slice through the previously defined architecture**.

 It does not feed backwards into the design by silently replacing production components with laboratory components.

 If laboratory limitations reveal a genuine architectural problem, that issue should instead be recorded as an engineering finding and addressed through the appropriate design or validation chapter.

---

 ## 13.15 Chapter 13 Conclusion

 The SSP PoC provides a practical demonstration of the central IoT concept without redefining the real-world system around laboratory constraints.

 The proposed demonstration follows the complete chain:

 **Sense → Process → BLE → Mobile/Edge → Cloud → Store/Analyze → User**

 and includes, where practical, communication interruption and recovery.

 The principal purpose of the PoC is therefore to demonstrate that the architectural concept established in Chapters 5–12 can be implemented as a coherent end-to-end IoT system.

 The distinction between the two levels remains fundamental:

 > **The real SSP design specifies the product that would be engineered for operational deployment.**

 > **The laboratory PoC demonstrates selected technical mechanisms of that design using available resources.**

 This separation allows the project to satisfy the course requirement for a practical IoT demonstration while preserving the engineering integrity of the complete SSP solution.

 The next stage is **Chapter 14 — Business / Costs / Scalability**, where the technically defined SSP solution is translated into a development, deployment and economic model, including BOM, manufacturing assumptions, cloud/OPEX costs, total cost of ownership and scaling strategy.
