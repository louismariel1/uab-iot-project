Absolutely. Chapter 6 is now the hardware-design baseline following Chapter 5. For the **study & assessment** version, the useful next step is to turn it into an answer-included learning chapter: key concepts, engineering reasoning, review questions, and assessment answers, while preserving the original technical decisions.

 # Chapter 6 — SSP Hardware and Device Architecture

 ## Answer-Included Study & Assessment

 ### 6.1 Chapter Learning Objectives

 After studying this chapter, you should be able to:

 - explain the role of the SSP device within the Device–Edge/Mobile–Cloud architecture;
- identify the major hardware subsystems required by SSP;
- explain why local processing is necessary;
- distinguish positioning, motion sensing and proximity functions;
- explain the importance of local storage and secure hardware;
- describe adaptive power-management states;
- understand the relationship between hardware, firmware and system architecture;
- explain prototype-to-product hardware evolution;
- identify the principal hardware KPIs and engineering risks;
- trace hardware decisions back to system requirements.

---

 ## 6.2 Core Concept: SSP Is Not Simply a GPS Tracker

 A central learning point from this chapter is that the SSP device is an **autonomous embedded computing node**.

 Its function is not limited to determining location.

 The hardware must support:

 **Sensing → Positioning → Processing → Event generation → Communication → Security → Power management → Health monitoring**

 This distinction is important because the device must operate as part of a distributed cyber-physical system.

 ### Study question

 **Q: Why is it inaccurate to describe SSP simply as a GPS tracker?**

 **Answer:**\
 Because positioning is only one SSP function. The device also performs motion sensing, local processing, event generation, communication, security, power management, tamper monitoring and health monitoring. It must also continue selected functions during communication loss.

---

 # 6.3 Hardware Role Within the SSP Architecture

 The device is the physical boundary between the monitored environment and the digital SSP system.

 The basic information chain is:

```
Physical environment
       ↓
     Sensors
       ↓
 Local processing
       ↓
 Event generation
       ↓
 Communication
       ↓
 Edge/Mobile
       ↓
     Cloud
```

 The device must therefore provide sufficient local capability to prevent every operation from depending on the Edge or Cloud.

 ### Key principle

 > **The device shall retain sufficient local capability to perform functions that cannot safely depend on continuous external connectivity.**

 ### Assessment question

 **Q: What is the principal architectural reason for giving the device local processing capability?**

 **Answer:**\
 Local processing reduces dependence on external connectivity and can improve latency, resilience, privacy and energy efficiency by allowing relevant information to be interpreted before transmission.

---

 # 6.4 SSP Device Functional Architecture

 The principal hardware blocks are:

```
                 SSP DEVICE
                     │
        ┌────────────┼────────────┐
        │            │            │
   Positioning    Motion       Proximity
        │         sensors        │
        └────────────┼────────────┘
                     ▼
              MCU / SoC
          ┌──────────┼──────────┐
          │          │          │
       Storage    Security   Communication
          │          │          │
          └──────────┼──────────┘
                     ▼
              Power Management
                     │
                  Battery
```

 Additional functions include tamper detection and device-health monitoring.

 ### Major subsystems

 | Subsystem | Primary purpose |
| --- | --- |
| MCU/SoC | Local processing and control |
| GNSS/positioning | Position and timing |
| IMU | Motion sensing |
| Local radio | Proximity and Edge interaction |
| Wide-area radio | Remote communication |
| Non-volatile storage | Buffering and configuration |
| Secure hardware | Identity and key protection |
| Power management | Controlled energy distribution |
| Battery | Autonomous energy |
| Tamper sensing | Device-integrity monitoring |
| Health monitoring | Device-state reporting |

---

 # 6.5 Hardware Design Principles

 The chapter establishes eight principal hardware-design principles.

 ### HD-01 — Local autonomy

 The device must retain essential local functionality.

 ### HD-02 — Energy proportionality

 Hardware must support different operating states and power levels.

 ### HD-03 — Modular communication

 Communication hardware should be replaceable or evolvable without redesigning the entire device.

 ### HD-04 — Secure identity

 The device requires protected identity and credentials.

 ### HD-05 — Sensor extensibility

 Interfaces and processing resources should permit justified future sensing.

 ### HD-06 — Graceful degradation

 Failure of a non-critical function should not necessarily disable the complete system.

 ### HD-07 — Lifecycle support

 Provisioning, diagnostics, secure updates and replacement must be considered from the beginning.

 ### HD-08 — Prototype-to-product continuity

 The prototype architecture should provide a realistic path toward a deployable product.

 ### Study question

 **Q: Which principle prevents the prototype from becoming an isolated technical demonstration?**

 **Answer:**\
 HD-08, prototype-to-product continuity. It requires the architecture to support evolution from development hardware through engineering prototypes and eventually toward production-oriented hardware.

---

 # 6.6 Embedded Processing Subsystem

 The MCU/SoC is the principal local computing element.

 It must potentially support:

 - sensor acquisition;
- signal preprocessing;
- motion-state estimation;
- position processing;
- event generation;
- communication management;
- power management;
- local buffering;
- diagnostics;
- security;
- lightweight inference.

 The key engineering principle is **sufficient performance**, not maximum performance.

 Excessive computational capability can increase:

 - energy consumption;
