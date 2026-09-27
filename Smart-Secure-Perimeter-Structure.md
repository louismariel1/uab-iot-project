 # Final SSP IoT Design Project Structure

 **Project principle:** the report describes the **complete real-world IoT solution as if we are the IoT/AI engineering consultancy designing it with adequate resources**. The laboratory PoC is a separate implementation exercise and should not constrain or redefine the proposed real-world design.

 | # | Chapter | Main purpose | Official course alignment |
| --- | --- | --- | --- |
| **1** | **Problem / Use Case** | Define the real-world problem, why it matters, and the proposed IoT solution | Original IoT project; real problem/use case |
| **2** | **Target Users & Stakeholders** | Identify users, customers, operators, organizations and other stakeholders | Use-case methodology; market/business analysis |
| **3** | **Requirements** | Establish functional, technical and measurable performance requirements | **P2** – Functional & performance specifications |
| **4** | **Market / Context Analysis** | Analyze existing solutions, alternatives, competitors, gaps and context | **P1** – Preliminary market research |
| **5** | **IoT Architecture** | Define the complete Device → Edge/Mobile → Cloud → User system | **P3** – IoT system block & communications architecture |
| **6** | **Hardware** | Select and justify sensors, MCU/SoC, actuators, interfaces, power and battery | SoC/sensors; **P4** – component/platform selection |
| **7** | **Communication** | Select and justify communication technologies and network architecture | Communication lectures; **P3/P4** |
| **8** | **Software** | Define embedded software, mobile application, backend, APIs and frontend | **L1–L5** |
| **9** | **Data Flow** | Describe what data is generated, processed, transmitted, stored and consumed | Full IoT chain; backend/frontend |
| **10** | **AI / EdgeAI** | Define AI functionality, models, inputs/outputs and where intelligence runs | **P5** – AI & Edge AI |
| **11** | **Energy / Performance** | Quantify latency, throughput, memory, computation, duty cycle, energy and battery requirements | **P2/P4**; energy/performance restrictions |
| **12** | **Cloud Architecture** | Specify backend, APIs, databases, authentication, storage, processing and user services | **L5**; cloud/backend/frontend |
| **13** | **PoC** | Define how the proposed system would be demonstrated and what functionality must be proven | Explicit course **PoC requirement** |
| **14** | **Business / Costs / Scalability** | Establish business model, BOM, development/OPEX costs, TCO and scaling strategy | **P6** – business model, development plan & TCO |
| **15** | **Testing & Validation** | Define experiments, metrics, acceptance criteria and validation methodology | PoC + performance requirements |
| **16** | **Reports / Presentations / Defence** | Organize the engineering documentation and defence material | 40% report & defence; partial/final defence |
| **17** | **Completeness / Critical Assessment** | Assess limitations, assumptions, risks, unresolved issues and future improvements | Incremental design documentation \+ defence |

---

 ## 1\. Problem / Use Case

 ### 1.1 Problem statement

 ### 1.2 Real-world context

 ### 1.3 Pain points and unmet needs

 ### 1.4 Proposed IoT solution

 ### 1.5 Main use cases

 ### 1.6 Operational scenarios

 ### 1.7 Project objectives

 ### 1.8 Scope and boundaries

 **Output:** a precise definition of _what problem SSP solves and why an IoT system is appropriate_.

---

 ## 2\. Target Users & Stakeholders

 ### 2.1 Primary users

 ### 2.2 Secondary users

 ### 2.3 Customers / buyers

 ### 2.4 Operators / administrators

 ### 2.5 Technical stakeholders

 ### 2.6 Regulatory and institutional stakeholders

 ### 2.7 User personas

 ### 2.8 Stakeholder needs and responsibilities

 ### 2.9 Adoption environment

 **Output:** a clear understanding of _who interacts with, benefits from, operates, pays for or regulates SSP_.

