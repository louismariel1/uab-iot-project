 ## TD1 — Derived structure of Project 2

 From the material you provided, **P2 (SMARTMOBALARM)** follows this overall structure:

 1. **Introduction / problem definition**
   - Portable security as the central problem.
   - Limitations of traditional wired and subscription-based alarm systems.
   - Need for a portable, autonomous and connectivity-independent security solution.
   - Target applications such as homes, vehicles, construction sites and logistics assets.
2. **System objectives and requirements**
   - Portable alarm functionality.
   - Acoustic and vibration sensing.
   - LTE-M connectivity.
   - GNSS/geolocation.
   - Low-power operation.
   - Twenty-day-plus autonomy.
   - Sub-20-second end-to-end event latency.
   - AI classification accuracy above 90%.
   - Cloud availability and data-storage requirements.
   - Security requirements based on the CIA Triad.
3. **System architecture**
   - Three principal system domains:\
      **Device → Cloud → User Interface**.
   - Embedded sensing and processing on the device.
   - Cellular/LTE-M communication.
   - Cloud-based processing and storage.
   - Web/mobile user interface.
   - Architecture diagrams for the overall system, device, cloud and UI.
4. **Hardware / embedded device design**
   - Nordic nRF9160 cellular IoT SiP.
   - Knowles digital microphone.
   - Vibration sensor.
   - GNSS capability.
   - Li-Po battery.
   - Power-management subsystem.
   - PCB.
   - IP65 enclosure.
   - Component selection and integration.
5. **Embedded software and sensing**
   - Acoustic acquisition.
   - Vibration monitoring.
   - Event detection.
   - Local data processing.
   - Audio compression.
   - Cellular transmission.
   - Power-management logic.
   - Sensor integration.
6. **Communication subsystem**
   - LTE-M cellular connectivity.
   - GNSS/location communication.
   - Cloud communication.
   - MQTT/IoT messaging infrastructure.
   - Network homologation.
   - LTE-M infrastructure assumptions.
   - Communication latency requirements.
7. **AI / cloud intelligence**
   - Cloud-based AI classification.
   - Acoustic-event classification.
   - Detection of relevant security events.
   - > 90% classification-accuracy target.
   - Audio compression before transmission.
   - Cloud-based processing pipeline.
8. **Cloud and user interface**
   - Cloud ingestion.
   - Data pipeline.
   - AI processing.
   - Storage.
   - Alert generation.
   - Mobile/web applications.
   - User interaction and monitoring.
   - Availability target \>99.5%.
   - Approximately 200 MB/device/month storage requirement.
9. **Security and data management**
   - CIA Triad:\
      **Confidentiality, Integrity, Availability**.
   - Data-pipeline validation.
   - GDPR-related legal considerations.
   - Cloud infrastructure.
   - Secure communication and data handling.
10. **Energy and performance analysis**
    - Battery autonomy.
    - Approximately 80 mWh/day consumption target.
    - Up to 22 days of continuous monitoring.
    - Audio/data compression.
    - End-to-end latency.
    - Vibration threshold.
    - Geolocation update interval.
11. **Prototyping and implementation**
    - Component procurement.
    - PCB assembly.
    - Mechanical enclosure development.
    - Prototype assembly.
    - Refinement and optimization.
    - Field testing.
12. **Testing and validation**
    - Battery/autonomy testing.
    - Latency validation.
    - Sensor calibration.
    - CIA Triad validation.
    - Logistics-flow testing.
    - Field testing.
    - Product polishing.
13. **Certification and regulatory compliance**
    - Technical documentation.
    - CE-related testing.
    - Safety and electromagnetic compatibility.
    - Physical compliance/homologation.
    - LTE-M/network homologation.
    - EU-specific homologations.
14. **Commercialization / deployment**
    - Manufacturing.
    - EMS manufacturing partner.
    - 3PL distribution.
    - BPO after-sales support.
    - Distributor agreements.
    - Social-media marketing.
    - SEO.
    - Product launch.
15. **Economic and business analysis**
    - Legal entity constitution.
    - NRE.
    - Personnel costs.
    - Manufacturing setup.
    - Certification costs.
    - Cloud infrastructure.
    - Marketing.
    - Indirect costs.
    - Contingency.
    - Total implementation budget.
    - Unit cost.
    - Selling price.
    - Unit margin.
    - Deployment scenarios.
    - Break-even analysis.
    - Revenue forecast.
16. **Project planning**
    - Development.
    - Prototyping.
    - Testing.
    - Certification.
    - Commercialization.
    - GANTT/timeline.
    - Parallel task execution.
    - Mandatory yearly rest periods.
    - Task/resource allocation.