- thermal load;
- cost;
- software complexity;
- attack surface.

 ### Assessment question

 **Q: Why should SSP not automatically select the highest-performance processor available?**

 **Answer:**\
 Because maximum performance can introduce unnecessary power consumption, heat, cost, software complexity and attack surface. SSP requires sufficient local computational capability rather than maximum computational capability.

---

 # 6.7 Four Levels of Local Processing

 The chapter establishes a useful processing hierarchy.

 ### Level 1 — Sensor processing

 Raw measurements are converted into usable quantities.

 Examples:

 - acceleration;
- angular velocity;
- position;
- battery state;
- communication state.

 ### Level 2 — Context interpretation

 Measurements are combined to determine device state.

 Examples:

 - stationary;
- walking;
- travelling;
- unexpected movement;
- positioning degradation.

 ### Level 3 — Event generation

 Relevant changes become structured events.

 Examples:

 - geofence transition;
- abnormal movement;
- tamper;
- communication failure;
- low battery.

 ### Level 4 — Local decision

 The device determines whether immediate action or higher-priority communication is required.

 ### Important design implication

 The device should not automatically transmit every raw sensor measurement.

 Instead:

```
Raw measurements
      ↓
Local interpretation
      ↓
Relevant information
      ↓
Structured event
      ↓
Transmission when required
```

 ### Assessment question

 **Q: What is the benefit of the four-level processing hierarchy?**

 **Answer:**\
 It progressively converts raw measurements into useful contextual information and events, reducing unnecessary communication and supporting SSP requirements for privacy, resilience and energy efficiency.

---

 # 6.8 Positioning Subsystem

 GNSS or an equivalent satellite-navigation technology is the expected primary outdoor positioning mechanism, subject to final component selection.

 The positioning subsystem should provide more than a simple coordinate.

 Conceptually:

 **Position + Time + Quality/Confidence + Validity**

 This is important because positioning quality varies with environmental conditions.

 The system must distinguish between:

 - valid high-confidence position;
- degraded position;
- unavailable position;
- potentially inconsistent position.

 ### Study question

 **Q: Why should SSP not treat every position measurement as equally reliable?**

 **Answer:**\
 Because positioning accuracy and availability can vary according to environmental and signal conditions. A confidence or quality indicator allows downstream decision-making to account for uncertainty.

---

 # 6.9 Motion-Sensing Subsystem

 The baseline motion subsystem should consider:

 - accelerometer;
- gyroscope where justified;
- other motion-related sensors where deployment requirements support them.

 The accelerometer can support:

 - movement detection;
- activity-state estimation;
- vibration detection;
- orientation changes;
- tamper detection;
- sensor plausibility checking.

 A gyroscope can provide additional information about:

 - angular motion;
- orientation;
- device manipulation;
- movement classification.

 ### Engineering rule

 A sensor should be justified according to:

 **Information value vs. energy consumption vs. cost vs. processing requirement**

 ### Assessment question

 **Q: Why should SSP not add every commercially available sensor?**

 **Answer:**\
 Every additional sensor increases hardware cost, energy consumption, integration complexity and potentially processing requirements. A sensor should therefore be included only when its information value justifies those costs.

---

 # 6.10 Proximity and Local Radio

 A local wireless technology such as BLE is a candidate for:

 - device association;
- proximity detection;
- Edge/Mobile connectivity;
- configuration;
- diagnostics.

 However, the radio should not necessarily operate continuously at maximum activity.

 The architecture distinguishes:

 1. association;
2. periodic discovery;
3. continuous proximity monitoring;
4. event-driven communication.

 These modes can have substantially different energy implications.

 ### Assessment question

 **Q: What is the main hardware concern with continuous local-radio scanning?**

 **Answer:**\
 It can increase energy consumption significantly. SSP therefore requires configurable radio behavior appropriate to the operating state and operational context.

---

 # 6.11 Wide-Area Communication Hardware

 The device may require cellular or another wide-area technology when autonomous remote communication is necessary.

 However, Chapter 6 deliberately does **not** make the final communication-technology selection.

 That decision belongs to Chapter 7.

 The hardware must instead provide a suitable platform for whichever communication technology is selected.

 Candidate-selection criteria include:

 - geographical coverage;
- latency;
- power consumption;
- bandwidth;
- security;
- module availability;
- antenna requirements;
- regulatory constraints;
- deployment environment.

 ### Key distinction

 **Chapter 6:** establishes hardware capability.

 **Chapter 7:** selects and evaluates communication technologies and protocols.

---

 # 6.12 Communication Failure and Fallback

 SSP must assume that communication can fail.

 Possible failures include:

 - loss of association;
- network unavailability;
- degraded signal;
- repeated transmission failure.

 The device therefore requires:

 **Detection → Local continuation → Event buffering → Recovery → Synchronization**

```
Normal communication
        ↓
Communication failure
        ↓
Local operation
        ↓
Store important events
        ↓
Communication restored
        ↓
Synchronize
```

 ### Assessment question

 **Q: What should happen to an important event generated while communication is unavailable?**

 **Answer:**\
 It should be retained locally, subject to storage and retention policies, and synchronized when communication is restored.

