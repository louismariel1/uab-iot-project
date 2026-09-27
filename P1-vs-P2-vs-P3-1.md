 # TD2 — Structural comparison of P1, P2, and P3

 At a high level, all three projects follow essentially the same engineering-product lifecycle:

 **Problem → requirements → architecture → hardware/software → connectivity → intelligence → energy/performance → implementation → validation → economics → commercialization → planning**

 The main difference is **which part of that lifecycle receives the greatest engineering emphasis**.

 - **P1 / EchoSense:** distributed environmental sensing, LoRa/LPWAN, EdgeAI/TinyML, energy harvesting, and large-scale IoT deployment.
- **P2 / SMARTMOBALARM:** portable security, LTE-M, GNSS, cloud AI, autonomous battery operation, cybersecurity, and commercialization.
- **P3 / SPSC:** smart parking, ultrasonic occupancy sensing, LoRaWAN, cloud backend, mobile/web applications, AI-based prediction, and campus-scale deployment.

 ## 1\. Direct structural mapping

 | Engineering area | P1 — EchoSense | P2 — SMARTMOBALARM | P3 — SPSC | Structural observation |
| --- | --- | --- | --- | --- |
| Problem / use case | Environmental acoustic monitoring | Portable security/alarm | Campus parking availability | All define a concrete IoT problem |
| Target users | Universities, municipalities, campus operators | Homes, vehicles, construction/logistics users | Universities, campus operators, parking users | P3 is strongly institutional/campus-oriented |
| Requirements | Extensive quantitative KPI appendix | Extensive KPI/performance requirements | Performance, latency, power, scalability and availability requirements | All formalize requirements |
| Market/context | Environmental monitoring | Security/alarm market | Smart parking / campus mobility | All include commercial justification |
| System architecture | Device → LoRa → Gateway → Cloud → UI | Device → LTE-M → Cloud → UI | Sensor → LoRaWAN → Gateway → Cloud → Web/Mobile | P1 and P3 require gateway infrastructure; P2 does not |
| Hardware | MEMS microphone, MCU, LoRa, battery, solar, enclosure | nRF9160, microphone, vibration sensor, GNSS, Li-Po, PCB, enclosure | Ultrasonic sensor, LoRa-capable node, battery/power system, gateway | All contain component-level hardware design |
| Embedded software | Acquisition, TinyML, feature extraction, power management | Acquisition, event detection, compression, transmission, power management | Occupancy sensing, local processing, communication, power management | P1 has strongest explicit EdgeAI role |
| Communication | LoRa/LPWAN | LTE-M, GNSS, MQTT | LoRaWAN, gateway/cloud communication | P1/P3 emphasize LPWAN; P2 emphasizes cellular |
| AI | **EdgeAI/TinyML** | **Cloud AI** | **AI prediction module / cloud analytics** | Intelligence is distributed differently |
| Data flow | Sensor → EdgeAI → LoRa → Gateway → Cloud | Sensor → processing → LTE-M → Cloud AI | Sensor → LoRaWAN → Gateway → Cloud → prediction/UI | P3 moves from sensing to centralized analytics |
| Cloud | Ingestion, storage, processing, alerts, APIs | Ingestion, AI, storage, alerts, UI | Backend, storage, real-time availability, analytics, prediction | Cloud is important in all three |
| User interface | Web/mobile dashboard | Web/mobile application | Web/mobile parking application | All provide user-facing software |
| Security | Platform/data considerations | **Explicit CIA Triad + GDPR** | Cloud/data security considerations | P2 has the most explicit security structure |
| Energy | Detailed power model + battery + solar | Battery autonomy + low-power operation | Low-power operation + battery/autonomy | P1 has strongest energy-generation analysis |
| Prototype | 10-node pilot/deployment planning | Prototype assembly, PCB, enclosure, field testing | Deployment/prototype planning and gateway integration | All address physical implementation |
| Validation | Acoustic, AI, PDR, latency, cloud, energy | Autonomy, latency, sensors, security, field tests | Occupancy, communication, latency, prediction, cloud, energy | Different validation domains |
| Certification | Acoustic/environmental/product certification | CE, EMC, safety, LTE-M/network homologation | Certification considerations for IoT deployment | P2 has strongest explicit regulatory emphasis |
| Manufacturing | Manufacturing readiness, EMS considerations | EMS + 3PL + BPO + manufacturing | Device production and deployment economics | P2 has the most explicit operational chain |
| Business model | Hardware + cloud/service | Product + services/deployment | Hardware/system + cloud/service/deployment | All move beyond prototype engineering |
| Economics | NRE, TCO, pricing, break-even, 500-node deployment | NRE, personnel, certification, cloud, marketing, unit cost, margin, break-even | Unit cost, installation, deployment scale, break-even | All include economic feasibility |
| Scalability | Hundreds/thousands of nodes | Manufacturing/distribution/customer scaling | Campus-scale sensor deployment | P1 and P3 have particularly strong network/deployment scalability |
| Project planning | 24-month GANTT, milestones | Development → prototype → certification → launch | GANTT, dependencies, development timeline | All include formal project planning |
| Team roles | Included | Included | Included | All address accountability |
| AI disclosure | Included | Included | Included | All explicitly disclose AI-tool use |
| References | Included | Included | Included | All contain formal references |
| Appendices | KPI/component/power/GANTT | Architecture/GANTT/break-even/task allocation | Protocol comparison + GANTT | All use appendices for supporting material |

