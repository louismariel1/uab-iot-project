 # Chapter 6\. SSP Hardware and Device Architecture

 ## 6.1 Purpose of the Hardware Design

 Chapter 5 established the overall SSP Device–Edge/Mobile–Cloud architecture and allocated system functions between the principal processing layers.

 This chapter translates that architectural structure into the physical and electronic design of the SSP device.

 The objective is not to select components merely because they are technically capable of performing individual functions. The hardware must support the system-level requirements established in Chapter 3 while remaining consistent with the architectural principles identified in Chapters 4 and 5:

 - distributed intelligence;
- adaptive monitoring;
- context-aware event interpretation;
- resilient operation;
- privacy-aware processing;
- secure device operation;
- energy efficiency;
- scalable deployment;
- lifecycle maintainability.

 The fundamental hardware-design relationship is therefore:

 **System requirement → Hardware function → Component capability → Interface → Power requirement → Verification**

 The SSP device should be regarded as an autonomous embedded computing node rather than simply as a GPS tracker.

 Its hardware must support a combination of:

 **Sensing → Positioning → Local processing → Communication → Security → Power management → Device integrity**

 while providing sufficient flexibility for the subsequent software and AI architecture.

---

 ## 6.2 Hardware Role Within the SSP Architecture

 The SSP device represents the physical boundary between the monitored environment and the digital SSP system.

 Its principal functions are:

 1. acquire physical and contextual information;
2. determine or assist in determining device position;
3. monitor movement and device state;
4. perform selected local processing;
5. generate structured local events;
6. communicate relevant information to the Edge/Mobile layer and, where required, directly to the wider network;
7. maintain operation during temporary connectivity loss;
8. protect device identity, credentials and configuration;
9. monitor its own health and energy state.

 The device therefore provides the first stage of the distributed SSP intelligence chain:

 **Environment → Sensors → Local processing → Communication → Edge/Mobile → Cloud**

 The hardware architecture shall ensure that the device can perform critical local functions without assuming permanent cloud connectivity.

---

 ## 6.3 SSP Device Functional Architecture

 The conceptual hardware architecture is:

```
                         ┌───────────────────────┐
                         │     SSP DEVICE        │
                         │                       │
                         │  ┌─────────────────┐  │
                         │  │ Positioning     │  │
                         │  │ GNSS / Context  │  │
                         │  └────────┬────────┘  │
                         │           │           │
                         │  ┌────────▼────────┐  │
                         │  │ Motion / Sensor  │  │
                         │  │ Subsystem        │  │
                         │  └────────┬────────┘  │
                         │           │           │
                         │  ┌────────▼────────┐  │
                         │  │ Embedded        │  │
                         │  │ Processing      │  │
                         │  │ MCU / SoC      │  │
                         │  └───┬────────┬────┘  │
                         │      │        │        │
                         │      │        │        │
                         │ ┌────▼───┐ ┌──▼─────┐ │
                         │ │ Local  │ │ Secure │ │
                         │ │ Storage│ │ Element│ │
                         │ └────────┘ └────────┘ │
                         │                       │
                         │  ┌─────────────────┐  │
                         │  │ Communication   │  │
                         │  │ Subsystem       │  │
                         │  └────────┬────────┘  │
                         │           │           │
                         │  ┌────────▼────────┐  │
                         │  │ Power Management │  │
                         │  │ + Battery       │  │
                         │  └─────────────────┘  │
                         │                       │
                         │  Tamper / Health /    │
                         │  Environmental State  │
                         └───────────┬───────────┘
                                     │
                                     ▼
                              Edge / Mobile
```

 This is a functional representation rather than a final schematic.

 The exact semiconductor devices, radio modules, memory sizes, battery technology and mechanical implementation shall be selected during detailed engineering.