---

 # 6.13 Local Storage

 Local non-volatile storage serves several functions:

 - event buffering;
- communication-loss operation;
- configuration;
- device state;
- diagnostics;
- security records;
- update metadata.

 The architecture distinguishes:

 | Data type | Example |
| --- | --- |
| Operational | Events |
| Configuration | Device policies |
| Security-sensitive | Credentials/metadata |
| Diagnostic | Fault and health records |

The device should not retain raw sensor data indefinitely unless there is an explicit operational justification.

 ### Study question

 **Q: How does local storage contribute to resilience?**

 **Answer:**\
 It allows important information to be retained during communication outages so that events are not necessarily lost and can be synchronized after connectivity returns.

---

 # 6.14 Secure Hardware

 SSP should use hardware security mechanisms where justified.

 Potential capabilities include:

 - protected device identity;
- secure key storage;
- cryptographic acceleration;
- secure boot;
- trusted execution;
- protected configuration;
- tamper-related security state.

 A secure element or equivalent mechanism may be appropriate.

 ### Core principle

 > **Compromise of ordinary application software should not automatically expose all device credentials.**

 ### Assessment question

 **Q: What is the primary purpose of protected key storage?**

 **Answer:**\
 To prevent device credentials and cryptographic keys from being directly exposed through ordinary application software or other less-trusted parts of the system.

---

 # 6.15 Secure Boot and Firmware Integrity

 The intended trust chain is:

```
Hardware root of trust
        ↓
Boot verification
        ↓
Trusted firmware
        ↓
Trusted application
        ↓
Authorized configuration
```

 The purpose is to prevent unauthorized or modified firmware from executing.

 This is particularly important for remotely deployed devices because physical access for manual recovery may not be available.

 ### Assessment question

 **Q: What does secure boot protect against?**

 **Answer:**\
 It helps prevent unauthorized or integrity-compromised firmware from being executed by establishing a verified chain of trust during device startup.

---

 # 6.16 Tamper Detection

 Tamper detection may involve:

 - enclosure opening;
- attachment/removal;
- unexpected orientation;
- abnormal movement;
- communication interruption;
- sensor inconsistency;
- power interruption;
- unauthorized configuration.

 Importantly, tamper information should be treated as contextual information rather than merely a binary signal.

 For example:

```
Tamper indication
      +
Movement
      +
Position
      +
Communication state
      +
Recent history
      ↓
Contextual tamper assessment
```

 ### Study question

 **Q: Why is contextual tamper detection preferable to a simple binary tamper flag?**

 **Answer:**\
 Because combining hardware resource usage and energy consumption should increase or decrease according to the operational requirements of the current state rather than remaining permanently at maximum for convenience, availability or experimentation rather than for production cost, size, power, RF, security or manufacturability. Treating it as tamper information with movement, position, communication state and history can provide more useful information about what actually happened and can support more appropriate event interpretation.

---

 # 6.17 Device Health Monitoring

 The device should monitor its own operational state.

 Important parameters include:

 - battery state;
- charging state;
- processor state;
- memory;
- sensor availability;
- positioning availability;
- communication status;
- storage utilization;
- firmware version;
- security state;
- temperature where relevant.

 This supports fleet management and predictive maintenance.

 Health reporting should also be adaptive rather than necessarily continuous.

---

 # 6.18 Power Architecture

 The power architecture supplies controlled energy to:

 - processor;
- positioning subsystem;
- motion sensors;
- local radio;
- wide-area radio;
- storage;
- security hardware;
- auxiliary circuitry.

 Conceptually:

```
Battery
   ↓
Power management
   ├── Sensors
   ├── MCU/SoC
   ├── Local radio
   ├── Wide-area radio
   └── Security/storage
             ↓
       Adaptive policy
```

 The power architecture must support selective activation and low-power states wherever practical.

---

 # 6.19 Device Operating Modes

 The hardware should support several operating states.

 ### Mode 0 — Deep low power

 Minimal activity.

 ### Mode 1 — Normal monitoring

 Routine sensing, positioning and communication.

 ### Mode 2 — Elevated monitoring

 Higher sensing and/or processing because contextual conditions justify it.

 ### Mode 3 — Critical monitoring

 Resources are prioritized for immediate event handling.

 ### Mode 4 — Connectivity-loss operation

 Local functions continue while communication recovery is attempted.

 ### Mode 5 — Recovery/maintenance

 Diagnostics, updates and controlled maintenance activities.

 ### Important distinction

 The **hardware provides the capability** for these states.

 The **software determines the transition logic**.

---

 # 6.20 Energy-Proportional Hardware

 The fundamental relationship is:

 **Operational significance → Resource allocation**

 Normal:

```
Normal state
   ↓
Lower sensing
   ↓
Lower processing
   ↓
Lower communication
   ↓
Lower energy
```

 Potential event:

```
Potential event
   ↓
Higher sensing
   ↓
More processing
   ↓
Priority communication
   ↓
Higher energy
```

 This is a core SSP design concept.

 ### Assessment question

 **Q: What does "energy proportionality" mean in SSP?**

 **Answer:**\
 It means that hardware resource usage and energy consumption should increase or decrease according to the operational requirements of the current state rather than remaining permanently at maximum activity.

