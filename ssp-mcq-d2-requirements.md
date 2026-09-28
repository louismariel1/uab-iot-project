 # D2 Requirements — Answer-Included Study & Assessment

 **Project:** Smart Safety & Protection IoT System\
 **Acronym:** SSP\
 **Deliverable:** D2 — Functional & Performance Specifications\
 **Purpose:** Study, understand and assess the D2 submission requirements\
 **Academic Year:** 2026/2027

---

 ## 1\. What D2 is actually asking us to do

 The central question behind D2 is:

 > **What must the final SSP system do, and how well must it do it?**

 The hypothetical institutional client has contracted the SSP team to design a complete IoT solution.

 Therefore, D2 is a **requirements document**, not an implementation report.

 We are defining the requirements that the final SSP solution is expected to satisfy.

 The distinction is:

 | D2 | Later deliveries |
| --- | --- |
| What the system shall do | How we implement it |
| Required performance | Components selected |
| Required data | Architecture implementation |
| Required communication characteristics | Actual communication technology |
| Required battery autonomy | Actual battery/component calculations |
| Required dimensions | Actual enclosure |
| Required cloud capacity | Actual cloud implementation |
| Required UI behavior | Actual UI implementation |
| Required AI performance | Actual AI model |

### Key principle

 **D2 defines the destination. D3–D6 explain and demonstrate how we get there.**

---

 # 2\. Official Question 1 — Are all possible functions at device, edge, cloud and UI well defined?

 ## What is being asked?

 The instructor wants to see that we understand the **complete IoT value chain**.

 It is not sufficient to say:

 > “The device collects sensor data and sends it to the cloud.”

 We need to explain what each major layer actually does.

 The four principal functional layers are:

 **Device → Edge → Cloud → UI**

 Communication connects these layers.

---

 ## 2.1 Device functions

 ### Requirement

 The SSP device shall perform functions necessary for local sensing, local processing, monitoring and autonomous operation.

 ### SSP answer

 The device functions include:

 - motion sensing;
- positioning;
- proximity detection;
- device-health monitoring;
- sensor-data preprocessing;
- local event detection;
- temporary data storage;
- local status generation;
- energy management;
- reception of authorized configuration;
- device identification;
- secure firmware lifecycle support.

 ### Why is this important?

 The device should not be treated simply as a collection of sensors.

 It is an **intelligent IoT node**.

 For example:

 **Sensor → local processing → event decision → communication**

 rather than:

 **Sensor → raw data → cloud**

---

 # 3\. Edge functions

 ## Requirement

 The edge layer shall provide local processing between the device and cloud.

 ### SSP answer

 The edge shall:

 - receive device data;
- validate messages;
- timestamp and order information;
- aggregate measurements;
- filter data;
- extract features;
- evaluate event rules;
- perform selected low-latency inference;
- buffer data during cloud outages;
- detect duplicate messages;
- forward information to the cloud;
- continue limited operation when cloud connectivity is unavailable;
- forward authorized configuration to devices.

 ### Important concept

 The edge exists because the cloud should **not necessarily be required for every decision**.

 For example:

 > Device detects abnormal movement → edge evaluates event → edge can react even if cloud connectivity is temporarily unavailable.

 This provides:

 - lower latency;
- resilience;
- reduced bandwidth;
- potentially lower energy consumption.

---

 # 4\. Cloud functions

 ## Requirement

 The cloud must provide centralized storage, processing, management and access.

 ### SSP answer

 The cloud shall:

 - register devices;
- authenticate devices and users;
- receive telemetry;
- receive events;
- validate information;
- store historical information;
- maintain device state;
- process events;
- perform cloud analytics;
- support AI development/monitoring where applicable;
- manage users and permissions;
- maintain audit records;
- provide APIs;
- manage the device fleet;
- apply data-retention policies;
- generate authorized notifications.

 ### Important distinction

 The cloud is **not just a database**.

 It provides:

 **Ingestion + storage + analytics \+ security + management \+ APIs + notifications**

---

 # 5\. UI functions

 ## Requirement

 The UI must provide useful information to authorized users.

 ### SSP answer

 The UI shall provide:

 - current device status;
- current/most recent position;
- event notifications;
- event history;
- map visualization;
- battery status;
- communication status;
- historical sensor/event information;
- device management;
- user management;
- authorized configuration;
- audit information for authorized administrators.

 The UI must respect the user's authorization level.

---

 # 6\. Assessment — Question 1

 ### Does the D2 answer this requirement?

 **Yes.**

 The revised D2 explicitly defines functions for:

 **Device → Edge → Communication → Cloud → UI**

 and separates those functions into individual requirements such as:

 - F-D01–F-D12;