---

 ## 6.4 Hardware Design Principles

 The SSP hardware design follows several principles.

 ### HD-01 — Local autonomy

 The device shall retain sufficient processing capability to perform functions that cannot safely depend on continuous cloud connectivity.

 ### HD-02 — Energy proportionality

 Hardware resources shall support different operating modes so that energy consumption can be adapted to operational requirements.

 ### HD-03 — Modular communication

 The communication subsystem should be sufficiently modular that communication technology can evolve without requiring complete redesign of the sensing and processing platform.

 ### HD-04 — Secure identity

 The device shall possess a protected identity suitable for authentication within the SSP architecture.

 ### HD-05 — Sensor extensibility

 The hardware should provide sufficient interfaces and processing capability to accommodate additional sensing where justified by future deployment scenarios.

 ### HD-06 — Graceful degradation

 Failure or unavailability of a non-critical hardware function should not automatically disable the entire device.

 ### HD-07 — Lifecycle support

 The hardware shall support provisioning, diagnostics, secure software updates and controlled replacement.

 ### HD-08 — Prototype-to-product continuity

 The selected architecture should allow the prototype to evolve toward a deployable product without requiring a fundamentally different system architecture.

---

 ## 6.5 Embedded Processing Subsystem

 The central embedded processor is the principal hardware element responsible for local SSP intelligence.

 It shall provide sufficient resources for:

 - sensor acquisition;
- sensor preprocessing;
- motion-state estimation;
- positioning-data processing;
- geofence evaluation where appropriate;
- event generation;
- communication management;
- power-state management;
- local buffering;
- device-health monitoring;
- security functions;
- lightweight local inference where justified.

 The processor may be implemented as a low-power microcontroller, microprocessor, system-on-chip or a combination of processing elements.

 The final selection shall depend on:

 - computational performance;
- power consumption;
- memory requirements;
- peripheral interfaces;
- security capabilities;
- real-time performance;
- software ecosystem;
- availability;
- cost;
- lifecycle support.

 The architecture should avoid selecting a processor solely on the basis of maximum computational performance.

 Excess processing capability can increase:

 - power consumption;
- thermal requirements;
- component cost;
- software complexity;
- attack surface.

 The appropriate target is therefore **sufficient local intelligence at the lowest practical resource cost**.

---

 ## 6.6 Local Processing Requirements

 The SSP processor should support a hierarchy of local processing.

 ### Level 1 — Sensor processing

 Raw sensor measurements are converted into usable quantities.

 Examples include:

 - acceleration;
- angular velocity;
- motion state;
- positioning measurements;
- battery state;
- communication state.

 ### Level 2 — Context interpretation

 Multiple measurements are combined to determine the current device state.

 Examples include:

 - stationary;
- walking;
- travelling;
- unexpected movement;
- possible sensor inconsistency;
- positioning degradation.

 ### Level 3 — Event generation

 Relevant changes are converted into structured events.

 Examples include:

 - geofence transition;
- proximity condition;
- tamper condition;
- abnormal movement;
- communication failure;
- low-battery condition.

 ### Level 4 — Local decision

 Where required, the device determines whether an event should trigger immediate action or higher-priority communication.

 This hierarchy avoids transmitting every raw measurement to higher layers.

---

 ## 6.7 Positioning Subsystem

 Positioning is a fundamental SSP hardware function.

 The primary outdoor positioning mechanism is expected to be based on GNSS or an equivalent satellite-navigation technology, subject to final technology selection.

 The positioning subsystem should provide:

 - position;
- timestamp;
- positioning quality indicators;
- satellite or solution-status information where available;
- velocity or movement information where available;
- positioning validity state.

 The hardware architecture should avoid treating a position value as inherently trustworthy.

 Instead, positioning information should be represented conceptually as:

 **Position + Time + Quality/Confidence + Validity**

 This allows downstream processing to distinguish between:

 - high-confidence position;
- degraded position;
- unavailable position;
- potentially inconsistent position.

 The positioning subsystem shall also support appropriate low-power operating modes.

---

 ## 6.8 Motion-Sensing Subsystem

 Motion sensing provides information complementary to positioning.

 The baseline SSP motion subsystem should consider:

 - accelerometer;
- gyroscope where justified;
- optional additional motion-related sensing depending on deployment requirements.

 The accelerometer provides information useful for:

 - movement detection;
- activity-state estimation;
- vibration;
- orientation changes;
- tamper detection;
- sensor plausibility checking.

 The gyroscope can provide additional information concerning:

 - angular motion;
- orientation changes;
- device manipulation;
- movement classification.

 The final sensor combination should be justified against:

 **information value versus energy consumption versus hardware cost versus processing requirement.**

 A sensor shall therefore not be included simply because it is available commercially.