---

 # 2\. Major structural similarities

 ## A. All three are complete product-development projects

 None of the projects is merely a description of an IoT device.

 They all progress through approximately:

 **technical problem → requirements → architecture → implementation → validation → economics → commercialization → project planning.**

 This is significant because it indicates that all three are structured as **end-to-end IoT product proposals**, rather than isolated technical prototypes.

---

 ## B. P1 and P3 share a particularly similar IoT architecture

 P1:

```
Sensor Node
    ↓
LoRa / LPWAN
    ↓
Gateway
    ↓
Cloud
    ↓
Web / Mobile UI
```

 P3:

```
Parking Sensor
    ↓
LoRaWAN
    ↓
Gateway
    ↓
Cloud Backend
    ↓
Web / Mobile UI
```

 P2:

```
Smart Alarm Device
    ↓
LTE-M
    ↓
Cloud
    ↓
Web / Mobile UI
```

 This creates an important three-project distinction:

 > **P1 and P3 are infrastructure-oriented LPWAN IoT systems, while P2 is a directly connected cellular IoT product.**

 The gateway is therefore a significant system component in P1 and P3 but is not required in P2's basic architecture.

---

 # 3\. The three different approaches to intelligence

 This is one of the most useful structural comparisons.

 ### P1 — Edge intelligence

```
Sensor
 ↓
Feature extraction
 ↓
TinyML
 ↓
Classification
 ↓
LoRa
 ↓
Gateway
 ↓
Cloud
```

 The device performs substantial processing locally.

 This is closely connected to P1's objectives of reducing communication load and power consumption.

 ### P2 — Cloud intelligence

```
Sensor / event
 ↓
Local processing
 ↓
LTE-M
 ↓
Cloud
 ↓
AI classification
 ↓
Alert
```

 P2 places more computational intelligence in the cloud.

 ### P3 — Cloud analytics and prediction

```
Occupancy sensor
 ↓
LoRaWAN
 ↓
Gateway
 ↓
Cloud backend
 ↓
Historical data
 ↓
AI prediction
 ↓
Parking availability / planning
```

 P3 uses AI primarily as a **prediction and planning layer**, rather than making AI-based classification the central function of each parking sensor.

 This gives the three projects three distinct intelligence models:

 | Project | Main intelligence location | Main purpose |
| --- | --- | --- |
| P1 | Edge/device | Local acoustic classification |
| P2 | Cloud | Security/event classification |
| P3 | Cloud | Parking-demand/availability prediction |

---

 # 4\. P3 is structurally closest to P1

 P3 shares several important characteristics with P1:

 - distributed sensor nodes;
- LoRa/LoRaWAN communication;
- gateway infrastructure;
- campus/institutional deployment;
- large numbers of devices;
- low-power operation;
- cloud backend;
- web/mobile interfaces;
- deployment-scale economics;
- network scalability;
- installation considerations.

 The principal difference is the sensing problem.

 ### P1

 **Continuous environmental/acoustic sensing**

 The system must interpret relatively complex sensor data and therefore places considerable emphasis on EdgeAI/TinyML.

 ### P3

 **Binary/near-binary occupancy detection**

 The fundamental sensor question is essentially whether a parking space is occupied. This allows P3's architecture to focus more heavily on:

 - reliable occupancy detection;
