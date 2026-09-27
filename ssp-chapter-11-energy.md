You wrote “chapter 10” at the end, but based on the frozen structure and the sequence, I’m treating this as **Chapter 11 — Energy / Performance**.

 ## Chapter 11 plan

 Chapter 11 should convert the qualitative architecture and component decisions from Chapters 5–10 into **quantitative engineering constraints**.

 The central question is:

 > **Can the proposed SSP architecture achieve the required responsiveness and functionality within the energy, computation, memory and battery constraints of the real-world device?**

 The chapter should not yet claim measured performance. At this stage, it establishes the **engineering model, budgets, assumptions and target values** that will later be verified through Chapter 15.

 The planned structure is:

 1. **11.1 Performance requirements**
   - Trace performance targets back to Chapter 3.
   - Separate targets from later measured results.
2. **11.2 Latency budget**
   - Sensor acquisition.
   - Device processing.
   - Device–Edge communication.
   - Edge inference.
   - Edge–Cloud communication where applicable.
   - Cloud processing.
   - User notification.
   - Distinguish local-critical and cloud-assisted paths.
3. **11.3 Sampling requirements**
   - Positioning.
   - IMU.
   - BLE/proximity.
   - Device-state monitoring.
   - Adaptive sampling according to operating state.
4. **11.4 Processing requirements**
   - Device computation.
   - Edge computation.
   - AI inference.
   - Cloud computation.
   - CPU/memory implications.
5. **11.5 Memory requirements**
   - Firmware.
   - Configuration.
   - Sensor buffers.
   - Event queue.
   - Offline event storage.
   - AI model storage.
   - OTA/update space.
6. **11.6 Communication energy**
   - BLE.
   - Wide-area communication.
   - Message frequency.
   - Payload size.
   - Retransmission.
   - Communication-state adaptation.
7. **11.7 Processing energy**
   - MCU/SoC active energy.
   - Edge/mobile energy where relevant.
   - AI inference energy.
   - Energy per event.
8. **11.8 Sensor energy**
   - GNSS.
   - IMU.
   - BLE/proximity.
   - Other selected sensors.
   - Continuous versus duty-cycled operation.
9. **11.9 Sleep / duty-cycle strategy**
   - Normal.
   - Elevated.
   - Critical.
   - Communication-loss modes.
   - Recovery behaviour.
10. **11.10 Battery capacity**
    - Required energy.
    - Usable battery capacity.
    - Conversion/power-management losses.
    - Reserve margin.
11. **11.11 Estimated battery life**
    - Operating-profile calculation.
    - Best/nominal/worst-case scenarios.
    - Sensitivity to communication and GNSS usage.
12. **11.12 Thermal considerations**
    - Device processing.
    - Cellular/radio activity.
    - Charging.
    - Continuous high-load conditions.
13. **11.13 Performance bottlenecks**
    - GNSS acquisition.
    - Radio transmission.
    - AI inference.
    - Cloud dependency.
    - Battery limitations.
14. **11.14 Optimization strategy**
    - Adaptive sensing.
    - Local processing.
    - Data minimization.
    - Communication prioritization.
    - Model optimization.
    - Duty cycling.
15. **11.15 Preliminary performance/energy budget**
    - Consolidated engineering assumptions and TBDs.
16. **11.16 Chapter conclusion**
    - Establish what must be validated in Chapter 15.

---

 # 11\. Energy / Performance

 ## 11.1 Performance Requirements

 Chapter 3 established that SSP must be evaluated quantitatively rather than only demonstrated functionally.

 The performance analysis therefore considers the relationship between:

 **Sensing → Processing → Communication → Decision → Alert**

 and the corresponding resource requirements:

 **Computation → Memory → Communication energy → Sensor energy → Battery consumption**

 The principal performance parameters are:

 - event-detection latency;
- alert-generation latency;
- positioning availability;
- positioning accuracy;
- local inference latency;
- communication latency;
- cloud-processing latency;
- dashboard response time;
- event-ingestion capacity;
- communication recovery time.

 The principal energy parameters are:

 - sensor energy;