---

 ## 6.9 Proximity and Local Radio Subsystem

 The SSP device shall support local wireless communication where required by the architecture.

 A short-range technology such as BLE is a candidate for:

 - device association;
- protected-person device interaction;
- proximity detection;
- local configuration;
- Edge/Mobile connectivity;
- service and diagnostic functions.

 The local-radio subsystem should support configurable operation because continuous high-duty-cycle scanning can have a significant energy cost.

 The system should therefore distinguish between:

 **association**

 **periodic discovery**

 **continuous proximity monitoring**

 **event-driven communication**

 These modes may have different power and operational implications.

---

 ## 6.10 Wide-Area Communication Subsystem

 The SSP device requires a mechanism for communication beyond the local device environment when operationally required.

 Candidate technologies include cellular and other wide-area communication technologies.

 The final selection shall be made in Chapter 7 based on:

 - geographical coverage;
- bandwidth;
- latency;
- power consumption;
- network availability;
- deployment environment;
- communication cost;
- security;
- module availability;
- antenna requirements;
- regulatory constraints.

 The hardware design should nevertheless reserve sufficient architectural flexibility to support the selected wide-area communication mechanism without coupling the entire embedded system to a single communication technology.

---

 ## 6.11 Communication Redundancy and Fallback

 The hardware architecture should support the possibility that the normal communication path becomes unavailable.

 Depending on the deployment configuration, the device may use:

 **Primary local path → Edge/Mobile**

 and/or

 **Primary wide-area path → Network/Cloud**

 with local storage providing an additional fallback mechanism.

 The device should be able to detect:

 - loss of communication;
- degraded communication;
- failed association;
- repeated transmission failure;
- network unavailability.

 During a communication disruption, the processor shall continue selected local functions.

 Relevant events should be stored until the communication path becomes available again, subject to memory capacity and retention policy.

---

 ## 6.12 Local Storage

 Non-volatile local storage is required for more than conventional logging.

 It supports:

 - temporary event buffering;
- communication-loss operation;
- configuration storage;
- device state;
- diagnostic records;
- security-related records;
- update metadata;
- controlled retention of locally generated information.

 The storage architecture should distinguish between:

 **Operational data**

 **Configuration data**

 **Security-sensitive data**

 **Diagnostic data**

 Different protection and retention requirements may apply to each category.

 The device should avoid retaining raw sensor information indefinitely unless there is a defined operational reason to do so.

 This supports the privacy and data-minimization requirements established in Chapter 3.

---

 ## 6.13 Secure Hardware

 Security-sensitive operations should be supported by hardware mechanisms where technically justified.

 Potential hardware security capabilities include:

 - secure device identity;
- protected key storage;
- hardware-assisted cryptographic operations;
- secure boot support;
- trusted execution mechanisms;
- tamper-related state;
- protected configuration storage.

 A secure element or equivalent hardware security mechanism may be used where it provides sufficient benefit relative to cost and complexity.

 The purpose is to ensure that compromise of ordinary application software does not automatically expose all device credentials.

---

 ## 6.14 Secure Boot and Firmware Integrity

 The SSP device should establish a chain of trust beginning at device startup.

 Conceptually:

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

 Only authenticated and integrity-verified software should be permitted to execute where the selected hardware supports this capability.

 This is particularly important because SSP devices may operate remotely and may not have physical access available for manual recovery.

---

 ## 6.15 Tamper Detection Hardware

 Tamper detection is both a security and operational function.

 Depending on the physical implementation, relevant mechanisms may include:

 - enclosure-open detection;
- attachment/removal detection;
- unexpected orientation change;
- abnormal movement;
- communication interruption;
- sensor inconsistency;
- power interruption;
- unauthorized configuration attempt.

 Not every mechanism is required for every SSP deployment.

 The hardware should therefore provide a configurable foundation from which deployment-specific tamper policies can be implemented.

 Tamper events should be treated as structured events rather than merely as binary hardware signals.

 For example:

 **Tamper indication + movement \+ position + communication state + recent history**

 can provide more useful context than a single tamper flag.

---

 ## 6.16 Device Health Monitoring

 The SSP device shall monitor its own operational condition.

 Relevant parameters include:

 - battery state;
- charging state;
- processor state;
- memory condition;
- sensor availability;
- positioning availability;
- communication status;
- storage utilization;
- firmware version;
- security state;
- temperature where relevant.

 Health information should be available to the management layer at an appropriate reporting frequency.

 As with other SSP information, health reporting should be adaptive rather than necessarily continuous at maximum frequency.

