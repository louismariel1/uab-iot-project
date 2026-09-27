 # TD1 — Derived structure of Project 3

 P3 is the **Smart Parking System for Campuses (SPSC)**. Its structure can be reconstructed as follows:

 1. **Problem / use-case definition**
   - Smart parking for university campuses and large private facilities.
   - Reduction of parking-search time.
   - Reduction of congestion.
   - Real-time parking availability.
   - Long-term parking monitoring and analytics.
2. **System requirements and objectives**
   - Real-time occupancy updates.
   - Low-latency communication.
   - Scalable device-to-cloud communication.
   - Low-power operation.
   - Multi-year device autonomy.
   - Parking-availability monitoring.
   - Long-term data collection.
   - Prediction capabilities for facility managers.
3. **Overall system architecture**
   - Parking-space sensing layer.
   - IoT communication layer.
   - LoRa/LoRaWAN infrastructure.
   - Cloud/backend layer.
   - Mobile/web user interfaces.
   - AI-based prediction module.
   - Integration with existing or dedicated LoRaWAN infrastructure.
4. **Hardware / sensing subsystem**
   - Ultrasonic occupancy sensing.
   - HC-SR04 ultrasonic sensor.
   - Feather M0 with RFM95 LoRa radio.
   - SX1276/77/78/79 LoRa transceiver technology.
   - Lithium battery.
   - Wiring, connectors, enclosure and PCB materials.
5. **Embedded device / edge layer**
   - Occupancy detection.
   - Sensor processing.
   - Local device operation.
   - Low-power operation.
   - LoRa communication.
   - Multi-year autonomy considerations.
6. **Wireless communication**
   - LoRa/LoRaWAN.
   - Gateway infrastructure.
   - Device-to-gateway communication.
   - Gateway-to-cloud communication.
   - Analysis of communication protocols.
   - Comparison of MQTT, AMQP and HTTP/HTTPS.
7. **Cloud / backend**
   - IoT cloud infrastructure.
   - Device-to-cloud communication.
   - Data storage.
   - Parking occupancy data.
   - Long-term monitoring.
   - Analytics.
8. **AI / prediction**
   - AI-based parking prediction.
   - Forecasting of parking availability.
   - Support for facility-manager decision making.
   - Use of historical/contextual data.
9. **User-facing applications**
   - Mobile application.
   - Web application.
   - Real-time parking availability.
   - User interaction with parking information.
10. **Energy analysis**
    - Low-power operation.
    - Battery-powered devices.
    - Multi-year autonomy.
    - Sensor and communication energy considerations.
11. **Deployment / scalability**
    - Initial deployment.
    - Large-scale campus deployment.
    - Existing LoRaWAN infrastructure.
    - Dedicated gateway installation where required.
    - 5,000-device deployment used for cost analysis.
12. **Economic / cost analysis**
    - Hardware cost.
    - Deployment and installation cost.
    - Installation amortization.
    - Per-device cost.
    - Scale effects.
    - Fixed-cost impact on smaller deployments.
    - Break-even analysis.
13. **Break-even analysis**
    - Break-even point at approximately **950 units**.
    - Relationship between production volume and profitability.
    - Importance of scaling production and sales.
14. **Project planning**
    - GANTT diagram.
    - Project timeline.
    - Dependencies between project activities.
15. **Conclusion**
    - Technical feasibility.
    - Scalability.
    - Cost-effectiveness.
    - Parking-search and congestion reduction.
    - Sustainability.
    - Future real-world pilot.
    - Improved prediction accuracy.
    - Navigation guidance.
    - Reservation mechanisms.
    - Dynamic pricing.
16. **Team contributions**
    - Natalia: system architecture and technical design.
    - Anna: market/cost analysis and documentation/revision.
    - Jan: hardware and implementation analysis.
    - 30% / 40% / 30% approximate workload distribution.
    - Joint decision-making and document integration.
17. **AI-tool disclosure**
    - ChatGPT.
    - Microsoft Copilot.
    - Information gathering.
    - Concept clarification.
    - Content structuring.
    - Incorporation of professor feedback.
    - Generation of illustrative images/diagrams.
    - Explicit recognition of AI limitations.
    - Manual verification of technical information.
18. **References**
    - UAB IoT/LoRa infrastructure.
    - AWS IoT Core.
    - Microsoft Azure IoT Hub.
    - MQTT/AMQP sources.
    - Adafruit hardware.
    - Semtech LoRa documentation.
    - HC-SR04.
    - Battery/component sources.
    - Certification/legal sources.