- F-E01–F-E12;
- F-C01–F-C09;
- F-CL01–F-CL15;
- F-U01–F-U11.

 ### What would constitute a weak answer?

 > “The sensors collect data and the cloud displays it.”

 That does not adequately define the complete system.

---

 # 7\. Official Question 2 — Is the data well described?

 This is one of the most important D2 requirements.

 The instructor is asking:

 > **What data exists at every stage of the IoT system, what does it look like, and how much data is being exchanged?**

 We therefore need to follow the data through the complete chain.

---

 # 8\. Sensor/device data

 The device may generate:

 | Data | Type | Unit | Example size |
| --- | --- | --- | --- |
| Device ID | UUID | — | 16 B |
| Timestamp | Integer | ms | 8 B |
| Latitude | Float | degrees | 4 B |
| Longitude | Float | degrees | 4 B |
| Position confidence | Float | m | 4 B |
| Accelerometer X/Y/Z | Integer/Float | g | 6–12 B |
| Gyroscope X/Y/Z | Integer/Float | °/s | 6–12 B |
| Proximity state | Integer | state | 1 B |
| Battery | Integer | % | 1 B |
| Device state | Integer | state | 1 B |
| Communication state | Integer | state | 1 B |
| Event flag | Integer | state | 1 B |
| Sequence number | Integer | — | 4 B |

This answers:

 > **What information does the device produce?**

---

 # 9\. Data format

 D2 specifies:

 - compact binary representation where bandwidth/energy efficiency is important;
- structured formats such as JSON at higher system layers.

 This is important because **data format is itself a requirement**.

 We should not prematurely say:

 > “We will definitely use protocol X.”

 unless the technology has already been selected.

 D2 defines the requirement.

 D3/D4 select the implementation.

---

 # 10\. Data frequency

 The D2 specification establishes target data rates.

 For example:

 - normal inertial sensing: up to 50 Hz;
- event/high-activity sensing: up to 100 Hz;
- positioning: approximately 0.1–1 Hz;
- device status: approximately once/minute;
- routine telemetry: approximately every 10–60 seconds;
- event packets: immediately when possible.

 This answers:

 > **How often is the data generated?**

---

 # 11\. Packet volume

 The D2 specification establishes:

 - nominal telemetry payload ≤128 bytes;
- event payload ≤512 bytes;
- nominal application throughput ≤10 kbit/s/device;
- event burst capability ≥50 kbit/s/device.

 This answers:

 > **How much data is transmitted?**

---

 # 12\. Edge data

 The edge transforms device information into structured records containing at least:

 - device ID;
- timestamp;
- received timestamp;
- sensor/feature values;
- position;
- position confidence;
- communication state;
- battery state;
- event state;
- processing status;
- sequence number.

 Target record size:

 > **normally ≤1 kB**

---

 # 13\. Cloud data

 The cloud maintains at least:

 1. telemetry;
2. event data;
3. device-management data;
4. user/audit data.

 Telemetry records contain:

 - device ID;
- timestamp;
- data type;
- measurement;
- unit;
- quality/confidence;
- source;
- sequence number.

 Event records additionally contain:

 - event ID;
- event type;
- severity;
- confidence;
- triggering inputs;
- event timestamp;
- processing status;
- acknowledgement status.

---

 # 14\. UI data

 The UI should normally receive:

 - current status;
- current position;
- recent events;
- historical summaries;
- device health;
- alerts.

 It should **not continuously request raw sensor streams** unless a diagnostic function requires them.

 Target normal UI/API payload:

 > **≤100 kB/request**

 with pagination for larger datasets.

---

 # 15\. Assessment — Question 2

 ### Does the D2 answer this requirement?

 **Yes, substantially.**

 The revised D2 specifies:

 **what → type → unit → approximate size → frequency → packet size → throughput → destination**

 across:

 **Sensor/device → Edge → Cloud → UI**

 This is much stronger than simply listing the sensors.

---

 # 16\. Official Question 3 — Are functional and performance specifications separated?

 This is a fundamental D2 concept.

 ## Functional specification

 Answers:

 > **What shall the system do?**

 Example:

 > The device shall determine its position.

 ## Performance specification

 Answers:

 > **How well shall it do it?**

 Example:

 > The system shall provide a valid position update at an interval between 1 and 60 seconds depending on monitoring mode.

---

 # 17\. SSP example

 ### Functional

 **F-D02 — Determine position**

 > The device shall acquire positioning information when positioning is available.

 ### Performance

 > Position updates shall be provided at a target interval between 1 and 60 seconds depending on monitoring mode.

 Therefore:

 **Function = position determination**

 **Performance = update frequency**