---

 ## 3. Requirements

 ### 3.1 Functional requirements

 ### 3.2 Non-functional requirements

 ### 3.3 Performance requirements

 ### 3.4 Safety requirements

 ### 3.5 Security and privacy requirements

 ### 3.6 Usability requirements

 ### 3.7 Reliability and availability requirements

 ### 3.8 Environmental requirements

 ### 3.9 Scalability requirements

 ### 3.10 Requirements traceability matrix

 Each important requirement should ideally be **measurable**.

 For example:

 > The system shall detect an abnormal ankle event within ≤ X seconds and generate an alert with ≥ Y% detection sensitivity under defined conditions.

 This chapter becomes the reference against which Chapters 11 and 15 evaluate the design.

---

 # 4\. Market / Context Analysis

 ### 4.1 Market/context overview

 ### 4.2 Existing solutions

 ### 4.3 Competitor analysis

 ### 4.4 Technological alternatives

 ### 4.5 Current limitations

 ### 4.6 Regulatory environment

 ### 4.7 Privacy/security considerations

 ### 4.8 Market gap

 ### 4.9 SSP differentiation

 ### 4.10 Design implications

 **Important:** this is not simply a list of competitors. We use the analysis to establish **why our proposed architecture and requirements make sense**.

---

 # 5\. IoT Architecture

 This is the central architectural chapter.

 ### 5.1 Overall system architecture

 ### 5.2 Device layer

 ### 5.3 Edge / Mobile layer

 ### 5.4 Cloud layer

 ### 5.5 User/interface layer

 ### 5.6 Inter-layer communication

 ### 5.7 System block diagram

 ### 5.8 Functional decomposition

 ### 5.9 Deployment architecture

 ### 5.10 Security boundaries

 The primary conceptual chain should remain:

 **Device → Edge/Mobile → Cloud → User**

 with appropriate feedback/control paths where necessary.

---

 # 6\. Hardware

 ### 6.1 Hardware architecture

 ### 6.2 Sensors

 ### 6.3 MCU / SoC

 ### 6.4 Actuators

 ### 6.5 Memory

 ### 6.6 Connectivity hardware

 ### 6.7 Power-management circuitry

 ### 6.8 Battery

 ### 6.9 Physical enclosure/form factor

 ### 6.10 Hardware interfaces

 ### 6.11 Component alternatives

 ### 6.12 Component selection justification

 ### 6.13 Estimated BOM

 This is where we answer the course question:

 > **Why did we choose these particular chips, sensors and components?**

---

 # 7\. Communication

 ### 7.1 Communication requirements

 ### 7.2 Device-level communication

 ### 7.3 Device → Edge communication

 ### 7.4 Edge → Cloud communication

 ### 7.5 Cloud → User communication

 ### 7.6 BLE / Wi-Fi / cellular / LoRa / other candidates

 ### 7.7 WBAN / WPAN / WLAN / LPWAN considerations

 ### 7.8 Protocol comparison

 ### 7.9 Selected communication architecture

 ### 7.10 Security

 ### 7.11 Communication failure modes

 The selection must be justified using **range, bandwidth, latency, energy consumption, infrastructure, cost and reliability**, rather than simply saying that a technology is popular.

---

 # 8\. Software

 ### 8.1 Embedded software

 ### 8.2 Sensor acquisition

 ### 8.3 Device control logic

 ### 8.4 BLE communication

 ### 8.5 Mobile/Edge application

 ### 8.6 Backend services

 ### 8.7 APIs

 ### 8.8 Database software

 ### 8.9 Frontend/dashboard

 ### 8.10 Authentication and authorization

 ### 8.11 Software architecture

 ### 8.12 Software technology selection

 This corresponds strongly to **L1–L5**.

---

 # 9\. Data Flow

 ### 9.1 Data sources

 ### 9.2 Raw sensor data

 ### 9.3 Device-level processing

 ### 9.4 Edge/mobile processing

 ### 9.5 Cloud processing

 ### 9.6 AI-generated data

 ### 9.7 Alerts/events

 ### 9.8 Data transmission

 ### 9.9 Data storage

 ### 9.10 Data visualization

 ### 9.11 Data lifecycle

 ### 9.12 Data privacy

 We should explicitly distinguish:

 **generated → acquired → processed → transmitted → stored → analyzed → presented → acted upon**