---

 # 6.21 Battery and Energy Storage

 Battery selection must be based on the complete operating profile rather than capacity alone.

 Important parameters include:

 - capacity;
- voltage;
- discharge characteristics;
- peak current;
- charging behavior;
- temperature performance;
- physical size;
- safety;
- cycle life;
- expected autonomy.

 Peak current is particularly relevant to radio transmission and positioning operations.

 The battery-management system should support appropriate:

 - state-of-charge estimation;
- charging control;
- electrical protection;
- low-voltage protection;
- temperature protection;
- battery-health information where supported.

---

 # 6.22 Energy Budget

 A preliminary SSP energy model is:

 **E\_total = E\_sensing + E\_processing \+ E\_positioning + E\_communication \+ E\_storage + E\_security \+ E\_idle**

 The important point is that energy consumption depends on operating state.

 For each state, engineering analysis should determine:

 - average current;
- peak current;
- duty cycle;
- energy per event;
- state duration;
- expected daily energy consumption.

 This information eventually determines battery autonomy.

 ### Assessment question

 **Q: Why is calculating energy consumption from a single continuous maximum-load condition inadequate?**

 **Answer:**\
 Because SSP operates adaptively. Different operating states have different duty cycles and resource usage. A realistic energy model must therefore represent the time spent in each state and the energy consumed by each function.

---

 # 6.23 Hardware Interfaces

 Potential processor interfaces include:

 - I²C;
- SPI;
- UART;
- GPIO;
- USB where required;
- ADC;
- PWM;
- security interfaces.

 The final allocation depends on selected components.

 An important security principle is that unused externally accessible interfaces should not simply remain exposed in a production device.

---

 # 6.24 Antenna Architecture

 Radio performance depends heavily on physical antenna implementation.

 The design must consider:

 - GNSS antenna;
- cellular/wide-area antenna;
- BLE antenna;
- placement;
- enclosure;
- body proximity;
- interference;
- simultaneous-radio operation;
- impedance matching;
- certification.

 For wearable SSP devices, human-body proximity can significantly influence RF performance.

 Therefore, RF testing should use the intended physical configuration rather than relying exclusively on isolated-module measurements.

 ### Assessment question

 **Q: Why should RF testing be performed with the intended wearable configuration?**

 **Answer:**\
 Because the human body, enclosure, orientation and antenna placement can alter RF performance. Measurements from an isolated module may therefore not accurately represent real deployment performance.

---

 # 6.25 Mechanical Architecture

 For a wearable SSP device, important characteristics include:

 - compact size;
- low weight;
- reliable attachment;
- comfort;
- environmental protection;
- tamper resistance;
- water/dust resistance;
- impact resistance;
- serviceability;
- charging access;
- RF performance.

 The architecture should distinguish:

 **Common electronic platform**

 from

 **Deployment-specific mechanical implementation**

 This allows different physical SSP variants without necessarily redesigning the complete electronic architecture.

---

 # 6.26 Environmental and Thermal Design

 Environmental requirements can include:

 - temperature;
- humidity;
- water;
- dust;
- vibration;
- shock;
- impact;
- electromagnetic interference.

 Thermal design becomes particularly important when using:

 - high-performance processors;
- cellular radios;
- continuous positioning;
- computationally intensive workloads;
- charging circuits.

 Reducing unnecessary computation and communication can therefore provide two benefits:

 **lower energy consumption \+ lower heat generation**

---

 # 6.27 Hardware–Software Partitioning

 An important engineering task is determining which functions belong primarily to hardware and which belong to software.

 | Function | Hardware | Software |
| --- | --- | --- |
| Sensor acquisition | Sensor/interface | Sampling/configuration |
| Positioning | GNSS/radio | Validation/context |
| Motion detection | IMU | Classification |
| Event detection | Compute capability | Event algorithms |
| Device identity | Secure hardware | Credential management |
| Communication | Radio | Protocol/session management |
| Energy control | Power hardware | State policy |
| Storage | Memory | Retention policy |
| Tamper | Physical/electronic sensing | Interpretation |
| AI | Compute capability | Model execution |
| Diagnostics | Hardware telemetry | Health assessment |

### Assessment question

 **Q: Why is hardware–software partitioning important?**

 **Answer:**\
 It prevents unnecessary hardware complexity while allowing software behavior, algorithms and AI models to evolve without requiring a complete hardware redesign.

---

 # 6.28 Hardware Modularity

 The SSP device is decomposed into modular subsystems:

```
SSP Device
│
├── Processing
├── Positioning
├── Motion sensing
├── Local radio
├── Wide-area communication
├── Secure identity
├── Storage
├── Power management
├── Battery
├── Tamper detection
└── Mechanical enclosure
```

 Modularity supports:

 - component replacement;
- technology evolution;
- alternative deployment configurations;
- supply-chain resilience;
- maintenance;
- future product versions.

 ### Study question

 **Q: How does modularity reduce engineering risk?**

 **Answer:**\
 It prevents one component decision from unnecessarily determining the complete device architecture and makes it easier to replace, upgrade or adapt individual subsystems.

