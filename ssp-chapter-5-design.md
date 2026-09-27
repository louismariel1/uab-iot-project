 # 5\. SSP System Architecture and First Engineering Design Decisions

 ## 5.1 Purpose of the Architecture Chapter

 Chapters 1–4 established the motivation, users, operational scenarios, system requirements and technological context for SmartSecurePerimeter (SSP).

 The purpose of this chapter is to convert those requirements into the **first explicit engineering design of SSP**.

 This chapter therefore answers the question:

 > **How should SSP be structured so that the requirements established in Chapter 3 can be satisfied while taking into account the technological opportunities and constraints identified in Chapter 4?**

 The architecture is deliberately defined before selecting individual hardware components, communication modules, software frameworks or machine-learning models.

 The design progression is therefore:

 **Requirements → Architectural principles → System layers → Functional allocation → Interfaces → Data flows → First technology decisions → Detailed subsystem design**

 The architecture established in this chapter becomes the baseline for the subsequent hardware, communication, embedded software, intelligence, energy, cloud and validation chapters.

---

 ## 5.2 Architectural Design Objectives

 The SSP architecture shall satisfy the following principal objectives:

 1. **Distributed processing**\
    Functions shall be allocated between Device, Edge/Mobile and Cloud according to latency, energy, privacy, connectivity and computational requirements.
2. **Adaptive operation**\
    Monitoring intensity, processing and communication shall be capable of changing according to operational context and risk.
3. **Local decision capability**\
    Critical or latency-sensitive functions shall not depend exclusively on continuous cloud availability.
4. **Context-aware event interpretation**\
    Position, motion, proximity, confidence and device state shall be capable of being combined before an operational decision is generated.
5. **Privacy-aware information flow**\
    Information shall be processed and transmitted according to operational necessity rather than automatically forwarding all available raw data.
6. **Secure-by-design operation**\
    Device identity, communication security, access control, software integrity and lifecycle management shall be architectural properties.
7. **Resilience**\
    Temporary loss of connectivity or individual subsystem failures shall result in defined fallback behavior rather than uncontrolled system failure.
8. **Scalability**\
    The same fundamental architecture shall support the progression from PoC to larger deployments.
9. **Measurable engineering**\
    Architectural decisions shall ultimately be evaluated against the KPIs established in Chapter 3.

 These objectives directly translate the design implications identified in Chapter 4 into architectural constraints.

---

 # 5.3 First Architectural Decision — Three-Layer SSP Architecture

 The first major engineering decision is to adopt a **three-layer distributed architecture**:

 **Device → Edge/Mobile → Cloud**

 Each layer has a distinct role.

```
┌──────────────────────────────────────────────┐
│                    CLOUD                     │
│                                              │
│ Historical data • Fleet management           │
│ Analytics • Models • Policies • Dashboards   │
│ Integration • Long-term storage              │
└──────────────────────▲───────────────────────┘
                       │
                 Cloud interface
                       │
┌──────────────────────┴───────────────────────┐
│                 EDGE / MOBILE                 │
│                                              │
│ Sensor fusion • Risk assessment              │
│ Predictive geofencing • Local analytics      │
│ Privacy filtering • Communication management │
│ Local resilience • Event aggregation         │
└──────────────────────▲───────────────────────┘
                       │
                Local interface
                       │
┌──────────────────────┴───────────────────────┐
│                    DEVICE                    │
│                                              │
│ Position • Motion • Proximity • Tamper       │
│ Local processing • Power management           │
│ Secure identity • Event generation           │
└──────────────────────────────────────────────┘
```

 This architecture is selected because no single processing location is optimal for every SSP function.

 The Device provides proximity to the physical phenomenon and therefore offers advantages in latency, local awareness and privacy.

 The Edge/Mobile layer provides additional computational capability without requiring every decision to traverse the cloud.

 The Cloud provides system-wide information, historical analysis, centralized management and scalable processing.

---

 # 5.4 Architectural Principle — Processing Where It Provides the Greatest Benefit

 A central SSP design rule is established:

 > **A function shall be implemented at the lowest practical architectural layer capable of satisfying its requirements.**

 This does not mean that all processing should occur on the device.

 Instead, the allocation shall consider:

 - latency;