---

 # 10\. AI / EdgeAI

 ### 10.1 AI problem definition

 ### 10.2 Why AI is required

 ### 10.3 Inputs/features

 ### 10.4 AI outputs

 ### 10.5 Candidate algorithms/models

 ### 10.6 Training data

 ### 10.7 Model training

 ### 10.8 Cloud AI

 ### 10.9 Edge AI

 ### 10.10 Device AI

 ### 10.11 Model deployment

 ### 10.12 Accuracy/performance requirements

 ### 10.13 AI resource requirements

 ### 10.14 Privacy implications

 ### 10.15 AI failure modes

 We should not add AI merely because the course mentions AI. If SSP genuinely benefits from AI, we demonstrate **where it creates measurable value** and why that processing location was selected.

---

 # 11\. Energy / Performance

 ### 11.1 Performance requirements

 ### 11.2 Latency budget

 ### 11.3 Sampling requirements

 ### 11.4 Processing requirements

 ### 11.5 Memory requirements

 ### 11.6 Communication energy

 ### 11.7 Processing energy

 ### 11.8 Sensor energy

 ### 11.9 Sleep/duty-cycle strategy

 ### 11.10 Battery capacity

 ### 11.11 Estimated battery life

 ### 11.12 Thermal considerations

 ### 11.13 Performance bottlenecks

 ### 11.14 Optimization strategy

 This chapter is particularly important because the course explicitly emphasizes **resource-constrained platforms and energy-efficient autonomous devices**.

---

 # 12\. Cloud Architecture

 ### 12.1 Cloud requirements

 ### 12.2 Cloud deployment model

 ### 12.3 API architecture

 ### 12.4 Backend services

 ### 12.5 Database

 ### 12.6 Data storage

 ### 12.7 Event processing

 ### 12.8 AI/cloud processing

 ### 12.9 Authentication

 ### 12.10 Authorization

 ### 12.11 Security

 ### 12.12 Monitoring

 ### 12.13 Backup/recovery

 ### 12.14 Scalability

 ### 12.15 Estimated cloud costs

---

 # 13\. PoC

 This chapter needs a particularly clear distinction.

 ## **Design Project vs Laboratory PoC**

 The **design project** specifies the complete real-world SSP system.

 The **laboratory PoC** is a practical demonstration of the concept using the hardware/software resources available in the course laboratory.

 Therefore:

 > **The laboratory implementation is not the definition of the final SSP product.**

 For example, if the real SSP solution requires a specialized ankle-monitor device, the design can specify that device in Chapter 6. The laboratory PoC could instead use a **generic MCU/SoC \+ BLE + Android phone** to simulate the relevant sensing and alert workflow.

 ### 13.1 PoC objectives

 ### 13.2 Functions to demonstrate

 ### 13.3 PoC architecture

 ### 13.4 Hardware substitution strategy

 ### 13.5 Device implementation

 ### 13.6 BLE communication

 ### 13.7 Mobile/Edge implementation

 ### 13.8 Cloud integration

 ### 13.9 Demonstration scenario

 ### 13.10 PoC limitations

 ### 13.11 Mapping between real system and laboratory implementation

 This chapter therefore demonstrates:

 **"Can the fundamental IoT concept work?"**

 rather than:

 **"Can we build the complete commercial SSP product in the laboratory?"**

---

 # 14\. Business / Costs / Scalability

 ### 14.1 Value proposition

 ### 14.2 Business model

 ### 14.3 Customer model

 ### 14.4 Revenue model

 ### 14.5 Hardware BOM

 ### 14.6 Manufacturing cost

 ### 14.7 Development cost

 ### 14.8 Cloud/operational cost

 ### 14.9 Maintenance cost

 ### 14.10 Total Cost of Ownership

 ### 14.11 Pricing assumptions

 ### 14.12 Production volumes

 ### 14.13 Scalability

 ### 14.14 Deployment strategy

 ### 14.15 Development roadmap

 This directly addresses **P6**.