- processing energy;
- communication energy;
- energy per event;
- energy per operating mode;
- daily energy consumption;
- battery capacity;
- expected battery autonomy.

 At this stage, values that depend on final component selection, radio configuration, model implementation or measured laboratory behaviour remain **engineering targets or TBD values**, rather than being presented as measured results.

 The fundamental relationship is:

 > **Requirement → Engineering budget → Implementation → Measurement → Acceptance**

 Chapter 11 establishes the engineering budgets. Chapter 15 will establish the corresponding measurements.

---

 ## 11.2 Latency Budget

 SSP does not have a single latency requirement because different operational paths have different urgency.

 A critical local event should not necessarily follow the same processing path as routine telemetry.

 The architecture therefore distinguishes between:

 ### Local/near-local critical path

 **Sensor → Device → Edge/Mobile → Alert**

 and, where required:

 **Sensor → Device → Local decision → Alert**

 ### Cloud-assisted analytical path

 **Sensor → Device → Edge → Cloud → Analysis → User**

 The second path can support functions such as historical analytics and fleet-level analysis without making the Cloud a mandatory dependency for every immediate decision.

 A preliminary latency budget is:

 | Processing stage | Target | Status |
| --- | --- | --- |
| Sensor acquisition | ≤ TBD ms | To be established |
| Device preprocessing | ≤ TBD ms | To be established |
| Device → Edge communication | ≤ TBD ms | To be established |
| Edge inference | ≤ TBD ms | To be established |
| Edge decision logic | ≤ TBD ms | To be established |
| Edge → Cloud communication | ≤ TBD ms | Application dependent |
| Cloud event processing | ≤ TBD ms | Application dependent |
| User notification | ≤ TBD ms | To be established |
| Critical end-to-end alert | ≤ TBD s | Chapter 3 target to be finalized |

The final value shall depend on the operational scenario.

 For example, a local safety/security event may require a substantially shorter response path than a routine historical analytics operation.

 The design principle is therefore:

 > **Critical decisions should use the shortest architecture path capable of satisfying the requirement.**

---

 ## 11.3 Sampling Requirements

 Sampling frequency has a direct effect on both event-detection capability and energy consumption.

 High sampling rates provide more information but increase:

 - sensor energy;
- processor activity;
- memory usage;
- data volume;
- communication requirements.

 SSP therefore uses **adaptive sampling** rather than assuming that every sensor must operate continuously at maximum rate.

 The principal sensing domains are:

 | Signal | Normal operation | Elevated operation | Critical operation |
| --- | --- | --- | --- |
| Position | Periodic | Increased | High-priority/appropriate rate |
| IMU | Low/moderate | Increased | High-rate where justified |
| BLE/proximity | Periodic | Increased | High-priority monitoring |
| Device state | Periodic | Increased | Continuous/near-continuous where required |
| Communication state | Periodic | Increased | Immediate monitoring |

The exact numerical frequencies shall be established after the Chapter 6 hardware and Chapter 7 communication selections have been finalized and characterized.

 The sampling strategy must satisfy:

 **Information requirement ↔ sampling rate ↔ energy cost**

 rather than simply maximizing the sampling frequency.

---

 ## 11.4 Processing Requirements

 Processing is distributed between Device, Edge/Mobile and Cloud according to the architecture established in Chapters 5 and 10.

 ### Device processing

 The Device must support:

 - sensor acquisition;
- signal conditioning;
- timestamping;
- basic sensor fusion;
- event preprocessing;
- communication management;
- power management;
- local rules;
- lightweight AI where justified.

 The Device processor must therefore provide sufficient computational capability without imposing excessive energy consumption.

 ### Edge/Mobile processing

 The Edge/Mobile layer may perform:

 - multi-source sensor fusion;