17. **Conclusion**
    - Technical feasibility.
    - Autonomy and latency achievements/targets.
    - AI performance.
    - Economic viability.
    - Unit economics.
    - Investment requirement.
    - Break-even and commercialization conditions.
18. **KPIs and performance specifications**
    - Battery life.
    - Power consumption.
    - Audio sampling.
    - Vibration sampling.
    - Detection latency.
    - Vibration threshold.
    - GNSS update rate.
    - Audio compression.
    - AI accuracy.
    - Cloud storage.
    - Cloud uptime.
19. **Team roles and contributions**
    - Andreu Plana: hardware/sensor-oriented work.
    - Zakaria Boudich: cloud, economics and UI.
    - Workload distribution.
20. **AI-tool disclosure**
    - Claude 3.5 Sonnet.
    - Gemini.
    - Use for LaTeX, drafting and ideation.
    - Explicit acknowledgement of AI-generated technical inaccuracies and the need for manual verification.
21. **References**
22. **Appendices**
    - Architecture diagrams.
    - nRF9160 diagram.
    - Project planning/GANTT.
    - Detailed task/resource allocation.
    - Break-even visualization.
    - Cumulative sales projection.

---

 # TD2 — Comparison of P1 and P2 structures

 The two projects have **very similar macro-structures**, but they emphasize different engineering aspects.

 | Structural element | P1 | P2 |
| --- | --- | --- |
| **Problem / use case** | Environmental acoustic monitoring | Portable security/alarm system |
| **Primary sensing** | Acoustic | Acoustic + vibration + GNSS |
| **Connectivity** | LoRa/LPWAN + gateway | LTE-M cellular |
| **Architecture** | Device → Gateway → Cloud → UI | Device → Cloud → UI |
| **Edge processing** | Strong TinyML/EdgeAI emphasis | More emphasis on cloud AI |
| **Hardware design** | Very detailed | Very detailed |
| **Embedded software** | Strong | Strong |
| **Communication analysis** | Very extensive | More focused on LTE-M/network integration |
| **AI** | EdgeAI/TinyML | Cloud-based classification |
| **Cloud** | Strong | Strong |
| **Energy analysis** | Very extensive, including solar | Battery autonomy focused |
| **Security** | Present implicitly | Explicit CIA Triad \+ GDPR |
| **PoC / pilot** | 10-node pilot → 500-node deployment | Physical alarm prototype → commercial product |
| **Testing** | Performance/KPI validation | Battery, latency, sensor, security and field validation |
| **Certification** | Planning/compliance | Explicit CE/EMC/network homologation phase |
| **Manufacturing** | Industrialization planning | Explicit EMS/manufacturing setup |
| **Distribution** | Commercialization | Explicit 3PL |
| **After-sales** | Less prominent | Explicit BPO support model |
| **Marketing** | Included | More explicitly developed |
| **Business model** | Detailed | Detailed |
| **Pricing** | TCO/business model | Explicit €156.15 selling price |
| **Break-even** | Included | Explicit 12,617-unit calculation |
| **Project planning** | 24-month roadmap | \~11–15-month development/commercialization planning |
| **Team roles** | Included | Included |
| **AI disclosure** | Included | Included |
| **Appendices** | Technical calculations and planning | KPIs, diagrams, GANTT, economics |

## The main structural difference

 The most important difference is **where the projects place their technical emphasis**.

 ### P1 is primarily an IoT sensing \+ EdgeAI project

 Its central chain is:

 > **Acoustic sensor → EdgeAI → LoRa → Gateway → Cloud → Dashboard**

 The gateway and low-power distributed-network architecture are therefore fundamental to P1.

 ### P2 is primarily a connected security-product project

 Its central chain is:

 > **Acoustic/vibration sensing → Embedded device → LTE-M → Cloud AI → Alert/UI**

 P2 consequently puts considerably more emphasis on:

 - cellular connectivity;
- portability;
- battery autonomy;
- security;
- certification;
- manufacturing;
- commercialization;
- after-sales operation.

 So although both projects are IoT systems, **P1 is more network/EdgeAI-oriented, whereas P2 is more productization/security-oriented**.

---

 # P1 vs. P2 at the level of project maturity

 There is also an important difference in the **engineering narrative**.

 ### P1

 P1 follows approximately:

 > **Research problem → IoT architecture → technical design → PoC → scalability → business case**

 It is particularly strong as an **IoT systems-engineering study**.

 ### P2

 P2 follows more closely:

 > **Product problem → system architecture → prototype → testing → certification → manufacturing → commercialization**

 This makes P2 resemble a **product-development and commercialization project** more strongly.

 That difference is visible in the later phases.

 P1's later stages concentrate on:

 > pilot → scalability → TCO → commercialization.

 P2 explicitly introduces:

 > prototype → validation → certification → manufacturing → distribution → launch.