- energy consumption;
- computational capability;
- communication availability;
- privacy;
- security;
- scalability;
- required information context.

 The resulting conceptual allocation is:

 | Function | Device | Edge/Mobile | Cloud |
| --- | --- | --- | --- |
| Sensor acquisition | Primary | — | — |
| Basic signal processing | Primary | Optional | — |
| Device-state monitoring | Primary | Secondary | Historical |
| Position acquisition | Primary | — | — |
| Position-confidence estimation | Primary/Edge | Primary | Historical |
| Motion classification | Primary/Edge | Primary | Model development |
| Geofence evaluation | Basic | Primary | Policy/historical |
| Proximity evaluation | Primary | Primary | Historical |
| Event generation | Primary | Secondary | — |
| Risk assessment | Basic | Primary | Advanced/historical |
| Predictive assessment | Limited | Primary | Model training/analysis |
| Privacy filtering | Primary | Primary | Policy |
| Communication prioritization | Primary | Primary | Policy |
| Offline operation | Primary/Edge | Primary | — |
| Historical analysis | — | Limited | Primary |
| Fleet management | — | Limited | Primary |
| Model management | — | — | Primary |
| Operational dashboard | — | Optional | Primary |

This table is an **architectural allocation**, not yet a final implementation specification.

 The detailed implementation of each function will be determined in later chapters.

---

 # 5.5 SSP Device Layer

 The Device layer is the physical interface between SSP and the monitored environment.

 The device shall provide the minimum sensing, processing, communication and security capabilities required to maintain appropriate monitoring without unnecessary energy consumption.

 A conceptual device architecture is:

```
                 ┌──────────────────┐
                 │ Positioning      │
                 │ GNSS / other     │
                 └────────┬─────────┘
                          │
┌──────────────┐          │          ┌───────────────┐
│ Motion       │──────────┼──────────│ Proximity     │
│ Sensors      │          │          │ / BLE         │
└──────────────┘          ▼          └───────────────┘
                  ┌─────────────────┐
                  │ Embedded        │
                  │ Processor       │
                  │                 │
                  │ • Filtering     │
                  │ • State        │
                  │ • Events        │
                  │ • Local logic   │
                  └───────┬─────────┘
                          │
            ┌─────────────┼─────────────┐
            ▼             ▼             ▼
       Communication   Security     Power manager
            │             │             │
            ▼             ▼             ▼
       Edge / WAN     Identity       Battery
```

 The Device therefore becomes more than a sensor node.

 Its principal functions are:

 - sensing;
- initial signal processing;
- positioning;
- motion interpretation;
- proximity detection;
- device-state monitoring;
- tamper detection;
- local event generation;
- communication;
- secure identity;
- power management.

---

 # 5.6 First Device Design Decision — Embedded Local Intelligence

 The Device shall include an embedded processing capability sufficient to perform local monitoring functions.

 The architecture shall **not** require raw sensor information to be continuously transmitted to the Edge or Cloud.

 The device should therefore be capable of performing functions such as:

 - sensor filtering;
- basic sensor fusion;
- movement-state determination;
- position-quality evaluation;
- event pre-processing;
- tamper-state evaluation;
- local threshold evaluation;
- communication prioritization;
- power-state management.

 This decision follows directly from the requirements for energy efficiency, privacy, resilience and local decision capability.

 It also establishes an important architectural boundary:

 > **Raw sensor information is not automatically considered system-wide information.**

 Only information required by the next processing layer should normally cross the interface.

---

 # 5.7 Device Operating States

 Adaptive monitoring requires the device to have defined operating states.

 The initial SSP state model is:

```
                  ┌───────────────┐
                  │    ACTIVE     │
                  │ High monitoring│
                  └───────┬───────┘
                          │
                  Normal conditions
                          │
                          ▼
                  ┌───────────────┐
                  │    NORMAL     │
                  │ Balanced mode │
                  └───────┬───────┘
                          │
                   Low activity /
                   low risk
                          ▼
                  ┌───────────────┐
                  │ LOW POWER     │
                  │ Reduced duty  │
                  └───────────────┘

Elevated risk ───────────► ACTIVE

Critical event ──────────► CRITICAL

Fault / abnormal state ──► FAULT
```

 The precise sensor frequencies, positioning intervals, communication intervals and processor states are deliberately left for the energy and hardware design chapters.

 The architectural decision is that **operating state controls resource usage**.