19. **Appendix A — Communication-protocol comparison**
    - MQTT.
    - AMQP.
    - HTTP/HTTPS.
    - Architecture.
    - Command targets.
    - Transport protocol.
    - Security.
    - Observability.
    - Messaging mode.
    - Queuing.
    - Message overhead.
    - Message size.
    - Content type.
    - Topic matching.
    - Reliability.
    - Multiplexing.
    - Message attributes.
    - Object persistence.
20. **Appendix B — Project planning**
    - GANTT diagram.
    - Project timeline and dependencies.

---

 # TD2 — P1 vs. P2 vs. P3

 With P3 added, the three projects show a clear common methodology but increasingly different technical applications.

 | Structural element | P1 | P2 | **P3** |
| --- | --- | --- | --- |
| **Problem / use case** | Environmental acoustic monitoring | Portable security/alarm | **Smart parking** |
| **Primary sensing** | Acoustic | Acoustic + vibration + GNSS | **Ultrasonic occupancy** |
| **Connectivity** | LoRa/LPWAN + gateway | LTE-M | **LoRa/LoRaWAN + gateway** |
| **Architecture** | Device → Gateway → Cloud → UI | Device → Cloud → UI | **Device → Gateway → Cloud → UI** |
| **Edge processing** | Strong EdgeAI/TinyML | Local event processing | **Local occupancy detection** |
| **AI** | EdgeAI/TinyML | Primarily cloud AI | **Cloud prediction/forecasting** |
| **Cloud** | Strong | Strong | **Strong** |
| **Energy** | Battery + solar | Battery | **Low-power battery operation** |
| **Main technical challenge** | Distributed environmental sensing | Portable autonomous security | **Large-scale occupancy sensing** |
| **Communication emphasis** | LPWAN/network scalability | Cellular/LTE-M | **LoRaWAN and protocol selection** |
| **Security emphasis** | Present | Strong/CIA/GDPR | **Present but less central** |
| **Testing emphasis** | Network, energy, sensing | Battery, latency, sensors, security | **Deployment/scalability/communication/economic feasibility** |
| **Certification** | Present | Strong | **Present, particularly component/system compliance considerations** |
| **Manufacturing** | Included | Strong | **Included through device-cost analysis** |
| **Commercialization** | Included | Strong | **Included through deployment/business analysis** |
| **Cost analysis** | Detailed | Detailed | **Detailed** |
| **Break-even** | Included | Explicit | **Explicit: \~950 units** |
| **Project planning** | Roadmap/GANTT | GANTT/resource planning | **GANTT/dependencies** |
| **Team contributions** | Included | Included | **Included** |
| **AI disclosure** | Included | Included | **Included** |
| **Appendices** | Technical/planning material | KPIs, diagrams, planning/economics | **Protocol comparison + GANTT** |

## The common P1–P3 architecture

 At a high level, all three projects follow essentially the same engineering progression:

 > **Real-world problem → requirements → IoT architecture → sensing hardware → communication → data/cloud → intelligence → user interface → energy → economics → implementation/planning → conclusion**

 The technology inserted into that framework changes according to the application.

 ### P1

 > **Environmental sound → acoustic sensing → EdgeAI → LoRa → gateway → cloud → monitoring**

 P1 therefore places particular emphasis on **distributed sensing, EdgeAI, LPWAN and energy management**.

 ### P2

 > **Security event → acoustic/vibration sensing → embedded processing → LTE-M → cloud AI → alert/UI**

 P2 places more emphasis on **portable product design, cellular connectivity, autonomy, security, certification and commercialization**.

 ### P3

 > **Parking occupancy → ultrasonic sensing → LoRaWAN → gateway → cloud → prediction → parking UI**

 P3 places more emphasis on **large-scale deployment, low-cost sensing, LoRaWAN infrastructure, protocol selection, parking analytics and scalability**.

---

 # P1 vs. P2 vs. P3 — project maturity and engineering emphasis

 The three projects can also be distinguished by the type of engineering problem they emphasize.

 ### P1 — Distributed IoT / EdgeAI system

 The dominant question is:

 > How can many low-power environmental sensing nodes collect and classify data efficiently?

 Consequently, P1 emphasizes:

 - EdgeAI;
- distributed nodes;
- LPWAN;
- energy harvesting;
- gateway capacity;
- communication performance;
- scalable monitoring.

 ### P2 — Connected commercial security product

 The dominant question is:

 > How can a portable security device detect events autonomously and become a commercially deployable product?

 Consequently, P2 emphasizes:

 - portability;