---

 # TD3 — How P1 and P2 implement the official project guidelines

 Using the P1-derived template as the interpretation of the official project structure, **both projects implement the guidelines quite comprehensively**, but they do so with different emphases.

 ## 1\. Problem definition

 ### P1

 Defines a distributed environmental acoustic-monitoring problem.

 The problem naturally requires:

 - distributed sensors;
- continuous monitoring;
- wireless communication;
- low power;
- automated classification;
- cloud visualization.

 ### P2

 Defines a portable security problem.

 The problem naturally requires:

 - autonomous sensing;
- rapid event detection;
- remote connectivity;
- location information;
- low power;
- alerts;
- security;
- physical robustness.

 **Guideline implementation:** Both satisfy the requirement to start from a concrete real-world problem rather than from a technology alone.

---

 ## 2\. Requirements and KPIs

 Both projects convert their use cases into quantitative engineering requirements.

 ### P1 emphasizes

 - PDR;
- communication range;
- Macro-F1;
- inference latency;
- acoustic accuracy;
- energy consumption;
- battery/solar autonomy;
- gateway capacity;
- cloud availability.

 ### P2 emphasizes

 - > 20-day autonomy;
- \<20-second event latency;
- > 90% AI accuracy;
- 16-kHz audio;
- 2-g vibration threshold;
- GNSS update rate;
- 320 kB → 40 kB audio compression;
- > 99.5% cloud uptime.

 This is an important common feature:

 > **Neither project remains at the level of qualitative requirements.**

 Both translate the project objectives into measurable technical KPIs.

---

 # 3\. Architecture

 Both implement the IoT architecture guideline through a clear physical-to-cloud chain.

 ### P1

 **Device → LoRa → Gateway → Cloud → UI**

 ### P2

 **Device → LTE-M → Cloud → UI**

 This is an especially useful comparison because it demonstrates that the same general IoT architecture can be adapted to different deployment requirements.

 P1 requires a local gateway because many nodes share an LPWAN infrastructure.

 P2 removes that gateway layer by giving each alarm direct cellular connectivity.

---

 # 4\. Hardware implementation

 Both projects satisfy the hardware-design component of the guidelines through actual component selection.

 P1 focuses on:

 - microphone;
- MCU;
- LoRa;
- PMIC;
- battery;
- solar harvesting;
- enclosure;
- gateway.

 P2 focuses on:

 - nRF9160;
- digital microphone;
- vibration sensor;
- GNSS;
- Li-Po battery;
- PCB;
- IP65 enclosure.

 The important common point is that both projects perform **system-level component selection rather than simply listing components**.

---

 # 5\. Embedded software

 Both projects implement the embedded portion of the IoT system.

 P1 emphasizes:

 > sensing → feature extraction → TinyML → transmission → power management.

 P2 emphasizes:

 > sensing → event acquisition → compression → cellular transmission → power management.

 Therefore, both satisfy the requirement that the physical device contain meaningful local computation rather than functioning as a simple sensor.

---

 # 6\. Communication

 This is where their implementation differs most clearly.

 ### P1

 Uses an LPWAN architecture:

 > **Node → LoRa → Gateway → Cloud**

 This requires analysis of:

 - range;
- packet delivery;
- gateway capacity;
- channel occupancy;
- packet loss.

 ### P2

 Uses cellular IoT:

 > **Node → LTE-M → Cloud**

 Consequently, the project must address:

 - cellular coverage;
- LTE-M compatibility;
- network homologation;
- network certification;
- direct device-to-cloud communication.

 Thus, both satisfy the communication requirement, but **they solve it using fundamentally different network architectures**.

---

 # 7\. AI

 P1 and P2 both incorporate AI, but in different architectural positions.

 ### P1

 AI is deliberately pushed toward the **edge**.

 This reduces:

 - transmitted data;
- communication energy;
- latency;
- cloud processing requirements.

 ### P2

 AI is primarily part of the **cloud intelligence pipeline**.

 The device captures and compresses acoustic data, while the cloud performs classification.

 This allows the project to exploit greater cloud computational resources while simplifying the embedded device.

 Therefore:

 > **P1 uses AI primarily as an edge-computing optimization; P2 uses AI primarily as a cloud-based security-analysis mechanism.**

---

 # 8\. Cloud and user interface

 Both projects provide the complete upper layers required for an IoT system.

 ### P1

 Cloud:

 - ingestion;
- database;
- processing;
- alerts;
- APIs;
- multi-tenancy.

 UI:

 - web/mobile dashboards;