- LoRaWAN communication;
- low-power operation;
- real-time availability;
- cloud analytics;
- prediction;
- deployment economics.

---

 # 5\. P3's main technical emphasis: networked occupancy sensing

 P3's engineering problem can be represented as:

```
Parking Space
     ↓
Ultrasonic Occupancy Sensor
     ↓
Low-power IoT Node
     ↓
LoRaWAN
     ↓
Gateway
     ↓
Cloud Backend
     ↓
Availability Database
     ↓
Mobile/Web Application
     ↓
AI Prediction
```

 Therefore, unlike P1, where **signal interpretation** is a major challenge, P3's major challenge is the **reliable deployment of a large distributed occupancy-sensing network**.

 That explains why the P3 material gives considerable attention to:

 - communication protocols;
- LoRaWAN;
- gateway infrastructure;
- power consumption;
- device cost;
- installation;
- deployment scale;
- break-even;
- cloud services;
- parking availability;
- prediction.

---

 # 6\. P1 vs P2 vs P3 — technical emphasis

 | Technical dimension | P1 | P2 | P3 |
| --- | --- | --- | --- |
| Distributed sensing | **Very high** | Moderate | **Very high** |
| Environmental sensing | **Very high** | Low | Low |
| Acoustic sensing | **Very high** | High | Low |
| Occupancy sensing | Low | Low | **Very high** |
| Edge processing | **Very high** | Moderate | Moderate |
| EdgeAI/TinyML | **Very high** | Lower | Low/Moderate |
| LPWAN | **Very high** | None | **Very high** |
| Cellular | Low | **Very high** | Low |
| GNSS | Low | **Very high** | None |
| Cloud AI | Moderate | **Very high** | **High** |
| Cloud platform | High | **Very high** | **Very high** |
| Energy optimization | **Very high** | **Very high** | **Very high** |
| Solar | High | None | Not central |
| Battery | High | **Very high** | High |
| Cybersecurity | Moderate | **High** | Moderate |
| GDPR/privacy | Moderate | **High** | Moderate |
| Certification | High | **Very high** | Moderate/High |
| Network scalability | **Very high** | Moderate | **Very high** |
| Gateway engineering | **Very high** | None | **Very high** |
| Prediction/analytics | Moderate | High | **Very high** |
| Manufacturing | High | **Very high** | High |
| Distribution/operations | Moderate | **High** | Moderate |
| Deployment economics | **Very high** | High | **Very high** |

Again, this is a **structural comparison of emphasis**, not a quality ranking.

---

 # 7\. P3's economics are particularly connected to deployment scale

 The P3 material adds an important economic component that fits naturally into the three-project comparison.

 The document estimates an installation cost of approximately **€3,100–€4,700** for a 5,000-device deployment, corresponding to approximately:

 - **€0.62/device** at the lower estimate;
- **€0.94/device** at the upper estimate.

 With the stated base device price of €93, this gives approximately:

 **€93.62–€93.94 per device including the amortized installation cost.**

 The document also states a break-even point of approximately **950 units**.

 This reinforces a central characteristic of P3:

 > **The economics are strongly dependent on deployment scale because fixed installation costs become relatively small when distributed across a large number of devices.**

 That is conceptually similar to P1's large-scale deployment economics.

---

 # 8\. P3's protocol comparison strengthens its architecture section

 P3 also contains an explicit appendix comparing:

 - MQTT;
- AMQP;
- HTTP/HTTPS.

 This is structurally useful because it demonstrates that the communication protocol was not simply chosen without comparison.

 The appendix considers characteristics such as:

 - architecture;
- command targets;
- underlying transport;
- secure connections;
- observability;
- messaging mode;
- message queuing;
- overhead;
- message size;
- content type;
- topic matching;
- reliability;
- connection multiplexing;
- message attributes;
- object persistence.

 This makes P3's architecture section more complete because the communication layer is treated as an **engineering decision** rather than merely a named technology.

---

 # TD3 — P1, P2 and P3 against the official project structure

 ## 1\. Problem / use case

 | Requirement | P1 | P2 | P3 |
| --- | --- | --- | --- |
| Clearly defined problem | Yes | Yes | Yes |
| Concrete IoT use case | Yes | Yes | Yes |
| Deployment context | Campus/municipality | Home/vehicle/construction/logistics | University/campus |
| Motivation | Environmental monitoring | Security | Parking efficiency/congestion |