- LTE-M;
- battery autonomy;
- security;
- certification;
- manufacturing;
- distribution;
- after-sales;
- commercialization.

 ### P3 — Scalable smart-infrastructure system

 The dominant question is:

 > How can parking occupancy be detected and communicated economically across a large campus deployment?

 Consequently, P3 emphasizes:

 - low-cost sensing;
- LoRaWAN;
- gateway infrastructure;
- large numbers of devices;
- multi-year autonomy;
- cloud analytics;
- prediction;
- deployment economics;
- break-even scaling.

 This makes P3 structurally closer to **large-scale IoT infrastructure deployment** than to a standalone connected product.

---

 # TD3 — P1, P2 and P3 against the project methodology

 Based on the project structure established in the P1/P2 analysis, P3 follows the same broad methodology.

 ## 1\. Problem definition

 All three begin with a concrete application rather than starting with a component or communication technology.

 | Project | Problem |
| --- | --- |
| P1 | Environmental acoustic monitoring |
| P2 | Portable security |
| P3 | Campus parking management |

P3 therefore fits the same **problem-driven engineering structure** as P1 and P2.

---

 ## 2\. Requirements and measurable objectives

 P3 translates the parking problem into technical requirements involving:

 - occupancy detection;
- real-time availability;
- communication latency;
- scalability;
- low-power operation;
- multi-year autonomy;
- cloud monitoring;
- prediction.

 Compared with P2, however, the supplied P3 material gives **less emphasis to highly explicit numerical system KPIs**. P2, for example, explicitly specifies targets such as latency, autonomy and AI accuracy.

 Therefore, structurally:

 > **P3 contains the requirements stage, but its requirements are less quantitatively developed in the material available here than P2's.**

---

 ## 3\. Architecture

 P3 clearly fulfills the IoT architecture requirement.

 Its architecture is effectively:

 > **Parking sensor → LoRa/LoRaWAN → Gateway → Cloud → Mobile/Web application**

 This is consistent with the IoT architecture already established in P1.

 The difference is that P3's gateway is especially important because the project is intended to support **large numbers of parking-space devices**.

---

 ## 4\. Hardware

 P3 includes concrete hardware choices rather than leaving the sensing layer abstract:

 - HC-SR04 ultrasonic sensor;
- Feather M0 + RFM95 LoRa;
- Semtech SX127x technology;
- lithium battery;
- enclosure;
- PCB/materials.

 This is consistent with the hardware-design approach used in P1 and P2.

---

 ## 5\. Communication

 This is one of P3's strongest structural components.

 P3 does not merely state that it uses LoRaWAN. It also includes an appendix comparing:

 - MQTT;
- AMQP;
- HTTP/HTTPS.

 The comparison covers architecture, transport, security, messaging, queuing, overhead, reliability, multiplexing and other characteristics.

 This demonstrates that the communication architecture is treated as an **engineering design decision**, rather than simply naming a technology.

---

 ## 6\. AI

 P3 includes an AI prediction component.

 Its purpose differs from both previous projects:

 - **P1:** AI helps classify environmental acoustic events at/near the edge.
- **P2:** AI classifies security-related acoustic events in the cloud.
- **P3:** AI is used for **parking-availability forecasting**.

 Thus, P3 demonstrates another legitimate position for AI in an IoT architecture: **using accumulated cloud data for predictive analytics rather than primarily for instantaneous event classification**.

---

 ## 7\. Cloud and applications

 P3 includes:

 > **sensing → communication → cloud → analytics → mobile/web interface**

 This satisfies the broader IoT requirement that sensor information ultimately become useful information for users or managers.

 The P3 conclusion specifically identifies real-time availability and long-term monitoring/analytics as system capabilities.

---

 ## 8\. Energy

 P3 explicitly addresses low-power operation and multi-year autonomy.

 This is important because a 5,000-space parking deployment would make frequent battery replacement operationally significant.

 The structure therefore connects:

 > **device power consumption → maintenance requirements → deployment scalability → economic feasibility**

 That connection is particularly appropriate for a large IoT deployment.

---

 ## 9\. Scalability

 Scalability is arguably one of the defining elements of P3.

 The document explicitly discusses:

 - 5,000-device deployment;
- existing LoRaWAN infrastructure;
- dedicated gateway installation;
- installation-cost amortization;
- smaller versus larger deployments;
- break-even at approximately 950 units.

 This gives P3 a strong connection between **technical architecture and economic scale**.

---

 ## 10\. Economic analysis

 P3 includes the important economic components expected in a complete engineering project:

 - device cost;