- trajectory estimation;
- predictive processing;
- anomaly detection;
- contextual event classification;
- local risk assessment;
- communication prioritization.

 ### Cloud processing

 The Cloud performs functions such as:

 - historical analytics;
- model training;
- fleet-level processing;
- long-term event analysis;
- model management;
- centralized reporting.

 This distribution prevents constrained hardware from being required to perform computationally expensive functions unnecessarily.

---

 ## 11.5 Memory Requirements

 Memory requirements arise from several independent functions.

 ### Firmware

 The device must store:

 - operating firmware;
- communication stacks;
- drivers;
- security functions;
- configuration logic.

 ### Configuration

 Memory must support:

 - device identity;
- configuration parameters;
- monitoring policies;
- geofences;
- thresholds;
- communication settings.

 ### Sensor buffering

 Temporary buffers may be required for:

 - inertial measurements;
- positioning information;
- BLE observations;
- sensor-fusion windows;
- AI feature extraction.

 ### Event storage

 During communication disruption, the device or Edge must retain relevant events until they can be securely transmitted.

 ### AI model storage

 If Device AI is implemented, sufficient non-volatile memory must be available for the model and associated inference software.

 ### OTA update capacity

 The device should reserve sufficient memory to support secure firmware updates without unnecessarily increasing the risk of an interrupted update.

 The memory architecture should therefore account for:

 **Runtime memory + persistent configuration + event buffer \+ model storage + update reserve**

 rather than considering firmware size alone.

 The final memory allocation will be determined following the hardware selection in Chapter 6 and software implementation in Chapter 8.

---

 ## 11.6 Communication Energy

 Communication is expected to be one of the major contributors to energy consumption in an autonomous SSP device.

 A simplified communication-energy relationship is:

 > **Ecommunication ≈ Nmessages × Emessage**

 where:

 - **Nmessages** is the number of transmissions;
- **Emessage** represents the energy required for transmission, protocol overhead, reception and associated radio activity.

 In practice, energy also depends on:

 - payload size;
- radio technology;
- signal quality;
- retransmissions;
- connection establishment;
- network conditions;
- transmit power;
- protocol overhead.

 SSP therefore does not assume that transmitting more information continuously is desirable.

 Instead, communication shall be prioritized according to operational importance.

 For example:

 **Routine state → periodic low-volume transmission**

 **Elevated state → increased contextual information**

 **Critical event → immediate high-priority transmission**

 This implements the Chapter 3 principle:

 > **Communication intensity should reflect operational significance.**

---

 ## 11.7 Processing Energy

 Processing energy is influenced by:

 - processor frequency;
- active execution time;
- computational workload;
- memory activity;
- AI inference;
- peripheral activity.

 A simplified model is:

 > **Eprocessing = Pactive × Tactive**

 where:

 - **Pactive** is average processor power while active;
- **Tactive** is accumulated active time.

 The system should therefore minimize unnecessary active periods.

 Potential optimization mechanisms include:

 - event-driven processing;
- low-power sleep states;
- hardware interrupts;
- lightweight feature extraction;
- efficient model architectures;
- local filtering;
- batching of non-critical operations.

 AI processing must be evaluated separately because a more computationally expensive model may provide improved predictive performance while increasing energy consumption.

 The selected model must therefore satisfy both:

 **AI performance**

 and

 **resource efficiency**.

---

 ## 11.8 Sensor Energy

 The principal SSP sensing functions have different energy characteristics.

 ### GNSS

 GNSS can represent a significant energy load, particularly if activated frequently.

 SSP should therefore avoid unnecessary continuous GNSS operation when the operational state does not require it.

 ### IMU

 An IMU can generally support relatively low-power continuous or event-driven monitoring, making it useful for determining whether the device is stationary or moving.

 This can allow other higher-energy functions to be activated selectively.

 For example:

 **Stationary → reduced positioning activity**

 **Movement detected → increased positioning activity**

 ### BLE/proximity

 BLE can support periodic proximity measurements while maintaining relatively low energy consumption, depending on configuration and operating mode.

 The system can adjust scanning and advertising behaviour according to operational requirements.

 The overall relationship is therefore:

 > **Low-energy sensors can help determine when higher-energy sensors should become active.**

 This is an important component of the SSP adaptive-energy strategy.