---

 # 5.8 First Energy-Management Decision

 The architecture shall treat energy management as a system-level function rather than simply a battery-management function.

 The intended relationship is:

 **Operational state → Required monitoring → Processing intensity → Communication intensity → Energy consumption**

 For example:

 | Operating condition | Monitoring strategy | Communication |
| --- | --- | --- |
| Normal / low risk | Reduced or scheduled sensing | Periodic status |
| Elevated condition | Increased sensing | Increased reporting |
| Approaching protected perimeter | High monitoring | Higher priority |
| Critical event | Maximum required monitoring | Immediate priority |
| Connectivity loss | Local monitoring | Buffer/store |
| Low battery | Energy-aware fallback | Policy-dependent |

The exact thresholds and operating profiles will be established later.

 This creates a direct link between the architecture and the energy KPIs defined in Chapter 3.

---

 # 5.9 Edge/Mobile Layer

 The Edge/Mobile layer is introduced as the intermediate intelligence and resilience layer between constrained devices and centralized cloud services.

 It may be implemented using one or more forms of infrastructure depending on the deployment scenario, such as:

 - a smartphone;
- a dedicated gateway;
- an embedded edge computer;
- a local server;
- another authorized edge-capable platform.

 The architecture therefore defines the **function of the layer before fixing its physical implementation**.

 Its principal functions include:

 - device aggregation;
- sensor-data correlation;
- position interpretation;
- predictive geofencing;
- trajectory estimation;
- risk assessment;
- event correlation;
- privacy filtering;
- communication prioritization;
- local storage;
- temporary cloud-independent operation.

---

 # 5.10 First Edge Design Decision — Local Predictive Assessment

 The Edge shall provide the principal location for SSP predictive event assessment.

 This includes functions such as:

 - predicted movement toward a protected zone;
- estimated time to boundary;
- trajectory consistency;
- position-confidence-aware prediction;
- contextual risk assessment;
- multi-device proximity interpretation.

 The reason for assigning these functions to the Edge is that they may require more computational context than is appropriate for a constrained wearable device while still benefiting from lower latency and reduced cloud dependency.

 A conceptual prediction chain is:

```
Position
   +
Motion
   +
Position confidence
   +
Geofence
   +
Historical/context information
        │
        ▼
Trajectory estimation
        │
        ▼
Predicted boundary interaction
        │
        ▼
Risk / severity assessment
        │
        ▼
Adaptive monitoring
```

 This is one of the principal engineering hypotheses of SSP and will require quantitative validation later.

---

 # 5.11 Position Confidence as an Architectural Input

 Chapter 3 established that positioning should not automatically be treated as perfectly accurate.

 Chapter 4 reinforced this requirement because positioning quality can vary with environmental conditions.

 The architecture therefore establishes:

 > **Position confidence shall be treated as an input to event interpretation wherever technically feasible.**

 For example:

```
Position ────────────┐
                     │
Motion ──────────────┤
                     ▼
Position confidence ─► Contextual assessment
                     │
Geofence ────────────┤
                     │
History ─────────────┘
```

 This prevents a low-confidence position estimate from automatically producing the same decision as a high-confidence measurement.

 The precise confidence representation—accuracy radius, covariance, quality score or another metric—will be determined during the positioning design.

---

 # 5.12 Predictive Geofencing

 Traditional geofencing asks:

 > **Is the device currently inside or outside the defined zone?**

 SSP extends this concept to:

 > **Given current position, movement and confidence, is the device likely to interact with the zone in the near future?**

 The architectural model is therefore:

```
Current position
       +
Movement vector/state
       +
Position confidence
       +
Protected geometry
       ↓
Trajectory estimation
       ↓
Predicted interaction
       ↓
Risk assessment
```

 This does not imply that predictive assessment will always use machine learning.

 A deterministic or statistical model may be preferable if it provides adequate performance, lower energy consumption, better explainability or easier validation.

 This is consistent with the Chapter 3 requirement that AI must provide measurable benefit over an appropriate alternative.