---

 # 6.29 Prototype Hardware Strategy

 The first prototype should validate the architectural assumptions with the greatest uncertainty.

 It should demonstrate at least:

 - positioning;
- motion sensing;
- local processing;
- local events;
- communication;
- buffering;
- adaptive modes;
- battery monitoring;
- device identity;
- representative security;
- Edge/Mobile interaction.

 Development boards and commercial modules may be used.

 However:

 > **Prototype hardware must not automatically be interpreted as final product hardware.**

 ### Assessment question

 **Q: Why can development-board hardware be misleading if documented poorly?**

 **Answer:**\
 Because a development board may be selected for convenience, availability or experimentation rather than for production cost, size, power, RF, security or manufacturability. Treating it as the final design could therefore create incorrect assumptions.

---

 # 6.30 Prototype-to-Product Evolution

 The intended progression is:

```
Development hardware
        ↓
Functional prototype
        ↓
Engineering prototype
        ↓
Integrated device
        ↓
Pilot hardware
        ↓
Production-oriented design
```

 Each stage progressively refines:

 - component selection;
- PCB integration;
- energy consumption;
- RF;
- enclosure;
- thermal behavior;
- security;
- manufacturability;
- cost;
- environmental performance.

 The architecture should remain relatively stable while implementation becomes increasingly optimized.

---

 # 6.31 Preliminary Hardware Bill of Functions

 | Subsystem | Function | Priority |
| --- | --- | --- |
| MCU/SoC | Local processing/control | Mandatory |
| GNSS | Outdoor positioning | Mandatory |
| IMU | Motion sensing | Mandatory |
| Local radio | Proximity/Edge interaction | High |
| Wide-area radio | Remote communication | Deployment-dependent mandatory |
| Non-volatile storage | Buffering/configuration | Mandatory |
| Secure identity | Authentication/key protection | Mandatory |
| Power management | Energy control | Mandatory |
| Battery | Autonomous operation | Mandatory |
| Tamper sensing | Integrity monitoring | High |
| Health monitoring | Device status | High |
| Environmental sensing | Context/health | Medium |
| Additional sensors | Scenario-specific | Future |

---

 # 6.32 Component Selection Criteria

 A component should ultimately be evaluated against a common engineering framework.

 ### Processor

 - computational performance;
- power modes;
- memory;
- interfaces;
- security;
- ecosystem;
- lifecycle;
- cost.

 ### Positioning

 - accuracy;
- acquisition time;
- sensitivity;
- supported constellations;
- power;
- assistance capabilities.

 ### Motion sensors

 - noise;
- range;
- sampling;
- power;
- size.

 ### Communication

 - coverage;
- latency;
- bandwidth;
- power;
- security;
- certification;
- availability.

 ### Storage

 - capacity;
- endurance;
- retention;
- write performance;
- power.

 ### Security hardware

 - key protection;
- identity;
- cryptographic support;
- secure boot;
- lifecycle.

 ### Battery

 - energy density;
- peak current;
- safety;
- charging;
- lifetime;
- dimensions.

 ### Key engineering rule

 > **Component selection should be justified quantitatively wherever practical.**

---

 # 6.33 Hardware Traceability

 Hardware decisions must connect back to system requirements.

 | Requirement | Hardware implication | Verification |
| --- | --- | --- |
| Local decisions | Embedded processor | Local-processing test |
| Position monitoring | GNSS | Positioning test |
| Motion awareness | IMU | Motion test |
| Proximity | Local radio | Proximity test |
| Communication resilience | Storage | Outage test |
| Authentication | Secure identity | Security test |
| Energy adaptation | Low-power hardware | Energy test |
| Tamper awareness | Tamper sensing | Tamper test |
| Privacy | Local processing/storage | Data-flow test |
| Fleet operation | Management capability | Fleet test |

This creates the chain:

 **Requirement → Architecture → Hardware → Test**

---

 # 6.34 Hardware Risks

 The major unresolved hardware questions include:

 ### HR-01 — Positioning performance

 Can the required positioning performance be achieved in real deployment environments?

 ### HR-02 — Battery autonomy

 Can the required monitoring behavior be maintained for the target duration?

 ### HR-03 — Communication energy

 How much of the energy budget is consumed by wide-area communication?

 ### HR-04 — Local computation

 How much processing is actually required?

 ### HR-05 — Wearable form factor

 Can all required hardware fit within acceptable size and weight?

 ### HR-06 — RF performance

 How does body proximity affect wireless performance?

 ### HR-07 — Tamper resistance

 Which tamper mechanisms provide meaningful operational value?

 ### HR-08 — Cost

 Can the architecture achieve the intended deployment economics?

---

 # 6.35 Hardware KPIs

 The principal KPIs include:

 ### Processing

 - local processing latency;
- CPU utilization;
- memory utilization;
- inference latency.

 ### Positioning

 - position error;
- time to first fix;
- positioning availability;
- energy per positioning operation.

 ### Motion

 - sampling rate;
- classification performance;
- sensor availability;
- false-event rate.

 ### Communication

 - transmission energy;
- success rate;
- connection time;
- recovery time.

 ### Energy

 - average current;