---

 ## 11.9 Sleep and Duty-Cycle Strategy

 The SSP device shall support multiple operating states.

 A preliminary operating-state model is:

 ### State 0 — Low-power / Normal

 Characteristics:

 - reduced sensing;
- periodic position acquisition;
- low-rate communication;
- event-driven processing;
- extended sleep periods.

 ### State 1 — Elevated monitoring

 Characteristics:

 - increased position acquisition;
- increased proximity monitoring;
- more frequent motion processing;
- increased communication;
- more frequent contextual assessment.

 ### State 2 — Critical monitoring

 Characteristics:

 - high-priority sensing;
- rapid event processing;
- immediate communication of relevant events;
- reduced tolerance for delayed processing;
- continuous or near-continuous monitoring of required functions.

 ### State 3 — Communication-loss mode

 Characteristics:

 - local monitoring continues;
- important events are stored;
- communication recovery is periodically attempted;
- energy is managed according to the duration and severity of the outage.

 The state transitions can be represented as:

 **Normal → Elevated → Critical**

 and, when the condition clears:

 **Critical → Elevated → Normal**

 The exact transition criteria will be defined by the software and operational policy.

 This state-based architecture is preferable to a single fixed operating mode because it allows SSP to trade resource consumption against operational requirements.

---

 ## 11.10 Battery Capacity

 The battery must be selected according to the complete operating profile rather than according to peak current alone.

 A simplified daily energy model is:

 > **Eday = Esensing + Eprocessing \+ Ecommunication + Eidle \+ Eoverhead**

 The required battery capacity is then approximately:

 > **Crequired ≥ Eday × Tautonomy / η**

 where:

 - **Tautonomy** is the required operating duration;
- **η** represents the usable system efficiency, including conversion and other losses.

 A reserve margin should also be included.

 The design therefore distinguishes between:

 **Nominal energy requirement**

 and

 **Required battery capacity**

 because not all nominal battery energy should be assumed to be available to the electronic system.

 The final battery specification will be derived after the component-level power characteristics have been established.

---

 ## 11.11 Estimated Battery Life

 Battery autonomy will be evaluated under representative operating profiles rather than using a single idealized value.

 At minimum, SSP should consider:

 ### Profile A — Normal operation

 Low movement and relatively infrequent critical events.

 Expected characteristics:

 - low-to-moderate sensor activity;
- low communication volume;
- significant sleep time.

 ### Profile B — Active movement

 The monitored device is moving for a significant proportion of the operating period.

 Expected characteristics:

 - increased GNSS activity;
- increased IMU processing;
- increased communication;
- increased contextual processing.

 ### Profile C — Elevated/critical operation

 The system spends significant time in elevated or critical monitoring states.

 Expected characteristics:

 - high sensing activity;
- increased processing;
- increased communication;
- reduced sleep time.

 ### Profile D — Poor communication conditions

 The device experiences degraded connectivity.

 Expected characteristics:

 - communication retries;
- event buffering;
- increased recovery attempts;
- potentially increased energy consumption.

 The autonomy calculation should therefore report a range rather than implying that one battery-life number represents every operating condition.

 The final result should take the form:

 | Operating profile | Estimated daily energy | Estimated autonomy | Status |
| --- | --- | --- | --- |
| Normal | TBD Wh/day | TBD days | Engineering estimate |
| Active movement | TBD Wh/day | TBD days | Engineering estimate |
| Elevated | TBD Wh/day | TBD days | Engineering estimate |
| Critical-heavy | TBD Wh/day | TBD days | Engineering estimate |
| Poor connectivity | TBD Wh/day | TBD days | Engineering estimate |