---

 # 5.13 Cloud Layer

 The Cloud layer provides system-wide capabilities that benefit from centralized information and scalable computing.

 The initial Cloud responsibilities are:

 - long-term event storage;
- fleet management;
- user and role management;
- policy management;
- operational dashboards;
- historical analytics;
- system-wide reporting;
- model management;
- configuration management;
- integration with authorized external systems;
- large-scale data analysis.

 The Cloud shall therefore complement rather than replace the Device and Edge layers.

 The architectural principle is:

 > **Cloud availability shall not be an unconditional prerequisite for every protection function.**

---

 # 5.14 First Cloud Design Decision — Centralized Management

 SSP shall use the Cloud as the authoritative management layer for the fleet.

 This includes management of:

 - devices;
- users;
- policies;
- configurations;
- software versions;
- models;
- operational history.

 This creates a distinction between:

 **Operational authority → Cloud**

 and

 **Operational continuity → Device/Edge**

 This separation supports both scalability and resilience.

---

 # 5.15 End-to-End SSP Architecture

 The resulting first complete architecture is:

```
                           ┌─────────────────────────┐
                           │          CLOUD          │
                           │                         │
                           │ Fleet management        │
                           │ Historical storage      │
                           │ Analytics               │
                           │ Policies                │
                           │ Model management        │
                           │ Dashboard               │
                           │ External integration    │
                           └────────────┬────────────┘
                                        │
                                  Secure WAN/API
                                        │
                           ┌────────────▼────────────┐
                           │       EDGE / MOBILE     │
                           │                         │
                           │ Device aggregation      │
                           │ Sensor fusion           │
                           │ Predictive geofencing   │
                           │ Risk assessment         │
                           │ Privacy filtering       │
                           │ Local event storage     │
                           │ Communication control   │
                           │ Offline operation       │
                           └────────────┬────────────┘
                                        │
                                Local / short-range
                                        │
             ┌──────────────────────────┼─────────────────────────┐
             │                          │                         │
       ┌─────▼─────┐              ┌─────▼─────┐             ┌─────▼─────┐
       │  Device 1 │              │  Device 2 │             │  Device N │
       │           │              │           │             │           │
       │ Position  │              │ Position  │             │ Position  │
       │ Motion    │              │ Motion    │             │ Motion    │
       │ Proximity│              │ Proximity│             │ Proximity│
       │ Tamper    │              │ Tamper    │             │ Tamper    │
       │ Local AI  │              │ Local AI  │             │ Local AI  │
       │ Power     │              │ Power     │             │ Power     │
       └───────────┘              └───────────┘             └───────────┘
```

 The architecture is intentionally scalable from a single-device PoC to a fleet.

---

 # 5.16 Communication Architecture

 The architecture establishes three principal communication boundaries:

 ### Interface A — Device ↔ Edge/Mobile

 Used for:

 - device association;
- local status;
- events;
- proximity information;
- configuration;
- selected sensor information.

 ### Interface B — Edge/Mobile ↔ Cloud

 Used for:

 - event synchronization;
- device status;
- configuration;
- policy updates;
- historical information;
- model management;
- fleet management.

 ### Interface C — Cloud ↔ Authorized User

 Used for:

 - dashboards;
- alerts;
- reports;
- configuration;
- operational management.

 The actual technologies are intentionally not frozen in this chapter.

 They will be evaluated in Chapter 7 against:

 - range;
- bandwidth;
- latency;
- energy;
- reliability;
- security;
- infrastructure requirements;
- cost;
- deployment environment.

---

 # 5.17 First Communication Decision — Policy-Based Data Flow

 SSP shall not treat all information as having identical communication requirements.

 Information will initially be classified into four conceptual categories:

 | Class | Example | Communication behavior |
| --- | --- | --- |
| Routine | Battery/status | Periodic |
| Contextual | Position/motion summary | Policy-controlled |
| Elevated | Approach/proximity condition | Increased priority |
| Critical | Confirmed protection event | Immediate/high priority |

This directly implements the communication-prioritization requirement from Chapter 3.

 It also provides the basis for later evaluation of the relationship between communication behavior, latency, data volume and energy consumption.

---

 # 5.18 First Privacy Architecture Decision

 Privacy shall influence the location at which information is processed.

 The architecture therefore establishes a **data-minimization boundary**:

```
Raw sensing
     ↓
Local interpretation
     ↓
Relevant information selected
     ↓
Privacy policy applied
     ↓
Only required information transmitted
```

 The design does not assume that all raw sensor information should enter the Cloud.

 Instead:

 > **The minimum information required to satisfy the operational function should cross each architectural boundary.**

 For example, a routine device state may require only a status message rather than a continuous raw sensor stream.

 During an elevated or critical event, additional contextual information may be transmitted where authorized and operationally necessary.

 The exact information classes and retention policies will be developed in the data architecture and privacy/security chapters.

---

 # 5.19 First Security Architecture Decision

 Security shall be implemented across all three layers.

 The initial trust model is:

```
Device identity
      ↓
Authenticated Device ↔ Edge
      ↓
Authenticated Edge ↔ Cloud
      ↓
Authenticated User ↔ Cloud
```

 Each device shall have an identity that can be associated with:

 - authorized device registration;
- configuration;
- cryptographic credentials;
- deployment state;
- software version;
- security state.

 The architecture shall also support:

 - authenticated communication;
- confidentiality;
- integrity;
- access control;
- secure configuration;
- secure updates;
- auditability.

 The specific cryptographic protocols and hardware security mechanisms remain design decisions for later chapters.

---

 # 5.20 Trust Boundaries

 The architecture contains several security trust boundaries.

```
         TRUST BOUNDARY
               │
       ┌───────▼───────┐
       │    Device     │
       └───────┬───────┘
               │
        Device/Edge link
               │
       ┌───────▼───────┐
       │ Edge / Mobile │
       └───────┬───────┘
               │
          WAN / API
               │
       ┌───────▼───────┐
       │     Cloud     │
       └───────┬───────┘
               │
        User/API access
               │
       ┌───────▼───────┐
       │ Authorized    │
       │ Users/System  │
       └───────────────┘
```

 Each boundary shall therefore be treated as potentially untrusted until authentication and authorization have been established.

 This prevents the architecture from implicitly assuming that an internal network is automatically trusted.

---

 # 5.21 Resilience Architecture

 The architecture explicitly incorporates degraded operating modes.

 The principal failure model is:

```
                 Normal
                   │
                   ▼
              Monitoring
                   │
          Connectivity loss
                   │
                   ▼
          Local / Edge mode
                   │
          Events buffered
                   │
        Connectivity restored
                   │
                   ▼
             Synchronize
                   │
                   ▼
                Normal
```

 During temporary Cloud disruption:

 - the Device continues required local functions;
- the Edge continues available local assessment;
- important events are retained;
- synchronization occurs after recovery.

 The precise offline storage duration and recovery requirements will be established through the performance and reliability analysis.

---

 # 5.22 Critical-Event Path

 The architecture distinguishes the critical-event path from the normal information path.

 ### Normal path

```
Sense
 ↓
Local processing
 ↓
Status/event summary
 ↓
Edge
 ↓
Cloud
 ↓
Dashboard
```

 ### Critical path

```
Sense
 ↓
Local detection
 ↓
Priority event
 ↓
Edge confirmation
 ↓
Priority communication
 ↓
Authorized alert
 ↓
Operational response
```

 This distinction is important because the critical path must be evaluated independently for latency.

 It also prevents routine cloud analytics from unnecessarily delaying time-sensitive operational events.

---

 # 5.23 SSP Event Model

 The architecture establishes an event-oriented information model.

 A conceptual event contains:

```
Event
 ├── Device identity
 ├── Timestamp
 ├── Position
 ├── Position confidence
 ├── Motion state
 ├── Proximity information
 ├── Device state
 ├── Communication state
 ├── Event type
 ├── Severity
 ├── Confidence
 └── Processing origin
```

 The exact data schema will be specified in the later software/data architecture.

 The important architectural decision is that SSP shall transmit **structured events and relevant context**, rather than treating the system simply as a continuous raw-sensor pipeline.

---

 # 5.24 Risk and Severity Architecture

 SSP shall distinguish between:

 **Detection**

 and

 **Operational significance**.

 The conceptual process is:

```
Raw observations
       ↓
Event detection
       ↓
Context enrichment
       ↓
Confidence evaluation
       ↓
Risk / severity assessment
       ↓
Operational classification
       ↓
Response
```

 This allows two technically different questions to remain separate:

 1. **Did something happen?**