---

 ## 6.17 Power Architecture

 Power management is one of the most important hardware-design aspects of SSP.

 The power architecture should provide controlled power to:

 - processor;
- positioning subsystem;
- motion sensors;
- local radio;
- wide-area radio;
- storage;
- security hardware;
- indicators and auxiliary circuits.

 A conceptual power architecture is:

```
                Battery
                   │
                   ▼
          Power Management
          /       |       \
         /        |        \
        ▼         ▼         ▼
     Sensors    MCU/SoC   Radios
        │         │         │
        └─────────┴─────────┘
                  │
             System state
                  │
                  ▼
          Adaptive power policy
```

 The hardware must support selective activation and low-power states where technically feasible.

---

 ## 6.18 Device Operating Modes

 The hardware architecture should support multiple operating states.

 A representative state model is:

 ### Mode 0 — Deep low-power state

 Used when the device has no immediate requirement for intensive sensing or communication.

 ### Mode 1 — Normal monitoring

 The device performs periodic sensing, positioning and communication according to the normal monitoring policy.

 ### Mode 2 — Elevated monitoring

 Monitoring frequency and/or processing intensity increases when contextual conditions justify additional information.

 ### Mode 3 — Critical monitoring

 The device prioritizes sensing, local processing and communication required for immediate event handling.

 ### Mode 4 — Connectivity-loss operation

 Selected local functions remain active while communication recovery is attempted.

 ### Mode 5 — Recovery / maintenance

 The device performs controlled diagnostics, update or maintenance functions.

 The exact state-transition policy belongs to the software and system-control design, but the hardware must be capable of supporting these modes.

---

 ## 6.19 Adaptive Hardware Resource Use

 The central hardware principle is:

 **Operational significance → Resource allocation**

 For example:

```
Normal state
    ↓
Low sensing intensity
    ↓
Low communication frequency
    ↓
Low energy consumption
```

 whereas:

```
Potential event
    ↓
Higher sensing intensity
    ↓
Additional local processing
    ↓
Higher communication priority
    ↓
Higher energy consumption
```

 The hardware therefore becomes an enabler of the adaptive-monitoring concept rather than simply a passive platform.

---

 ## 6.20 Battery and Energy Storage

 The battery system shall be selected according to the intended operating profile rather than a nominal capacity requirement alone.

 Relevant parameters include:

 - capacity;
- nominal voltage;
- discharge characteristics;
- peak current capability;
- charging characteristics;
- temperature behavior;
- physical dimensions;
- safety;
- cycle life;
- expected autonomy.

 Battery selection shall consider peak-current requirements associated with radio transmission and positioning operations.

 The battery-management subsystem should provide:

 - state-of-charge estimation;
- charging control;
- protection;
- low-voltage protection;
- temperature protection where applicable;
- battery-health information where supported.

---

 ## 6.21 Energy Budget

 The hardware design shall eventually establish an energy budget.

 A representative model is:

 **E\_total = E\_sensing + E\_processing \+ E\_positioning + E\_communication \+ E\_storage + E\_security \+ E\_idle**

 Communication and positioning may become significant contributors depending on the operating mode.

 The final energy model shall therefore be linked to the operating-state model rather than calculated from a single continuous maximum-load condition.

 For each operating mode, the project should determine:

 - average current;
- peak current;
- duty cycle;
- energy per event;
- expected duration;
- resulting daily energy consumption.

 This will provide the basis for the battery-autonomy analysis in Chapter 11.

---

 ## 6.22 Hardware Interfaces

 The embedded processor should expose appropriate interfaces for the selected peripherals.

 Potential interfaces include:

 - I²C;
- SPI;
- UART;
- GPIO;
- USB where required;
- ADC where required;
- PWM where required;
- secure communication interfaces.

 The final interface allocation shall be determined from the selected components.

 Interfaces connected to security-sensitive or externally accessible functions should be treated according to the SSP security architecture.

 Unused interfaces should not automatically remain exposed in the final product.

---

 ## 6.23 Antenna Architecture

 Wireless performance depends not only on the radio module but also on antenna implementation.

 The hardware design shall consider:

 - GNSS antenna;