---

 # 18\. Another example

 ### Functional

 > The system shall detect and report relevant events.

 ### Performance

 > An event requiring immediate communication shall be made available to the edge within ≤2 seconds under nominal connectivity.

 Again:

 **Function = event detection/reporting**

 **Performance = latency**

---

 # 19\. Assessment — Question 3

 ### Does the D2 answer this requirement?

 **Yes.**

 The revised D2 deliberately separates:

 - functional requirements;
- computational performance;
- communication performance;
- energy;
- mechanical;
- cloud;
- UI;
- AI;
- economic requirements.

 This is one of the strongest structural aspects of the revised document.

---

 # 20\. Official Question 4 — Computational performance

 The instructor specifically mentions:

 - maximum latency;
- maximum throughput;
- duty cycle;
- device → edge.

 The D2 therefore needs measurable computational requirements.

---

 ## Device computational requirements

 Current D2 targets:

 | Parameter | Requirement |
| --- | --- |
| Sensor acquisition latency | ≤20 ms |
| Local preprocessing latency | ≤100 ms |
| Local event-rule evaluation | ≤200 ms |
| Average local processing duty cycle | ≤20% |
| Event decision generation | ≤500 ms |
| Local buffer write latency | ≤100 ms |

---

 ## Device-to-edge

 | Parameter | Target |
| --- | --- |
| Application latency | ≤2 s |
| Typical telemetry interval | 10–60 s |
| Nominal throughput | ≤10 kbit/s/device |
| Event burst | ≥50 kbit/s |
| Offline buffer | ≥24 h |

These are **requirements**, not measured results.

---

 # 21\. Official Question 5 — Communications

 The instructor specifically wants:

 - wired/wireless;
- maximum range.

 The D2 defines the device-to-edge connection as:

 > **Wireless, short-range, low-power and bidirectional.**

 Target characteristics:

 | Parameter | Target |
| --- | --- |
| Nominal range | ≥10 m |
| Minimum practical range | ≥5 m |
| Application throughput | ≥100 kbit/s |
| Typical latency | ≤500 ms |
| Event latency | ≤2 s |
| Communication | Bidirectional |

The exact technology remains open for D3/D4.

 This is intentional.

 D2 says **what the communication system must achieve**, rather than prematurely deciding how.

---

 # 22\. Edge-to-cloud communication

 Target:

 - wireless wide-area communication;
- ≥50 kbit/s/device application throughput;
- event latency ≤5 s;
- availability ≥99% when network coverage exists;
- offline operation;
- synchronization after recovery.

---

 # 23\. Official Question 6 — Energy

 The instructor asks:

 > What is the maximum energy consumption and minimum battery duration?

 The D2 defines:

 | Mode | Target |
| --- | --- |
| Deep sleep | ≤1 mW |
| Normal monitoring | ≤50 mW |
| Active sensing | ≤150 mW |
| Communication peak | ≤500 mW |
| Positioning peak | ≤300 mW |

Battery requirement:

 > **Minimum autonomy ≥7 days**

 Design objective:

 > **≥14 days nominal**

 This is important because the SSP device is intended to be wearable/portable.

---

 # 24\. Energy duty cycle

 D2 also defines:

 | State | Target |
| --- | --- |
| Sleep/low power | 80–90% |
| Normal sensing | 8–15% |
| Positioning | 1–5% |
| Communication | \<2% |
| High-intensity event | Event dependent |

The final values will need to be recalculated after component selection.

 This demonstrates that the battery requirement is not arbitrary: it must eventually be supported by an engineering energy calculation.

---

 # 25\. Official Question 7 — Mechanical requirements

 The instructor specifically asks about:

 - maximum size;
- maximum weight;
- supports;
- etc.

 D2 specifies:

 | Parameter | Requirement |
| --- | --- |
| Maximum volume | ≤100 cm³ |
| Maximum mass | ≤100 g |
| Enclosure | Wearable/protective |
| Operating temperature | −10 to +50 °C |
| Storage temperature | −20 to +60 °C |
| Ingress protection | Target IP65+ |
| Drop resistance | ≥1 m target |

This gives D4 concrete constraints for component and enclosure selection.

---

 # 26\. Official Question 8 — Cloud

 The cloud requirements must answer more than:

 > “We will use the cloud.”

 D2 therefore defines:

 ### Capacity

 - initial fleet: 100 devices;
- scalable target: ≥10,000 devices.

 ### Ingestion

 - ≥100 messages/s initial telemetry capacity;