These values will be populated once the component, radio and software operating assumptions have been quantified.

---

 ## 11.12 Thermal Considerations

 Although the SSP wearable/device is primarily energy constrained, thermal behaviour must also be considered.

 Potential sources of heat include:

 - processor activity;
- cellular transmission;
- high-rate radio operation;
- battery charging;
- intensive AI inference;
- simultaneous operation of multiple subsystems.

 Continuous high-load operation may increase device temperature and potentially reduce:

 - user comfort;
- battery lifetime;
- component reliability;
- processor performance.

 Thermal analysis is therefore particularly relevant to:

 - critical monitoring;
- frequent cellular communication;
- intensive local AI;
- charging while operating.

 The design should avoid requiring continuous maximum processing or radio activity when the operational scenario does not justify it.

---

 ## 11.13 Performance Bottlenecks

 The preliminary architecture identifies several potential bottlenecks.

 ### 11.13.1 Position acquisition

 GNSS acquisition and positioning availability can affect both latency and energy.

 ### 11.13.2 Wide-area communication

 Network availability, signal quality and retransmission can affect:

 - latency;
- energy;
- reliability.

 ### 11.13.3 AI inference

 Complex models may increase:

 - latency;
- memory requirements;
- processor utilization;
- energy consumption.

 ### 11.13.4 Cloud dependency

 Cloud processing introduces additional communication latency and creates a dependency on connectivity.

 For this reason, critical functions should not depend exclusively on cloud processing.

 ### 11.13.5 Battery capacity

 Increasing sensing, communication or AI performance generally increases energy consumption.

 This produces a fundamental engineering trade-off:

 > **Higher monitoring intensity → higher information quality → higher resource consumption**

 SSP therefore requires adaptive resource management.

---

 ## 11.14 Optimization Strategy

 The energy/performance architecture adopts several optimization mechanisms.

 ### 1\. Adaptive sensing

 Sensor activity changes according to operating state.

 ### 2\. Local preprocessing

 Unnecessary raw data is filtered close to the source.

 ### 3\. Adaptive positioning

 Position acquisition frequency changes according to movement and operational context.

 ### 4\. Communication prioritization

 Only information necessary for the receiving layer is transmitted.

 ### 5\. Local/Edge intelligence

 Processing is moved closer to the source when this reduces latency, communication or cloud dependency.

 ### 6. Lightweight AI

 Models should be selected according to the required performance rather than maximizing model complexity.

 ### 7\. Duty cycling

 Sensors, processors and radios enter low-power states when possible.

 ### 8\. Event-driven operation

 The system should respond to meaningful changes rather than continuously processing unchanged conditions at maximum intensity.

 ### 9\. Data minimization

 Reducing unnecessary transmitted data simultaneously supports:

 - privacy;
- communication efficiency;
- energy efficiency;
- cloud cost reduction.

 The resulting optimization relationship is:

 **Operational context → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

---

 ## 11.15 Preliminary Performance and Energy Budget

 The principal engineering budgets established at this stage are summarized below.

 | Category | Parameter | Initial target |
| --- | --- | --- |
| Latency | Critical alert | ≤ TBD |
| Latency | Device processing | ≤ TBD |
| Latency | Edge inference | ≤ TBD |
| Positioning | Accuracy | ≤ TBD error |
| Sampling | Position acquisition | TBD according to operating state |
| Sampling | IMU | TBD according to operating state |
| Processing | Device CPU load | ≤ TBD |
| Memory | Runtime requirement | ≤ TBD |
| Memory | Firmware/model/storage | ≤ TBD |
| Communication | Routine data rate | ≤ TBD |
| Communication | Critical-event transmission | ≤ TBD |
| Energy | Normal daily consumption | ≤ TBD Wh/day |
| Energy | Critical-event energy | ≤ TBD Wh/event |
| Battery | Required autonomy | ≥ TBD |
| Availability | System availability | ≥ TBD |
| Recovery | Communication recovery | ≤ TBD |