**Overall:** all three clearly satisfy this structural requirement.

---

 ## 2\. Users and stakeholders

 ### P1

 Focuses on:

 - universities;
- municipalities;
- campus operators;
- technical/operations personnel;
- B2B customers.

 ### P2

 Includes:

 - homeowners;
- vehicle users;
- construction operators;
- logistics/asset operators;
- distributors;
- support organizations.

 ### P3

 Primarily addresses:

 - universities;
- campus operators;
- parking users;
- facility managers;
- technical/operations personnel.

 A useful common improvement would be a formal:

 **Stakeholder → need → system function → KPI**

 matrix.

---

 # 3\. Requirements and KPIs

 All three projects formalize their requirements.

 ### P1 emphasizes

 - acoustic accuracy;
- AI classification;
- PDR;
- latency;
- power;
- cloud availability.

 ### P2 emphasizes

 - AI accuracy;
- battery autonomy;
- daily energy;
- event latency;
- cloud availability;
- GNSS;
- sensing thresholds.

 ### P3 emphasizes

 - occupancy detection;
- communication performance;
- latency;
- low-power operation;
- cloud availability;
- scalability;
- prediction.

 Thus:

 > **P1's requirements are strongly measurement/network/energy-oriented; P2's are security/autonomy/connectivity-oriented; P3's are occupancy/network/scalability-oriented.**

---

 # 4\. Architecture

 All three satisfy the architecture requirement clearly.

 ### P1

 **Device → Gateway → Cloud → UI**

 ### P2

 **Device → LTE-M → Cloud → UI**

 ### P3

 **Sensor → LoRaWAN → Gateway → Cloud → UI**

 P3 therefore structurally resembles P1 more than P2.

---

 # 5\. Hardware

 All three provide component-level hardware design.

 ### P1

 - MEMS microphone;
- MCU;
- LoRa radio;
- battery;
- solar;
- PMIC;
- enclosure;
- gateway.

 ### P2

 - nRF9160;
- digital microphone;
- vibration sensor;
- GNSS;
- Li-Po;
- PMIC;
- PCB;
- enclosure.

 ### P3

 - ultrasonic occupancy sensor;
- low-power IoT/LoRa node;
- battery/power system;
- gateway;
- enclosure/deployment hardware.

 The three represent three different physical product architectures:

 **P1 = environmental sensor node**

 **P2 = integrated cellular smart device**

 **P3 = distributed parking-space sensor network**

---

 # 6\. Software

 All three include the major software layers:

 - embedded firmware;
- sensing;
- processing;
- communication;
- cloud/backend;
- database;
- application/UI.

 The distinction is again in emphasis:

 - **P1:** embedded AI;
- **P2:** cloud AI/security application;
- **P3:** cloud availability/analytics/prediction.

---

 # 7\. Communication

 Communication is a major engineering subsystem in all three.

 | Project | Main communication | Structural problem |
| --- | --- | --- |
| P1 | LoRa/LPWAN | Large distributed network |
| P2 | LTE-M | Direct cellular connectivity |
| P3 | LoRaWAN | Large distributed parking network |

P3's communication architecture is particularly similar to P1 because both require gateways and distributed low-power nodes.

---

 # 8\. AI

 All three incorporate AI, but in different ways.

 ### P1

 **EdgeAI/TinyML**

 AI directly reduces the amount of information that needs to be transmitted.

 ### P2

 **Cloud AI**

 AI performs higher-level security/event analysis in the cloud.

 ### P3

 **AI prediction**

 AI uses accumulated parking data to forecast availability/demand and support facility planning.

 This is an important distinction:

 > P1 uses AI primarily for **local interpretation**, P2 for **centralized event intelligence**, and P3 for **forecasting and operational planning**.

---

 # 9\. Energy

 All three address energy explicitly.

 ### P1

 **Current → duty cycle → power → battery → solar → autonomy**

 ### P2

 **Event/monitoring consumption → daily energy → battery → autonomy**

 ### P3

 **Sensor/communication duty cycle → average consumption → battery/autonomy**

 The engineering problem differs:

 - **P1:** energy-autonomous distributed sensing;
- **P2:** long-duration portable battery operation;
- **P3:** low-cost, low-power operation across many parking sensors.

---

 # 10\. Cloud

 All three include:

 - data ingestion;