2. **How significant is it?**

 This distinction is important for avoiding unnecessary alerts and supporting adaptive monitoring.

---

 # 5.25 Adaptive Monitoring Control Loop

 The architecture establishes a closed control loop:

```
        ┌─────────────────────────┐
        │   Operational context   │
        └────────────┬────────────┘
                     ▼
              Risk assessment
                     │
                     ▼
             Monitoring policy
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Sensing   Processing  Communication
          │          │          │
          └──────────┼──────────┘
                     ▼
                 New data
                     │
                     └──────────────► Risk assessment
```

 This is a fundamental SSP architectural feature.

 It means that monitoring is not simply a fixed configuration.

 Instead:

 > **The system observes its environment, assesses the current condition and adjusts its resource usage according to policy.**

 The actual control algorithm remains open for subsequent engineering analysis.

---

 # 5.26 Architecture Decision Summary

 The principal decisions made in this chapter are:

 | ID | Architectural decision | Status |
| --- | --- | --- |
| AD-01 | Device–Edge/Mobile–Cloud architecture | **Selected** |
| AD-02 | Local processing on Device | **Selected** |
| AD-03 | Edge as principal predictive-processing layer | **Selected** |
| AD-04 | Cloud as centralized management and historical-analysis layer | **Selected** |
| AD-05 | Position confidence propagated into decision functions | **Selected** |
| AD-06 | Adaptive monitoring states | **Selected** |
| AD-07 | Policy-based communication prioritization | **Selected** |
| AD-08 | Privacy-aware information flow | **Selected** |
| AD-09 | End-to-end device/layer authentication | **Selected** |
| AD-10 | Local/Edge fallback during connectivity disruption | **Selected** |
| AD-11 | Structured event model | **Selected** |
| AD-12 | Predictive geofencing | **Selected for evaluation** |
| AD-13 | Machine learning for critical functions | **Not yet selected** |
| AD-14 | Specific positioning technology | **Open** |
| AD-15 | Specific cellular technology | **Open** |
| AD-16 | Specific Device processor | **Open** |
| AD-17 | Specific Edge platform | **Open** |
| AD-18 | Specific Cloud platform | **Open** |

This distinction is important.

 Chapter 5 makes the **architectural decisions**, but it does not prematurely decide the detailed implementation technology.

---

 # 5.27 Design Decisions Deferred to Subsequent Chapters

 Several important decisions must remain open until sufficient engineering information is available.

 ### Hardware

 Chapter 6 will determine:

 - processor/MCU;
- GNSS receiver;
- inertial sensors;
- BLE capability;
- additional sensors;
- battery;
- power-management components;
- secure-storage capability;
- physical enclosure.

 ### Communication

 Chapter 7 will determine:

 - Device–Edge communication technology;
- Edge–Cloud connectivity;
- cellular technology;
- communication protocols;
- fallback mechanisms;
- security protocols;
- communication power profile.

 ### Embedded software

 Later chapters will determine:

 - RTOS or firmware architecture;
- sensor drivers;
- event engine;
- state machine;
- power-management implementation;
- device security;
- update mechanism.

 ### Intelligence

 The intelligence design will determine:

 - deterministic algorithms;
- statistical methods;
- predictive models;
- machine-learning models;
- model deployment locations;
- confidence handling;
- model lifecycle management.

 ### Cloud

 The cloud design will determine:

 - storage architecture;
- APIs;
- database technology;
- dashboards;
- fleet management;
- authentication services;
- scalability architecture.

 This staged approach prevents technology selection from becoming arbitrary.

---

 # 5.28 Architecture-to-Requirement Traceability

 The first architectural mapping can now be established.

 | Chapter 3 requirement | Architectural response |