- maps;
- time series;
- monitoring.

 ### P2

 Cloud:

 - ingestion;
- AI;
- storage;
- alerting;
- data pipeline.

 UI:

 - mobile/web interaction;
- alarm monitoring.

 So both demonstrate the complete path:

 > **Physical event → digital data → cloud processing → user-visible information.**

---

 # 9\. Energy engineering

 This is a particularly strong area in both projects.

 P1 goes further into **energy harvesting and environmental energy balance**.

 P2 focuses more strongly on **battery autonomy**, with the requirement of approximately 20\+ days.

 That difference reflects their deployment environments:

 - P1: fixed/distributed environmental sensors → solar harvesting is practical.
- P2: portable alarm → battery-only operation is more appropriate.

---

 # 10\. Testing and validation

 Both include a dedicated validation stage.

 ### P1

 Validation is strongly KPI-oriented:

 - acoustic accuracy;
- PDR;
- inference performance;
- energy;
- cloud performance.

 ### P2

 Validation is more product-oriented:

 - sensor calibration;
- battery stress testing;
- latency;
- security/data pipeline;
- field testing;
- logistics;
- certification preparation.

 This is another indication that P2 is structured more explicitly around **taking a prototype toward a marketable product**.

---

 # 11\. Certification and regulatory compliance

 This is one area where **P2 has a much more explicit structural role**.

 P2 has an entire:

 > **Certification → Technical documentation → Physical compliance → Network homologation → EU-specific homologations**

 sequence.

 This makes sense because the project is explicitly targeting a commercial LTE-connected security product in the EU.

 P1 includes certification considerations, but they are less dominant in the project structure.

---

 # 12\. Economics and commercialization

 Both projects strongly implement the business/economic requirement.

 P1 covers:

 - NRE;
- TCO;
- personnel;
- deployment;
- scalability;
- subscription/business model;
- break-even.

 P2 covers these as well, but additionally makes the **unit economics** particularly explicit:

 > Unit cost = €124.90\
>  Selling price = €156.15\
>  Unit margin = €31.25\
>  Initial investment ≈ €394,284\
>  Break-even ≈ 12,617 units

 This makes the economic model very easy to connect to the technical design.

---

 # 13\. Project management

 Both projects include:

 - development phases;
- task breakdown;
- resource allocation;
- timelines;
- milestones;
- commercialization stages.

 P2's structure is particularly explicit because Table XIX connects:

 > **task → duration → responsible resource**

 This is a direct implementation of the project-management aspect of the guidelines.

---

 # 14\. Team contribution and AI disclosure

 Both projects satisfy the expected academic transparency requirements.

 P2 explicitly identifies:

 - individual contributions;
- use of AI tools;
- appropriate uses of AI;
- limitations;
- examples of inaccurate AI-generated technical information;
- need for manual verification.

 That last point is particularly valuable for an engineering report because it distinguishes **AI-assisted drafting** from **engineering validation**.

---

 # Overall comparison

 The relationship between the two projects can therefore be summarized as:

 | Dimension | P1 | P2 |
| --- | --- | --- |
| Central identity | **IoT monitoring system** | **IoT security product** |
| Main sensing problem | Environmental sound | Security events |
| Network architecture | LoRa + gateway | LTE-M direct connectivity |
| AI location | Edge | Primarily cloud |
| Energy strategy | Battery + solar | Li-Po battery |
| Main technical challenge | Distributed scalable sensing | Autonomous portable security |
| Validation emphasis | IoT/network/energy KPIs | Product/security/latency/autonomy |
| Regulatory emphasis | Moderate | High |
| Manufacturing emphasis | High | Very high |
| Commercialization emphasis | High | Very high |
| Business model | System/deployment-oriented | Product/unit-economics-oriented |
| Overall project character | **IoT system engineering** | **IoT product engineering** |

## Final conclusion for TD1–TD3

 The two projects are **structurally compatible with the same official project methodology**, even though their technical architectures differ.

 The common underlying structure is:

 > **Problem → Requirements → Architecture → Hardware/Software → Communication → AI/Data → Cloud/UI → Energy → Implementation → Testing → Economics → Planning → Conclusion**

 P1 develops this structure around a **distributed environmental-monitoring platform**, while P2 develops it around a **portable security product**.

 The strongest distinction is therefore not that one follows the guidelines and the other does not. **Both follow them.** The distinction is in what each project emphasizes:

 - **P1:** distributed IoT architecture, LPWAN, EdgeAI, energy harvesting and scalable sensing.
- **P2:** cellular IoT, portability, battery autonomy, security, certification, manufacturing and commercialization.