- peak current;
- energy per event;
- energy per mode;
- battery autonomy.

 ### Security

 - secure-boot verification;
- unauthorized firmware rejection;
- credential protection;
- tamper detection.

 ### Physical

 - mass;
- dimensions;
- environmental tolerance;
- attachment integrity.

---

 # 6.36 Assessment:/confidence and validityNo. Prototype hardware is intended to validate architectural assumptions. Production hardware must additionally satisfy requirements for power, size, RF system architecture. Starting with individual components risks creating an arbitrary architecture based on whatever hardware happens, energy, security, infrastructure, regulatory requirements, cost and deployment environment. Chapter 7 evaluates. Therefore, power management, processor states, radio control and sensor activation must support multiple device architecture for a wearable deployment. Explain why each major subsystem is required and how the subsystems cooperate during a Short-Answer Questions

 ### Q1. What is the principal role of the SSP device?

 **Answer:**\
 It is the physical sensing and embedded-processing node that connects the monitored environment to the Edge/Mobile and Cloud layers.

 ### Q2. What are the three principal processing layers established in Chapter 5?

 **Answer:**\
 Device, Edge/Mobile and Cloud.

 ### Q3. Why does SSP require local processing?

 **Answer:**\
 To support low-latency decisions, resilience, privacy, energy efficiency and operation during connectivity disruption.

 ### Q4. What does GNSS provide?

 **Answer:**\
 Primarily position and timing, together with quality/status information where available.

 ### Q5. Why is an IMU useful?

 **Answer:**\
 It provides motion and orientation information that complements positioning and supports movement classification, tamper detection and contextual interpretation.

 ### Q6. What is the purpose of local non-volatile storage?

 **Answer:**\
 To retain events, configuration, diagnostics and other required information, particularly during communication loss.

 ### Q7. What is secure hardware intended to protect?

 **Answer:**\
 Device identity, cryptographic keys and other security-sensitive information.

 ### Q8. What is secure boot?

 **Answer:**\
 A mechanism that establishes a verified chain of trust so that only authenticated/integrity-verified firmware is allowed to execute.

 ### Q9. Why is battery capacity alone insufficient for battery selection?

 **Answer:**\
 Because actual autonomy depends on duty cycles, peak currents, radio use, positioning, processing, operating states, temperature and other factors.

 ### Q10. Why is adaptive hardware important?

 **Answer:**\
 Because SSP does not require maximum sensing, processing and communication continuously. Adaptive resource use reduces energy consumption while preserving higher activity when operational conditions require it.

---

 # 6.37 Assessment: Scenario Questions

 ## Scenario 1 — Loss of Connectivity

 An SSP device detects a significant event but cannot communicate with the Edge.

 **What should the hardware support?**

 **Answer:**

 1. Continue selected local processing.
2. Generate a structured local event.
3. Store the event in non-volatile memory.
4. Continue attempting communication according to policy.
5. Transmit the retained event when connectivity returns.
6. Synchronize with the higher layer.

 The important principle is **graceful degradation rather than uncontrolled failure**.

---

 ## Scenario 2 — Poor Positioning Quality

 The device reports a position but the positioning subsystem indicates degraded quality.

 **Should the position automatically be treated as equivalent to a high-confidence measurement?**

 **Answer:**\
 No. Position should be represented together with quality/confidence and validity information. Higher-level event interpretation should account for the uncertainty.

---

 ## Scenario 3 — Unexpected Device Movement

 The enclosure reports a possible tamper condition while the IMU simultaneously detects movement.

 **Why should SSP combine these signals?**

 **Answer:**\
 Because the combination provides more contextual information than either signal independently. Position, movement, tamper state, communication state and recent history can improve event interpretation.

---

 ## Scenario 4 — Critical Event

 A potential critical event is detected near a protected boundary.

 **What should happen to resource allocation?**

 **Answer:**\
 The system can transition toward a higher monitoring state, increasing relevant sensing, processing and communication priority according to policy.

 The principle is:

 **Higher operational significance → greater resource allocation**

---

 ## Scenario 5 — Prototype Selection

 A development team selects a development board because it is inexpensive and easy to program.

 **Does this automatically mean it is the final SSP hardware?**

 **Answer:**\
 No. Prototype hardware is intended to validate architectural assumptions. Production hardware must additionally satisfy requirements for power, size, RF performance, security, manufacturability, environmental robustness, cost and lifecycle support.

---

 # 6.38 Assessment: Design-Reasoning Questions

 ### Q1. Why is hardware architecture defined before individual component selection?

 **Answer:**\
 Because component selection should implement an already-defined system architecture. Starting with individual components risks creating an arbitrary architecture based on whatever hardware happens to be available.

 ### Q2. Why is communication deliberately left open in Chapter 6?

 **Answer:**\
 Because communication technology depends on coverage, latency, energy, security, infrastructure, regulatory requirements, cost and deployment environment. Chapter 7 evaluates these factors systematically.

 ### Q3. Why is modularity particularly important for SSP?

 **Answer:**\
 Communication technologies, processors, sensors and security components can evolve. A modular design permits individual subsystems to change without requiring a complete architectural redesign.

 ### Q4. Why should hardware support software evolution?

 **Answer:**\
 Many SSP functions, particularly event interpretation, control algorithms and AI models, are expected to evolve. Sufficient compute, storage and secure update mechanisms allow the hardware platform to support those changes.

 ### Q5. What is the relationship between adaptive monitoring and hardware design?

 **Answer:**\
 Adaptive monitoring requires hardware capable of changing sensing, processing and communication activity. Therefore, power management, processor states, radio control and sensor activation must support multiple operating modes.