---

 # 15\. Testing & Validation

 ### 15.1 Validation strategy

 ### 15.2 Functional tests

 ### 15.3 Sensor tests

 ### 15.4 Communication tests

 ### 15.5 AI tests

 ### 15.6 Performance tests

 ### 15.7 Energy tests

 ### 15.8 Reliability tests

 ### 15.9 Security tests

 ### 15.10 Usability tests

 ### 15.11 Acceptance criteria

 ### 15.12 Expected/actual results

 ### 15.13 Requirements traceability

 ### 15.14 Failure analysis

 The key relationship should be:

 **Requirement → Metric → Test → Result → Pass/Fail**

---

 # 16\. Reports / Presentations / Defence

 ### 16.1 Design report structure

 ### 16.2 Executive summary

 ### 16.3 Technical diagrams

 ### 16.4 Architecture diagrams

 ### 16.5 Data-flow diagrams

 ### 16.6 Tables and design decisions

 ### 16.7 Partial defence

 ### 16.8 Final defence

 ### 16.9 PoC demonstration

 ### 16.10 Presentation structure

 ### 16.11 Anticipated defence questions

 ### 16.12 Evidence supporting design decisions

 This chapter is not merely administrative. It ensures that the engineering work is **communicated and defended as a coherent professional design**.

---

 # 17\. Completeness / Critical Assessment

 ### 17.1 What the design achieves

 ### 17.2 Requirements coverage

 ### 17.3 Technical assumptions

 ### 17.4 Known limitations

 ### 17.5 Technical risks

 ### 17.6 Business risks

 ### 17.7 Security/privacy risks

 ### 17.8 AI limitations

 ### 17.9 PoC limitations

 ### 17.10 Remaining engineering work

 ### 17.11 Future improvements

 ### 17.12 Product-development roadmap

 ### 17.13 Final system assessment

 The purpose is to demonstrate that we understand not only **how SSP could work**, but also **what remains uncertain or would have to be solved before real deployment**.

---

 # Official-course traceability

 The most important thing is that the 17 chapters collectively cover **every explicit project-design activity** in the course:

 | Official activity | SSP chapter(s) |
| --- | --- |
| **P1. Original idea + preliminary market research** | **1, 2, 4** |
| **P2. Functional & performance specifications** | **3, 11** |
| **P3. IoT system block + communications architecture** | **5, 7** |
| **P4. Component/platform selection + performance estimation** | **6, 7, 8, 11** |
| **P5. AI & Edge AI** | **10** |
| **P6. Business model + development plan + TCO** | **14** |
| **L1. MCU-BLE SoC programming** | **6, 7, 8, 13** |
| **L2. Sensor + MCU + Bluetooth** | **6, 7, 8, 13** |
| **L3. Android + BLE data acquisition** | **8, 9, 13** |
| **L4. Android + JSON/server connection** | **8, 9, 12, 13** |
| **L5. Cloud backend + frontend** | **8, 12, 13** |
| **IoT full-stack chain** | **5–13** |
| **Energy-efficient autonomous devices** | **6, 7, 10, 11** |
| **Cloud storage/processing** | **9, 10, 12** |
| **AI distributed along chain** | **10, with implications in 5, 9, 11** |
| **PoC of same idea** | **13** |
| **Design documentation** | **1–17** |
| **Business, costs and scalability** | **14** |
| **Report and defence** | **16–17** |

## The frozen architecture

 That separation should prevent us from accidentally designing the _report around the laboratory hardware_ instead of designing the **actual IoT solution**.

 We can later expand these 17 chapters into the **24-chapter version** purely for finer documentation granularity. The 24 chapters would therefore be a _subdivision of this frozen structure_, not a new project structure.