- ≥20 events/s burst.

 ### Performance

 - API p95 ≤1 s;
- event processing p95 ≤2 s.

 ### Availability

 > ≥99.5%

 ### Storage

 > ≥500 GB initial usable application storage.

 ### Retention

 > ≥12 months historical data.

 ### Other requirements

 - backup;
- audit logging;
- device management;
- user management;
- APIs;
- analytics;
- data retention/deletion.

---

 # 27\. Cloud storage calculation

 The D2 document includes an engineering justification.

 Assume:

 - 200 bytes/record;
- one record every 30 seconds.

 Then:

 $$
200 \times \frac{86400}{30}
=
576,000 \text{ bytes/day/device}
$$

 Approximately:

 > **0.576 MB/device/day**

 For 1,000 devices:

 > **576 MB/day**

 For one year:

 > , D2 needs to demonstrateapproximately **210 GB/year**

 before:

 - indexes;
- replication;
- metadata;
- backups.

 Therefore the initial target:

 > **≥500 GB usable application storage**

 provides design margin.

 This is exactly the kind of reasoning expected in a performance specification.

---

 # 28\. Official Question 9 — UI

 The UI must have both **functions and performance requirements**.

 ### Functions

 The UI shall display:

 - device status;
- location;
- events;
- history;
- battery;
- communications;
- maps;
- authorized management functions.

 ### Performance

 | Function | Target |
| --- | --- |
| Login | ≤2 s |
| Dashboard | ≤3 s |
| Status refresh | ≤5 s |
| Event display | ≤5 s |
| Historical query p95 | ≤2 s |
| Map display | ≤3 s |
| Normal API payload | ≤100 kB |

This is another good example of the functional/performance separation.

---

 # 29\. Official Question 10 — Economic requirement

 The instructor asks:

 > What is the maximum global cost?

 The current D2 contains preliminary economic constraints.

 ### Device

 Initial low-volume target:

 > **≤€150/device**

 Larger-scale production objective:

 > **≤€100/device**

 ### Recurring cost

 Target:

 > **≤€10/device/month**

 ### Global deployment

 For 100 devices, the later economic analysis must consider:

 - device hardware;
- edge infrastructure;
- communications;
- cloud;
- software;
- maintenance;
- replacement;
- development;
- personnel;
- certification.

 The final lifecycle/business analysis belongs to D6.

---

 # 30\. Official Question 11 — Is SSP consistent with the market study?

 This needs special attention because **D1 is not being submitted**.

 The instructor assumes that the market study has already been performed.

 Therefore, D2 does not need to reproduce D1.

 Instead, D2 needs to demonstrate that the requirements were **derived consistently with the market/competitive context**.

 The revised D2 identifies the intended differentiation areas:

 - multi-source sensing;
- adaptive monitoring;
- device/edge/cloud processing;
- communication resilience;
- energy management;
- contextual event processing;
- controlled access;
- fleet management;
- optional AI assistance.

 The document also explicitly avoids claiming:

 > “SSP is already commercially superior.”

 Instead it says that final competitiveness requires comparison against actual products using:

 - specifications;
- price;
- reliability;
- battery life;
- deployment cost.

 That is appropriate because D2 establishes requirements; it does not yet prove commercial superiority.

---

 # 31\. The most important D2 distinction

 You should be able to answer this question in an oral presentation:

 ### “What is the difference between a functional and a performance specification?”

 Your answer should be:

 > **A functional specification defines what the system shall do, while a performance specification defines the measurable level at which that function shall operate.**

 For example:

 > **Functional:** SSP shall detect relevant events.

 > **Performance:** A high-priority event shall reach the UI within a target maximum of 5 seconds under nominal connectivity.

---

 # 32\. Another important distinction: requirement vs implementation

 You should also be able to answer:

 ### “Why don't we specify the exact communication protocol in D2?”

 Because D2 defines **requirements before implementation choices**.

 For example:

 ### D2

 > Device-to-edge communication shall be wireless, low-power, bidirectional and provide ≥10 m nominal range.

 ### D3/D4

 > We selected a specific wireless technology because it satisfies the D2 requirements while meeting the energy, range, throughput and cost constraints.

 This prevents the project from becoming:

 > “We bought a development board, therefore these are our requirements.”

 Instead, it becomes:

 > “The client requires these capabilities; we selected hardware capable of satisfying them.”