- installation cost;
- amortization;
- deployment scale;
- per-device pricing;
- break-even;
- profitability after break-even.

 The supplied calculation shows:

 > Installation cost: **€3,100–€4,700**

 For 5,000 devices:

 > **€0.62–€0.94 per device**

 With a base device price of €93:

 > **€93.62–€93.94 per device including installation amortization**

 The project then identifies approximately **950 units as the break-even point**.

 This is structurally comparable to P2's explicit unit economics and break-even analysis, although the exact financial model differs.

---

 ## 11\. Project planning

 P3 contains a GANTT diagram showing:

 > **project timeline + task dependencies**

 This means that, like P1 and P2, the report does not stop at technical design. It also addresses the **implementation process**.

---

 ## 12\. Conclusion and future development

 P3 concludes by connecting technical, economic and societal objectives:

 - practical deployment;
- scalability;
- cost-effectiveness;
- reduced parking-search time;
- reduced congestion;
- sustainable mobility.

 It also proposes future extensions:

 - real-world pilots;
- richer prediction data;
- navigation guidance;
- reservation;
- dynamic pricing.

 This is consistent with the broader project methodology of moving from the proposed system toward possible real-world deployment.

---

 # P1 vs. P2 vs. P3 — compliance matrix

 Using the **project methodology inferred from the earlier P1/P2 analysis**, rather than claiming this is the official university rubric, the three projects can be summarized as follows:

 | Requirement / project component | P1 | P2 | P3 |
| --- | --- | --- | --- |
| Concrete real-world problem | ✓ | ✓ | ✓ |
| System objectives | ✓ | ✓ | ✓ |
| Quantitative requirements/KPIs | ✓ | ✓ | △ |
| IoT architecture | ✓ | ✓ | ✓ |
| Hardware selection | ✓ | ✓ | ✓ |
| Embedded/software design | ✓ | ✓ | ✓ |
| Communication architecture | ✓ | ✓ | ✓ |
| AI component | ✓ | ✓ | ✓ |
| Cloud/backend | ✓ | ✓ | ✓ |
| User interface | ✓ | ✓ | ✓ |
| Energy analysis | ✓ | ✓ | ✓ |
| Scalability analysis | ✓ | ✓ | ✓ |
| Testing/validation | ✓ | ✓ | △ |
| Security/privacy | ✓ | ✓ | △ |
| Certification/compliance | ✓ | ✓ | ✓/△ |
| Economic analysis | ✓ | ✓ | ✓ |
| Break-even analysis | ✓ | ✓ | ✓ |
| Commercialization/deployment | ✓ | ✓ | ✓ |
| Project planning/GANTT | ✓ | ✓ | ✓ |
| Team contributions | ✓ | ✓ | ✓ |
| AI-use disclosure | ✓ | ✓ | ✓ |
| References | ✓ | ✓ | ✓ |
| Appendices | ✓ | ✓ | ✓ |

**Interpretation:**

 - ✓ = clearly represented in the material analyzed
- △ = present but less developed/less explicit in the material available
- ✓/△ = present, but the completeness of the specific compliance evidence would require checking the earlier P3 chunks and/or the actual official rubric

---

 # Overall P1–P3 evolution

 The three projects show a fairly coherent evolution of the same project methodology:

 ### P1 — IoT sensing and EdgeAI

 > **Sense → classify locally → communicate → monitor**

 The main engineering concerns are **distributed sensing, EdgeAI, LPWAN and energy**.

 ### P2 — IoT productization

 > **Sense → detect → communicate → analyze → alert → commercialize**

 The main concerns become **portability, cellular connectivity, security, certification, manufacturing and commercialization**.

 ### P3 — IoT infrastructure at scale

 > **Sense occupancy → communicate through LoRaWAN → analyze → predict → deploy at scale**

 The main concerns become **large-scale deployment, low unit cost, gateway infrastructure, scalability and economic break-even**.

 Therefore, structurally, the three projects can be represented as:

 > **P1: IoT system engineering**\
>  ↓\
>  **P2: IoT product engineering and commercialization**\
>  ↓\
>  **P3: IoT infrastructure and scalable deployment**

 The important conclusion for the overall TD1–TD3 task is that **P3 does not represent a completely different report structure from P1 and P2**. It follows the same fundamental engineering-project template, but changes the technical and business emphasis to fit smart-campus parking.

 The strongest common structure across all three is:

 > **Problem → Requirements → Architecture → Hardware → Software → Communication → AI/Data → Cloud/UI → Energy → Validation → Economics → Deployment/Planning → Conclusion → Contributions/AI → References → Appendices**

 And the main P3-specific contribution to that structure is the strong connection between **LoRaWAN-based mass deployment, low-cost devices, installation amortization, prediction, and break-even scaling**.