- cellular or wide-area antenna;
- BLE/local-radio antenna;
- antenna placement;
- enclosure effects;
- human-body proximity;
- interference;
- simultaneous-radio operation;
- impedance matching;
- certification requirements.

 For a wearable device, antenna performance can be affected significantly by device orientation and proximity to the body.

 Therefore, RF performance shall be evaluated using the intended mechanical configuration rather than only through laboratory measurements of an isolated module.

---

 ## 6.24 Mechanical Architecture

 The mechanical design depends on the SSP deployment configuration.

 For a wearable device, relevant requirements include:

 - compact size;
- low weight;
- attachment reliability;
- comfort;
- enclosure protection;
- tamper resistance;
- water and dust resistance;
- impact resistance;
- serviceability;
- charging access;
- antenna performance.

 For a fixed device or gateway, different requirements may dominate:

 - mounting;
- external power;
- environmental protection;
- cable management;
- physical security;
- thermal management;
- maintenance access.

 The hardware architecture should therefore distinguish the **common SSP electronic platform** from **deployment-specific mechanical implementations**.

---

 ## 6.25 Environmental Requirements

 The device shall be designed for its intended operating environment.

 Environmental parameters may include:

 - operating temperature;
- storage temperature;
- humidity;
- water exposure;
- dust;
- vibration;
- shock;
- mechanical impact;
- electromagnetic interference.

 The final environmental specifications shall be derived from the intended deployment scenario.

 For a wearable deployment, the design should place particular emphasis on:

 **mechanical robustness + water resistance + attachment security + user comfort \+ battery safety.**

---

 ## 6.26 Thermal Considerations

 Thermal design becomes relevant when the device contains:

 - high-performance processors;
- cellular radios;
- continuous positioning hardware;
- charging circuits;
- high computational workloads.

 The design should avoid unnecessary thermal generation because increased temperature can affect:

 - battery life;
- component reliability;
- user comfort;
- positioning and radio performance;
- long-term device lifetime.

 Adaptive operation therefore has a secondary thermal benefit: reducing unnecessary computational and communication activity can also reduce heat generation.

---

 ## 6.27 Hardware Security Boundary

 The device shall establish clear security boundaries between:

 - trusted hardware;
- security-sensitive storage;
- operating firmware;
- application software;
- sensor interfaces;
- communication interfaces;
- external physical interfaces.

 A conceptual model is:

```
┌──────────────────────────────────────┐
│              SSP DEVICE              │
│                                      │
│  ┌──────────── Trusted ────────────┐ │
│  │ Secure identity / keys          │ │
│  │ Boot verification               │ │
│  │ Security state                  │ │
│  └─────────────────────────────────┘ │
│                  │                   │
│  ┌─────────────────────────────────┐ │
│  │ Embedded software               │ │
│  └─────────────────────────────────┘ │
│                  │                   │
│  ┌─────────────────────────────────┐ │
│  │ Sensors / Radios / Interfaces   │ │
│  └─────────────────────────────────┘ │
└──────────────────────────────────────┘
```

 This boundary will later connect directly to the security architecture defined in Chapter 12.

---

 ## 6.28 Hardware-Software Partitioning

 The SSP hardware shall not attempt to implement functions that are more appropriately handled by software.

 A preliminary allocation is:

 | Function | Hardware responsibility | Software responsibility |
| --- | --- | --- |
| Sensor acquisition | Sensor + interfaces | Sampling/configuration |
| Positioning | GNSS/radio hardware | Position validation/context |
| Motion detection | IMU | Motion classification |
| Local event detection | Processing capability | Event algorithms |
| Security identity | Secure hardware | Credential management |
| Communication | Radio hardware | Protocol/session management |
| Energy control | Power hardware | Operating-state policy |
| Storage | Non-volatile memory | Data-retention policy |
| Tamper detection | Physical/electronic sensing | Event interpretation |
| AI inference | Compute capability | Model execution |
| Device diagnostics | Hardware telemetry | Health assessment |

This separation allows the same hardware platform to support evolving software and AI functions.

---

 ## 6.29 Hardware Modularity

 The SSP device should be designed as a modular set of functional subsystems.

 A representative decomposition is:

```
SSP Device
│
├── Processing
├── Positioning
├── Motion sensing
├── Local radio
├── Wide-area communication
├── Secure identity
├── Local storage
├── Power management
├── Battery
├── Tamper detection
└── Mechanical enclosure
```

 This modularity supports:

 - component replacement;
- technology evolution;
- prototype development;
- alternative deployment configurations;
- supply-chain resilience;
- maintenance;
- future product versions.

 It also reduces the risk that a single component decision unnecessarily determines the entire SSP architecture.

---

 ## 6.30 Prototype Hardware Strategy

 The first SSP prototype should not attempt to reproduce every aspect of a production wearable.

 The prototype should instead validate the architectural assumptions that have the greatest engineering uncertainty.

 The prototype should demonstrate at least:

 - positioning;
- motion sensing;
- local processing;
- local event generation;
- communication;
- local buffering;
- adaptive operating modes;
- battery monitoring;
- device identity;
- representative security mechanisms;
- interaction with the Edge/Mobile layer.

 The prototype may use development boards and commercial modules where this accelerates experimentation.

 However, prototype hardware choices should be documented separately from final product assumptions.

 This prevents a development-board configuration from being incorrectly interpreted as the final SSP hardware design.

---

 ## 6.31 Prototype-to-Product Evolution

 The expected evolution is:

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

 At each stage, the following should be progressively refined:

 - component selection;
- PCB integration;
- power consumption;
- RF performance;
- enclosure;
- thermal behavior;
- security;
- manufacturability;
- cost;
- environmental performance.

 The architecture should remain stable while implementation details become progressively optimized.

---

 ## 6.32 Preliminary Hardware Bill of Functions

 A preliminary hardware bill of functions is:

 | Subsystem | Function | Priority |
| --- | --- | --- |
| MCU/SoC | Local processing and control | Mandatory |
| GNSS | Outdoor positioning | Mandatory |
| IMU | Motion sensing | Mandatory |
| Local radio | Proximity / Edge interaction | High |
| Wide-area radio | Remote communication | Mandatory for autonomous wide-area deployment |
| Non-volatile storage | Buffering and configuration | Mandatory |
| Secure identity | Device authentication/key protection | Mandatory |
| Power management | Energy control | Mandatory |
| Battery | Autonomous operation | Mandatory |
| Tamper sensing | Device integrity monitoring | High |
| Health monitoring | Device status | High |
| Environmental sensing | Context/health where justified | Medium |
| Additional sensors | Deployment-specific functions | Future/Scenario-dependent |

The table defines functional requirements, not final component selections.

---

 ## 6.33 Preliminary Component Selection Criteria

 The eventual component-selection process shall evaluate candidate components against a common set of criteria.

 ### Processing

 - computational performance;
- low-power modes;
- memory;
- peripheral interfaces;
- security features;
- software ecosystem;
- lifecycle availability.

 ### Positioning

 - positioning accuracy;
- acquisition time;
- sensitivity;
- supported constellations;
- power consumption;
- assistance features.

 ### Motion sensing

 - noise characteristics;
- measurement range;
- sampling capability;
- power consumption;
- physical size.

 ### Communication

 - coverage;
- bandwidth;
- latency;
- power;
- security;
- certification;
- module availability.

 ### Storage

 - capacity;
- endurance;
- retention;
- write performance;
- power consumption.

 ### Security hardware

 - key protection;
- secure identity;
- cryptographic acceleration;
- secure boot integration;
- lifecycle support.

 ### Battery and power

 - energy density;
- peak current;
- safety;
- charging;
- lifecycle;
- physical dimensions.

 The final component selection shall be justified quantitatively wherever practical.

---

 ## 6.34 Hardware Decision Traceability

 The hardware design shall remain traceable to the requirements and architectural decisions.

 An initial example is:

 | Requirement | Hardware implication | Architectural reason | Verification |
| --- | --- | --- | --- |
| Local decision capability | Embedded processor | Reduce cloud dependency | Local-processing test |
| Position monitoring | GNSS subsystem | Core monitoring function | Positioning test |
| Motion awareness | IMU | Contextual interpretation | Motion test |
| Proximity monitoring | Local radio | Relative-presence information | Proximity test |
| Communication resilience | Local storage | Preserve events during outage | Connectivity-failure test |
| Device authentication | Secure identity mechanism | Security by design | Security test |
| Adaptive energy management | Low-power modes | Battery autonomy | Energy test |
| Tamper awareness | Tamper sensing | Device integrity | Tamper test |
| Privacy-aware operation | Local processing/storage | Reduce unnecessary data transmission | Data-flow test |
| Fleet deployment | Remote management capability | Lifecycle scalability | Fleet-management test |