- storage;
- processing;
- application services;
- alerts/notifications or outputs;
- user interface;
- availability considerations.

 The role differs:

 - P1: cloud aggregation and analytics;
- P2: cloud intelligence and security application;
- P3: real-time parking data, analytics, and prediction.

---

 # 11\. Security and privacy

 This remains one of the clearest structural differences.

 ### P1

 Security exists, but is not as strongly separated as its own engineering domain.

 ### P2

 Security is explicitly structured around:

 **Confidentiality → Integrity → Availability**

 with GDPR, secure communication, cloud security, and data handling.

 ### P3

 Security and data protection are relevant to the cloud/backend architecture, but the material supplied for P3 does not give security the same dedicated depth as P2.

 Therefore:

 > **P2 has the most explicit security/privacy structure; P1 and P3 could strengthen this part by making security requirements and mechanisms more visible as dedicated subsections.**

---

 # 12\. PoC / implementation

 All three address implementation, but there is an important documentation issue across the projects.

 The final documents should clearly distinguish:

 - **implemented;**
- **experimentally tested;**
- **calculated;**
- **simulated;**
- **planned;**
- **target value;**
- **assumption.**

 This is especially important because some of the P3 conclusions describe the proposed system in language that can sound as though it has already been experimentally validated.

---

 # 13\. Testing and validation

 The three projects have different validation priorities.

 ### P1

```
Acoustic
AI
Communication
Energy
Cloud
Environmental
Certification
```

 ### P2

```
Battery
Latency
Sensors
Security
Connectivity
Field operation
Certification
```

 ### P3

```
Occupancy detection
Communication
Latency
Energy
Cloud
Prediction
Scalability
Deployment
```

 A common formal validation matrix would strengthen all three:

 | Requirement | Target | Test method | Result | Status |
| --- | --- | --- | --- | --- |
| KPI | Target value | Measurement/test | Actual value | Pass/Planned |
| Communication | Target | Network test | Measured result | Pass/Planned |
| Energy | Target | Power measurement | Measured/calculated | Pass/Planned |
| Cloud | Target | Availability/load test | Result | Pass/Planned |

---

 # 14\. Business and economics

 All three contain significant economic analysis.

 ### P1

 Strong emphasis on:

 - NRE;
- TCO;
- hardware/service pricing;
- deployment scale;
- 500-node deployment;
- break-even.

 ### P2

 Broader operating model:

 - personnel;
- manufacturing;
- certification;
- cloud;
- marketing;
- indirect costs;
- contingency;
- unit economics;
- margin;
- revenue;
- break-even.

 ### P3

 Strong emphasis on:

 - device cost;
- installation cost;
- per-device cost;
- deployment scale;
- break-even;
- economics of large deployments.

 This gives a useful three-way distinction:

 > **P1 emphasizes IoT network deployment economics; P2 emphasizes complete product/company operating economics; P3 emphasizes campus-scale deployment economics.**

---

 # 15\. Commercialization

 ### P1

```
Prototype
 ↓
Pilot
 ↓
Manufacturing readiness
 ↓
Large deployment
 ↓
Commercial launch
```

 ### P2

```
Prototype
 ↓
Certification
 ↓
EMS manufacturing
 ↓
3PL
 ↓
Distribution
 ↓
Marketing
 ↓
Sales
 ↓
Support
```

 ### P3

```
Prototype / pilot
 ↓
Deployment
 ↓
Large-scale production
 ↓
Campus installation
 ↓
Cloud service
 ↓
Commercial deployment
```

 P2 remains the project with the most explicit **end-to-end commercial operations chain**.

 P1 and P3 are more strongly structured around **large-scale IoT deployment**.

---

 # 16\. Project planning

 All three include project planning.

 - **P1:** 24-month GANTT and manufacturing/commercial milestones.
- **P2:** development, prototype, testing, certification, commercialization, and resource/task planning.
- **P3:** GANTT diagram showing project timeline and dependencies.

 Therefore all three satisfy the planning component structurally.

---

 # 17\. Team accountability and AI disclosure

 All three include:

 - team contributions;
- responsibilities;
- workload/contribution percentages;
- AI-tool disclosure;
- references.

 P3 specifically states that ChatGPT and Microsoft Copilot were used for:

 - general information;