| --- | --- |
| Position acquisition | Device positioning subsystem |
| Position confidence | Device/Edge confidence processing |
| Motion monitoring | Device sensing and local processing |
| Geographical monitoring | Edge geofence engine |
| Proximity monitoring | Device + Edge |
| Tamper detection | Device security/state monitoring |
| Event generation | Device + Edge event engine |
| Risk assessment | Edge intelligence |
| Alert generation | Edge priority path + Cloud notification |
| Adaptive monitoring | Device/Edge control loop |
| Local decision capability | Device + Edge |
| Cloud processing | Cloud analytics/management |
| Communication resilience | Device/Edge fallback |
| Data minimization | Device/Edge privacy filtering |
| Secure communication | Security boundaries between layers |
| Battery autonomy | Adaptive device operating states |
| Scalability | Multi-device Edge + centralized Cloud |
| Fleet management | Cloud management layer |
| Model management | Cloud intelligence layer |

This provides the first formal bridge between Chapter 3 and the engineering architecture.

---

 # 5.29 Architecture KPIs

 The architecture introduces several KPIs that will become particularly important in later validation.

 ### Latency

 - local event-detection latency;
- Edge processing latency;
- critical alert latency;
- synchronization latency.

 ### Energy

 - energy per operating state;
- energy per event;
- communication energy;
- battery autonomy.

 ### Communication

 - transmitted data volume;
- communication availability;
- recovery time;
- critical-event delivery latency.

 ### Intelligence

 - event-detection performance;
- prediction accuracy;
- prediction lead time;
- false-positive rate;
- confidence calibration.

 ### Privacy

 - proportion of processing performed locally;
- reduction in raw-data transmission;
- sensitive-data transmission volume.

 ### Resilience

 - offline operating duration;
- event preservation;
- recovery time;
- synchronization success.

 ### Scalability

 - devices supported;
- events per second;
- cloud response time;
- Edge processing capacity.

 These KPIs provide the basis for quantitative evaluation in the later chapters.

---

 # 5.30 First SSP Design Baseline

 At the completion of this chapter, the first SSP engineering baseline can be defined as:

```
                    SSP SYSTEM
                        │
        ┌───────────────┼────────────────┐
        │               │                │
     DEVICE            EDGE             CLOUD
        │               │                │
   Sense             Interpret        Manage
   Position          Assess           Store
   Motion            Predict          Analyse
   Proximity         Filter           Configure
   Tamper            Aggregate        Learn
   Local logic       Resilience       Integrate
   Power             Prioritize
        │               │
        └───────┬───────┘
                │
         Adaptive control
                │
                ▼
       Monitoring intensity
                │
                ▼
        Energy / communication
```

 The resulting system is therefore not defined simply as a wearable device connected to a cloud service.

 It is defined as a **distributed cyber-physical monitoring system** in which sensing, interpretation, prediction, communication and management are deliberately distributed across multiple processing layers.

---

 # 5.31 Chapter 5 Conclusion

 The first engineering design of SSP establishes a **Device–Edge/Mobile–Cloud architecture** as the foundation for the system.

 The Device provides sensing, positioning, local interpretation, event generation, security and adaptive energy management.

 The Edge/Mobile layer provides contextual processing, predictive geofencing, risk assessment, privacy filtering, event correlation and resilience during communication disruption.

 The Cloud provides centralized management, historical storage, system-wide analytics, model management, operational visualization and integration capabilities.

 The architecture also establishes several important SSP design principles:

 **Process locally when latency, energy, privacy or resilience justify it.**

 **Use the Edge when contextual intelligence requires more resources than the Device can efficiently provide.**

 **Use the Cloud when centralized information, historical analysis or fleet-scale processing provides greater value.**

 **Treat position confidence as part of the information used for decision-making.**

 **Adapt sensing, processing and communication according to operational context.**

 **Transmit information according to operational necessity rather than automatically transmitting all available raw data.**

 **Maintain defined local and Edge functionality during temporary connectivity loss.**

 **Keep critical-event processing separate from routine information flows.**

 The chapter deliberately leaves detailed component and technology selections open. These will now be derived from the architecture rather than selected independently.

 The resulting design progression is:

 **Requirements → System Architecture → Hardware Architecture → Communication Architecture → Embedded Software → Data Architecture → Intelligence/AI → Energy & Performance → Cloud Architecture → PoC → Economic Analysis → Validation**

 ### References

 The architectural decisions in this chapter are derived primarily from the requirements, context analysis and technical references already established in Chapters 1–4. The detailed hardware, communication, software, AI and cloud chapters should introduce additional component- and technology-specific references as those decisions are made.