---

 # 6.39 Assessment: Architecture-to-Hardware Traceability Exercise

 Complete the following chain:

 **Requirement → Hardware → Verification**

 | Requirement | Expected hardware response | Example verification |
| --- | --- | --- |
| Position monitoring | GNSS/positioning subsystem | Position test |
| Motion awareness | IMU | Motion test |
| Local decision capability | MCU/SoC | Local-processing test |
| Communication resilience | Non-volatile storage | Connectivity-outage test |
| Device authentication | Secure identity | Authentication test |
| Adaptive energy use | Low-power hardware | Energy-profile test |
| Tamper detection | Tamper sensing | Tamper test |
| Privacy | Local processing/storage | Data-flow analysis |
| Autonomous operation | Battery + PMIC | Autonomy test |

### Learning objective

 The student should understand that a hardware component is not justified merely because it exists.

 It must be connected to:

 **Requirement → Function → Component → Interface → Power → Verification**

---

 # 6.40 Assessment: Multiple-Choice Questions

 ### 1\. Which component is primarily responsible for local SSP computation?

 A. Battery\
 B. MCU/SoC\
 C. Antenna\
 D. Enclosure

 **Answer: B — MCU/SoC**

---

 ### 2\. Which function most directly supports event buffering during connectivity loss?

 A. GNSS antenna\
 B. IMU\
 C. Non-volatile storage\
 D. Battery charger

 **Answer: C — Non-volatile storage**

---

 ### 3\. Which information representation is most appropriate for SSP positioning?

 A. Latitude only\
 B. Longitude only\
 C. Position + confidence/quality + validity + time\
 D. Position without metadata

 **Answer: C**

---

 ### 4\. Which is NOT a primary reason for local processing?

 A. Privacy\
 B. Resilience\
 C. Reduced unnecessary communication\
 D. Guaranteed unlimited battery life

 **Answer: D**

---

 ### 5\. What is the purpose of secure boot?

 A. Increase GNSS accuracy\
 B. Reduce antenna size\
 C. Verify trusted software before execution\
 D. Increase battery capacity

 **Answer: C**

---

 ### 6\. Which subsystem provides motion information?

 A. IMU\
 B. Secure element\
 C. Flash memory\
 D. PMIC

 **Answer: A**

---

 ### 7\. Which statement best describes prototype hardware?

 A. It must always be identical to production hardware.\
 B. It exists primarily to validate engineering assumptions.\
 C. It eliminates the need for later hardware engineering.\
 D. It determines the Cloud architecture automatically.

 **Answer: B**

---

 ### 8\. Which factor is particularly important for wearable antenna design?

 A. Human-body proximity\
 B. Database schema\
 C. Cloud storage capacity\
 D. User-interface color

 **Answer: A**

---

 ### 9\. What does graceful degradation mean?

 A. The device always operates at maximum power.\
 B. Failure of one non-critical function does not necessarily disable the complete system.\
 C. Every failure shuts down the device.\
 D. The Cloud takes over every function immediately.

 **Answer: B**

---

 ### 10\. Which equation represents the preliminary SSP energy model?

 A. E = Battery capacity only\
 B. E = Position \+ Motion\
 C. E\_total = sensing \+ processing + positioning \+ communication + storage \+ security + idle\
 D. E = communication only

 **Answer: C**

---

 # 6.41 Assessment: True or False

 ### 1\. SSP hardware should be selected solely according to maximum computational performance.

 **Answer: False.**

 It should provide sufficient performance while controlling energy, cost, thermal load and complexity.

 ### 2\. The SSP device should automatically transmit all raw sensor measurements.

 **Answer: False.**

 Local processing and data minimization are fundamental architectural principles.

 ### 3\. Position confidence can be relevant to SSP event interpretation.

 **Answer: True.**

 ### 4\. Local storage can support operation during communication outages.

 **Answer: True.**

 ### 5\. Secure identity is only a Cloud responsibility.

 **Answer: False.**

 The device requires a protected identity suitable for authentication.

 ### 6\. Hardware and software should be completely independent.

 **Answer: False.**

 Hardware capabilities and software responsibilities must be deliberately partitioned.

 ### 7\. A prototype development board is automatically the production hardware.

 **Answer: False.**

 ### 8\. Adaptive operation can reduce both energy consumption and thermal generation.

 **Answer: True.**

 ### 9\. Chapter 6 permanently selects the SSP wide-area communication technology.

 **Answer: False.**

 Communication technology selection is deferred to Chapter 7.

 ### 10\. Hardware design should be traceable to system requirements.

 **Answer: True.**