The values deliberately remain provisional where they depend on decisions still to be finalized or measured.

 The final engineering process is:

 **Architecture assumptions → Component specifications → Power model → Prototype measurements → Updated model → Validation**

 The resulting values will therefore become progressively more precise rather than being invented prematurely.

---

 ## 11.16 Relationship Between Energy and Performance

 Energy and performance cannot be optimized independently.

 Increasing the frequency of positioning can improve location awareness but increases energy consumption.

 Increasing sensor sampling can improve event-detection performance but increases processing and potentially communication requirements.

 Using a more sophisticated AI model may improve prediction performance but increase computation and memory consumption.

 Increasing communication frequency may reduce the delay before information reaches the Cloud but increase radio energy consumption.

 SSP therefore adopts a multi-objective engineering approach:

 > **Performance must be sufficient for the operational requirement, while energy consumption must remain compatible with the required autonomy.**

 The design objective is not:

 > **Maximum sensing + maximum processing + maximum communication**

 but:

 > **Minimum resource consumption consistent with required operational performance.**

 This is one of the principal architectural consequences of designing SSP as an autonomous IoT device rather than as a continuously powered infrastructure node.

---

 ## 11.17 Relationship to Previous Chapters

 Chapter 11 consolidates decisions made throughout the preceding design stages.

 | Chapter | Contribution to Chapter 11 |
| --- | --- |
| Chapter 3 — Requirements | Performance, autonomy, latency, reliability and energy requirements |
| Chapter 4 — Market/Context | Need for adaptive monitoring, resilience and resource-aware operation |
| Chapter 5 — Architecture | Device/Edge/Cloud processing distribution |
| Chapter 6 — Hardware | Sensor, processor, memory and battery constraints |
| Chapter 7 — Communication | Radio characteristics, communication energy and latency |
| Chapter 8 — Software | Processing workload and operating-state management |
| Chapter 9 — Data Flow | Sampling, data volume, buffering and transmission requirements |
| Chapter 10 — AI | Inference workload, model size, latency and AI energy |

Chapter 11 therefore acts as the quantitative bridge between the architecture and the eventual validation process.

---

 ## 11.18 Inputs to Chapter 12

 The performance analysis also establishes several requirements for the Cloud architecture.

 The Cloud must support:

 - the expected event-ingestion rate;
- storage growth;
- concurrent device connections;
- historical analytics;
- model training;
- model management;
- dashboard response requirements;
- communication recovery;
- scalable processing.

 However, Cloud performance shall not be used to compensate for an inappropriate Device or Edge architecture.

 The complete system must instead maintain the principle:

 **Device efficiency + Edge responsiveness + Cloud scalability**

---

 ## 11.19 Chapter 11 Conclusion

 Chapter 11 establishes the preliminary quantitative engineering framework for SSP.

 The key conclusion is that **energy and performance are coupled system-level design variables**.

 The architecture must simultaneously satisfy:

 **Latency**

 **Sensing quality**

 **Processing capability**

 **Communication reliability**

 **AI performance**

 **Memory constraints**

 **Battery autonomy**

 **Thermal limits**

 The resulting SSP strategy is therefore based on adaptive operation:

 > **Normal conditions → low resource consumption**

 > **Elevated conditions → increased monitoring**

 > **Critical conditions → maximum necessary response**

 while maintaining local fallback capability during communication disruption.

 The principal engineering relationship is:

 **Operational requirement → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

 The numerical values established in this chapter will be progressively refined using the actual component specifications, software workloads, communication characteristics and AI model requirements.

 Most importantly, Chapter 11 does **not** present unmeasured performance as achieved performance. It establishes the budgets and targets that Chapter 15 will ultimately test.

 The next chapter, **Chapter 12 — Cloud Architecture**, will translate the Device–Edge–Cloud data and processing requirements into the concrete backend architecture, including APIs, event processing, databases, storage, authentication, authorization, monitoring, recovery and scalability.