This traceability will be expanded when concrete components are selected.

---

 ## 6.35 Hardware Risks and Engineering Questions

 Several hardware questions remain open and shall be resolved during subsequent engineering stages.

 ### HR-01 — Positioning performance

 What positioning accuracy and availability can realistically be achieved in the intended environments?

 ### HR-02 — Battery autonomy

 What operating profile provides the required autonomy while preserving critical monitoring functions?

 ### HR-03 — Communication energy

 What proportion of the energy budget is consumed by wide-area communication?

 ### HR-04 — Local computation

 How much local processing is required before additional compute capability produces diminishing operational benefits?

 ### HR-05 — Wearable form factor

 Can the required sensors, radios, battery and security mechanisms be integrated within acceptable physical dimensions?

 ### HR-06 — RF performance

 How does human-body proximity and enclosure design affect radio performance?

 ### HR-07 — Tamper resistance

 Which physical tamper mechanisms provide meaningful operational benefit without excessive complexity?

 ### HR-08 — Cost

 Can the required hardware architecture achieve the target cost at the intended deployment scale?

 These questions will feed the quantitative evaluation in later chapters.

---

 ## 6.36 Hardware KPIs

 The hardware design introduces several measurable KPIs.

 ### Processing

 - local processing latency;
- CPU utilization;
- memory utilization;
- local inference latency.

 ### Positioning

 - position error;
- time to first fix;
- positioning availability;
- energy per positioning operation.

 ### Motion sensing

 - sensor sampling rate;
- motion-classification performance;
- sensor availability;
- false event rate.

 ### Communication

 - transmission energy;
- communication success rate;
- connection establishment time;
- recovery time.

 ### Energy

 - average current;
- peak current;
- energy per event;
- energy per operating mode;
- battery autonomy.

 ### Security

 - secure-boot verification;
- unauthorized firmware rejection;
- credential-protection effectiveness;
- tamper-event detection.

 ### Physical

 - mass;
- dimensions;
- environmental tolerance;
- attachment integrity.

 These KPIs connect the hardware design to the validation methodology established in Chapter 3.

---

 ## 6.37 Hardware Design and Chapter 7

 The hardware architecture establishes the physical capabilities required for communication, but it does not yet select the complete communication architecture.

 Chapter 7 will therefore determine the communication technologies and protocols used between:

 **Device ↔ Edge/Mobile**

 **Device ↔ Wide-Area Network**

 **Edge/Mobile ↔ Cloud**

 **Cloud ↔ Authorized User**

 The communication design will use the hardware constraints identified in this chapter, particularly:

 - radio capability;
- energy consumption;
- antenna requirements;
- local processing;
- storage;
- communication fallback;
- security hardware.

 This preserves the intended design progression:

 **Architecture → Hardware → Communication**

 rather than selecting communication technologies independently of the device design.

---

 ## 6.38 Chapter 6 Conclusion

 The SSP device is defined as an autonomous, secure and energy-aware embedded node within the larger Device–Edge/Mobile–Cloud architecture.

 Its hardware must support more than basic location acquisition.

 The device combines:

 **Positioning → Motion sensing → Local processing → Event generation → Communication → Security → Energy management → Device health**

 The principal hardware-design decision is therefore to provide sufficient local capability to support the distributed SSP architecture without unnecessarily increasing device complexity, energy consumption or cost.

 The hardware architecture also preserves the central SSP principle established in the previous chapters:

 > **The device should process locally whenever local processing provides a meaningful benefit in latency, resilience, privacy or energy efficiency, while forwarding the information required by higher layers for broader assessment and operational management.**

 At this stage, the exact semiconductor components, communication modules, battery capacity and mechanical implementation remain engineering-selection tasks rather than fixed architectural assumptions.

 The next chapter therefore defines the **SSP communication architecture**, including communication technologies, protocol selection, data prioritization, communication resilience, security and the relationship between Device, Edge/Mobile and Cloud.

 The design progression is now:

 **Requirements → Market/Context → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Business/Costs → Validation**