---

 # 6.42 Assessment: Fill in the Blanks

 1. The SSP device is an autonomous embedded **\_\_\_\_\_**.

 **Answer:** computing node

 2. The three principal architectural layers are Device, Edge/Mobile and **\_\_\_\_\_**.

 **Answer:** Cloud

 3. The main local processing component is the **\_\_\_\_\_ / SoC**.

 **Answer:** MCU

 4. GNSS provides positioning together with relevant quality and **\_\_\_\_\_** information.

 **Answer:** validity

 5. An accelerometer and gyroscope form part of the **\_\_\_\_\_ sensing** subsystem.

 **Answer:** motion

 6. Events can be retained during connectivity loss using **\_\_\_\_\_ storage**.

 **Answer:** non-volatile

 7. Secure boot establishes a **\_\_\_\_\_ of trust**.

 **Answer:** chain

 8. Adaptive resource allocation links operational significance to **\_\_\_\_\_ allocation**.

 **Answer:** resource

 9. Battery autonomy depends on operating **\_\_\_\_\_**, not merely nominal capacity.

 **Answer:** profile

 10. The next chapter defines the SSP **\_\_\_\_\_ architecture**.

 **Answer:** communication

---

 # 6.43 Integrated Assessment Question

 ### Question

 Design a conceptual SSP device architecture for a wearable deployment. Explain why each major subsystem is required and how the subsystems cooperate during a critical event.

 ### Answer

 A conceptual wearable SSP device should contain:

 - an **MCU/SoC** for local processing and control;
- a **GNSS subsystem** for outdoor positioning;
- an **IMU** for motion sensing;
- a **local radio**, such as BLE, for proximity and Edge/Mobile interaction;
- a **wide-area communication subsystem** where autonomous remote connectivity is required;
- **non-volatile storage** for event buffering and configuration;
- **secure hardware** for device identity and key protection;
- **power-management hardware**;
- a **battery**;
- **tamper detection**;
- device-health monitoring.

 During a critical event, the device may transition from normal monitoring to critical monitoring. Relevant sensors increase their activity according to policy, local processing interprets the observations, and a structured high-priority event is generated.

 The event may contain:

 **Device identity + timestamp \+ position + position confidence \+ motion state + proximity \+ device state + event type + severity + confidence**

 The communication subsystem then prioritizes the event for transmission to the Edge/Mobile layer. If connectivity is temporarily unavailable, the device retains the event locally and attempts synchronization when communication returns.

 The architecture therefore supports:

 **Sense → Interpret → Classify → Prioritize → Communicate → Recover if necessary**

 rather than relying on continuous raw-data transmission.

---

 # 6.44 Final Chapter 6 Knowledge Check

 A student who understands Chapter 6 should be able to explain the following without referring to the chapter:

 1. **Why does SSP need local processing?**\
    To provide local autonomy, lower latency, resilience, privacy and potentially lower communication energy.
2. **Why are GNSS and IMU complementary?**\
    GNSS provides positioning while the IMU provides motion/orientation information useful for contextual interpretation.
3. **Why is local storage important?**\
    It provides buffering, configuration storage and continuity during communication disruption.
4. **Why is secure hardware required?**\
    To protect device identity, keys and other security-sensitive functions.
5. **Why does SSP need multiple operating modes?**\
    To adapt sensing, processing and communication to operational conditions and conserve energy.
6. **Why isn't battery capacity enough to predict autonomy?**\
    Because actual consumption depends on duty cycles, operating states, positioning, communication, processing and other loads.
7. **Why should hardware be modular?**\
    To support technology evolution, maintenance, alternative deployments and prototype-to-product development.
8. **Why is the communication technology not finalized here?**\
    Because Chapter 7 must evaluate communication options against system-level requirements.
9. **Why must hardware decisions be traceable to requirements?**\
    To ensure every major hardware element has an engineering justification and a corresponding verification method.
10. **What is the central hardware-design principle of SSP?**\
     Provide sufficient local capability to support autonomous, secure and adaptive operation without unnecessary hardware complexity, energy consumption or cost.

---

 # 6.45 Chapter 6 Exam-Level Summary

 The most important concepts to retain are:

 > **SSP is an embedded cyber-physical device, not merely a location tracker.**

 > **Local processing converts raw measurements into relevant information before transmission.**

 > **Position should be represented together with confidence, quality and validity.**

 > **Motion sensing complements positioning and supports contextual event interpretation.**

 > **Local storage enables resilience during communication disruption.**

 > **Secure hardware establishes protected device identity and supports the device trust model.**

 > **Secure boot protects firmware integrity.**

 > **Tamper detection should be interpreted in context rather than treated only as a binary signal.**

 > **Hardware must support adaptive operating states.**

 > **Energy consumption must be modelled from realistic operating profiles.**

 > **Prototype hardware validates architectural assumptions but is not automatically production hardware.**

 > **Hardware selection follows requirements and architecture; it does not define them arbitrarily.**

 The complete engineering progression remains:

 **Requirements → Architecture → Hardware → Communication → Software → Data → Intelligence/AI → Energy/Performance → Cloud → PoC → Economics → Validation**

 And Chapter 6 establishes the physical foundation for the next step:

 **Hardware capability → Communication architecture → Chapter 7**