---

 # 33\. Requirement hierarchy

 A useful way to understand the entire D2 is:

 ### Level 1 — Function

 **What must SSP do?**

 ↓

 ### Level 2 — Data

 **What information does SSP need to perform those functions?**

 ↓

 ### Level 3 — Performance

 **How quickly/how much/how far/how long?**

 ↓

 ### Level 4 — Constraints

 **What physical, energy, economic, security and environmental limits apply?**

 ↓

 ### Level 5 — Verification

 **How will we prove that the final design satisfies the requirements?**

 That is the logic behind the revised D2.

---

 # 34\. D2 master checklist

 Use this checklist before submitting.

 ### System functions

 - [x] Device functions defined
- [x] Edge functions defined
- [x] Communication functions defined
- [x] Cloud functions defined
- [x] UI functions defined
- [x] Security functions defined
- [x] Privacy requirements defined

 ### Data

 - [x] Sensor data defined
- [x] Data types defined
- [x] Units defined
- [x] Data sizes defined
- [x] Sampling/update rates defined
- [x] Device packet size defined
- [x] Event packet size defined
- [x] Device-to-edge throughput defined
- [x] Edge records defined
- [x] Cloud records defined
- [x] UI data defined

 ### Computational performance

 - [x] Sensor latency
- [x] Processing latency
- [x] Event-processing latency
- [x] Device-to-edge latency
- [x] Throughput
- [x] Duty cycle
- [x] Offline buffering

 ### Communications

 - [x] Wireless/wired characteristics
- [x] Device-to-edge range
- [x] Throughput
- [x] Latency
- [x] Bidirectional communication
- [x] Reliability
- [x] Offline operation
- [x] Synchronization

 ### Energy

 - [x] Sleep power
- [x] Normal power
- [x] Active power
- [x] Communication peak
- [x] Positioning peak
- [x] Duty cycle
- [x] Minimum battery duration
- [x] Target battery duration

 ### Mechanical/environmental

 - [x] Maximum mass
- [x] Maximum volume
- [x] Operating temperature
- [x] Storage temperature
- [x] Ingress protection
- [x] Drop resistance
- [x] Wearability

 ### Cloud

 - [x] Fleet size
- [x] Scalability
- [x] Ingestion
- [x] Event processing
- [x] API latency
- [x] Availability
- [x] Storage
- [x] Retention
- [x] Backup
- [x] Audit

 ### UI

 - [x] Functional requirements
- [x] Performance requirements
- [x] Mobile/desktop usability
- [x] Access control

 ### Economics

 - [x] Device cost
- [x] Scaled device target
- [x] Recurring cost
- [x] Global deployment cost categories

 ### Market consistency

 - [x] Requirements linked to intended value proposition
- [x] Competitive dimensions identified
- [x] No unsupported claim of commercial superiority
- [x] Final competitive assessment deferred to appropriate later work

---

 # 35\. What D2 does NOT need to prove

 This is equally important.

 D2 does **not** need to prove that:

 - the prototype already works;
- the selected hardware has been purchased;
- the battery actually lasts 14 days;
- the wireless link actually reaches 10 m;
- the cloud has already processed 100 messages/s;
- the AI achieves 90% accuracy;
- the final enclosure is already ≤100 cm³;
- the system is already commercially competitive.

 Those are things that can be **designed, calculated, implemented and verified later**.

 D2 establishes the targets against which those later results can be evaluated.

---

 # 36\. The D2 mental model

 If you remember only one diagram for the exam/presentation, remember this:

```
                    D2
                     │
           ┌─────────┴─────────┐
           │                   │
      WHAT SSP DOES       HOW WELL IT DOES IT
       FUNCTIONAL          PERFORMANCE
           │                   │
     ┌─────┼─────┐       ┌─────┼───────────────┐
     │     │     │       │     │       │       │
  Device Edge Cloud    Latency Energy  Range  Cost
                 │
                 UI
                 │
                DATA
                 │
       Type + Format + Size
       + Rate + Packet volume
```

 And then:

```
D2 requirements
      ↓
D3 Architecture
      ↓
D4 Hardware / Software / Engineering
      ↓
D5 AI / Edge AI
      ↓
D6 Validation + Economics
```

 ## Bottom line

 The revised SSP D2 is **substantively aligned with the official questions**. Its strongest aspects are the complete Device–Edge–Cloud–UI functional decomposition, explicit data specification, functional/performance separation, and quantitative targets for latency, throughput, communication, energy, mechanical constraints, cloud, UI and cost.

 For your actual submission, however, I would treat this **Answer-Included Study & Assessment as a learning document**, not the document you submit. The submission should be the clean **IEEE-style D2 Functional & Performance Specifications**, containing the requirements without the teaching commentary and assessment marks.