- concept clarification;
- content structuring;
- processing professor feedback;
- illustrative images/diagrams.

 It also acknowledges limitations in AI-generated technical information and the need for verification.

 That is consistent with the disclosure structure already present in P1 and P2.

---

 # Consolidated TD3 matrix

 | Official project element | P1 — EchoSense | P2 — SMARTMOBALARM | P3 — SPSC | Main structural observation |
| --- | --- | --- | --- | --- |
| Problem/use case | **Covered** | **Covered** | **Covered** | Different IoT applications |
| Users/stakeholders | **Covered** | **Covered** | **Covered** | P2 has broadest application range |
| Requirements/KPIs | **Very strong** | **Strong** | **Strong** | Different KPI emphasis |
| Market/context | **Covered** | **Covered** | **Covered** | All provide commercial context |
| IoT architecture | **Very strong** | **Very strong** | **Very strong** | P1/P3 use gateway architecture |
| Hardware | **Very strong** | **Very strong** | **Strong** | Different physical architectures |
| Embedded software | **Strong** | **Strong** | **Strong** | Different processing strategies |
| Communication | **Very strong** | **Very strong** | **Very strong** | LoRa vs LTE-M |
| Data flow | **Covered** | **Covered** | **Covered** | All define device-to-cloud flow |
| AI | **Very strong** | **Strong** | **Strong** | EdgeAI vs cloud AI vs prediction |
| Cloud | **Strong** | **Very strong** | **Very strong** | Cloud central to all |
| Security/privacy | **Present** | **Very strong/explicit** | **Present** | P2 has strongest explicit treatment |
| Energy | **Very strong** | **Very strong** | **Strong** | Solar vs battery vs low-power network |
| PoC/implementation | **Covered** | **Covered** | **Covered** | Evidence/status should be distinguished |
| Validation | **Strong** | **Strong** | **Strong** | Different test domains |
| Certification | **Covered** | **Very strong** | **Covered** | P2 most explicit |
| Business model | **Very strong** | **Very strong** | **Strong** | Different commercial models |
| Cost/TCO | **Very strong** | **Very strong** | **Very strong** | All address feasibility |
| Scalability | **Very strong** | **Strong** | **Very strong** | P1/P3 are distributed-network projects |
| Manufacturing | **Strong** | **Very strong** | **Strong** | P2 most operationally detailed |
| Commercialization | **Strong** | **Very strong** | **Strong** | P2 most detailed |
| Project planning | **Covered** | **Covered** | **Covered** | All include GANTT/planning |
| Team roles | **Covered** | **Covered** | **Covered** | All explicit |
| AI disclosure | **Covered** | **Covered** | **Covered** | All explicit |
| References | **Covered** | **Covered** | **Covered** | P3 references need cleanup |
| Appendices | **Extensive** | **Extensive** | **Extensive** | Supporting technical material in all |

# Overall structural interpretation

 The three projects can be viewed as three implementations of essentially the same official project framework:

```
                    OFFICIAL PROJECT STRUCTURE
                              │
             ┌────────────────┼────────────────┐
             │                │                │
            P1               P2               P3
        EchoSense       SMARTMOBALARM          SPSC
             │                │                │
     Environmental       Security IoT      Smart Parking
          IoT                │                │
             │          Portable device   Distributed sensors
             │                │                │
        LoRa + GW           LTE-M          LoRaWAN + GW
             │                │                │
          EdgeAI           Cloud AI       Cloud prediction
             │                │                │
       Solar + battery     Li-Po battery   Low-power battery
             │                │                │
      Campus-scale IoT   Product-scale IoT  Campus-scale IoT
             │                │                │
             └────────────────┼────────────────┘
                              │
                 Cloud + Application + Business
                              │
                  Validation + Certification
                              │
                     Commercialization
```

 The clearest three-way interpretation is therefore:

 > **P1 is primarily a distributed environmental sensing and EdgeAI project. P2 is primarily a portable cellular security product with cloud intelligence and a strong cybersecurity/commercialization layer. P3 is primarily a distributed smart-parking infrastructure project based on low-power occupancy sensing, LoRaWAN, cloud services, and predictive analytics.**

 Structurally, **P3 is closer to P1 than to P2**, because both P1 and P3 depend on distributed LPWAN nodes, gateways, low-power operation, and large-scale deployment. P2 differs architecturally because cellular connectivity removes the gateway layer and shifts more intelligence and operational complexity toward the cloud, security, certification, and product operations.
