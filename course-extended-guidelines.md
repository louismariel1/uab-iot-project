 ## 1\. Course purpose

 The course teaches the **full IoT value chain**, from physical devices through edge/mobile computing to cloud services and user interfaces.

 The central idea is:

 **Device → Communication → Edge/Mobile → Cloud → AI → User interface**

 Students learn the concepts, metrics, technologies and platforms needed to build this complete chain, with particular attention to:

 - Connected devices operating autonomously.
- Sensors and data collection.
- Energy efficiency and battery constraints.
- Embedded systems and SoCs.
- Wired and wireless communications.
- Mobile/edge platforms.
- Cloud storage and processing.
- AI distributed across the IoT chain.
- Real-world IoT applications.

 The course is explicitly oriented toward the skills expected of **full-stack IoT developers**.

---

 ## 2\. The course is strongly project-based

 The main learning mechanism is not just lectures. Students work in groups on an **original end-to-end IoT project**.

 The project combines:

 - Technical design.
- Market/problem analysis.
- Hardware selection.
- Communication architecture.
- Performance and energy considerations.
- AI/EdgeAI.
- Cloud architecture.
- Business model.
- Cost and total cost of ownership.
- Development planning.
- A working **Proof of Concept (PoC)**.

 The project is developed incrementally throughout the semester rather than being left until the end.

---

 ## 3\. The IoT technical architecture you are expected to understand

 The course divides an IoT solution roughly into four levels:

 | Level | Main focus |
| --- | --- |
| **Device** | Sensors, MCU/SoC, Bluetooth, embedded programming |
| **Edge/Mobile** | Smartphone/mobile application, local processing, communication |
| **Cloud** | Backend, databases, APIs, processing and AI |
| **User** | Front-end/interface and presentation of information |

A major theme is that **each level has different resource constraints, programming models and communication technologies**.

 Energy efficiency is especially important at the device/edge level.

 The course also distinguishes traditional/cloud AI from **EdgeAI**, where AI processing can occur on resource-constrained edge or device platforms.

---

 # 4\. Lecture topics

 The scheduled lectures build the project knowledge progressively.

 ### September

 1. **Introduction**
   - IoT concepts and methods.
   - Course/project overview.
2. **SoCs and sensors**
   - How to select chips and sensors for an IoT device.
3. **Connecting chips**
   - Communication between components within the device.
4. **IoT system restrictions**
   - Functional requirements.
   - Performance constraints.
5. **Energy consumption**
   - Energy requirements.
   - Battery selection.

 ### October–November

 6. **Communication protocols**
   - Choosing an appropriate protocol for the device.
7. **Wired vs. wireless communication**
   - Comparing communication alternatives.
8. **Wireless network selection**
   - WBAN
   - WPAN
   - WLAN
   - LPWAN
9. **Embedded platforms**
   - Choosing the appropriate "heart" of the hardware.
10. **Mobile platforms and wearables**

 - Designing IoT systems involving mobile devices and wearable platforms.

 ### December

 11. **Cloud backend and frontend**

 - Managing IoT data in the cloud.
- Backend/frontend architecture.

 The course therefore progresses logically from **hardware → communications → embedded/edge → mobile → cloud**.

---

 # 5\. The design project

 The design project has **six stages**:

 ### P1 — Idea and market research

 Develop an original IoT idea and investigate the market/problem.

 ### P2 — Requirements

 Define:

 - Functional requirements.
- Performance requirements.
- System specifications.

 ### P3 — Architecture

 Design:

 - IoT system blocks.
- Communication architecture.
- Alternative implementation approaches.

 There is also a **partial defence/examination** associated with this stage.

 ### P4 — Implementation planning

 Choose:

 - Components.
- Hardware platforms.
- Software platforms.

 Then estimate expected performance.

 ### P5 — AI and EdgeAI

 Determine how AI can be incorporated into the system, including **EdgeAI**.

 ### P6 — Business and cost

 Develop:

 - Business model.
- Development plan.
- Total cost of ownership.

 This is important: the project isn't merely "build a gadget." You are expected to justify **why the system should be built, how it should be engineered, and whether it makes practical/business sense**.

---

 # 6\. Laboratory / Proof of Concept

 The laboratory turns the design into a working prototype.

 The intended chain is:

 **MCU + sensors → Bluetooth → Android app → processing/JSON → cloud backend → frontend**

 The labs cover:

 ### L1 — MCU/BLE programming

 Introduction to programming the MCU-Bluetooth SoC using the Thingy platform.

 ### L2 — Device implementation

 C++ implementation involving:

 - Sensors.
- MCU.
- Bluetooth.

 ### L3 — Android I

 Build an Android application for:

 - Data acquisition.
- BLE communication.

 ### L4 — Android II

 Extend the application for:

 - Local computation.
- JSON.
- Server connection.

 ### L5 — Cloud

 Implement:

 - Cloud backend.
- Frontend.

 So the practical objective is to demonstrate a **complete working IoT pipeline**, rather than a disconnected hardware or software exercise.

---

 # 7\. Project team structure

 The document specifies groups of approximately **3 students**, with interdisciplinary participation encouraged.

 The stated structure includes combinations of:

 - Computer Engineering students.
- Computational Mathematics/Data Analytics students.
- Data Engineering students.
- Erasmus/exchange students.

 The overall course capacity is listed as **49 students**, organized into approximately **15 groups of three and one group of four**.

 Design and laboratory sessions alternate between groups **A and B**.

---

 # 8\. You can choose your own project — or use an external challenge

 There are two routes.

 ### Option A — Your own project

 Your group develops its own IoT idea after discussing it with the tutors.

 ### Option B — Third-party challenge

 A limited number of groups can choose from externally supplied challenges.

 The document gives examples involving:

 - **NeumaCare** — IoT for wellbeing in domestic/hospital environments.
- **Molins de Rei** — IoT/AI/sensors for reducing and monitoring outdoor noise.
- **UbraHealth** — secure wearable → mobile → cloud health-data architecture.

 The third-party projects therefore expose students to **real-world constraints**, rather than purely academic examples.

---

 # 9\. Examples of previous projects

 The previous projects illustrate the expected range:

 | Project | Domain | Device | Edge | Cloud |
| --- | --- | --- | --- | --- |
| SmartHeadPhone | eHealth | HR + GPS | Phone | AWS |
| ChessBoard | Gaming | SoC/BLE + NFC | Phone | AWS |
| ClassMonitor | eHealth | Sensors | Raspberry Pi 4 | Google |
| EcoSmart | eHealth | Camera + sensors | Raspberry Pi 5 | Google |
| MoodAware | eHealth | Sensors | Raspberry Pi 4 | AWS |
| SomnoSense | eHealth | Sensors | Router | Google |
| Smart Parking | Social/smart-city | Ultrasonic | LoRa gateway | AWS |

The important lesson is that **the technology is selected according to the problem**, rather than every project being required to use the same architecture.

---

 # 10\. Invited talks

 The course also includes invited speakers covering areas such as:

 - **Energy measurement for AI on edge platforms.**
- **IoT applications in food and health.**
- **Smart sensors and IoT.**

 The exact dates are announced through the virtual campus.

---

 # 11\. Attendance and course methodology

 The methodology combines:

 - Lectures/master classes.
- Tutored sessions.
- Project-based learning.
- Laboratory work.
- Use cases.
- Debates.
- Collaborative activities.

 ### Important rule

 **Attendance is mandatory for all face-to-face activities.**

 The UAB virtual campus is used for:

 - Course materials.
- Links.
- Exercises.
- Activities.
- Student submissions.
- Course communication.

---

 # 12\. Workload

 The course workload is approximately:

 | Activity | Hours | ECTS |
| --- | --- | --- |
| Lectures/seminars | 30 | 1.2 |
| Supervised labs/exercises | 28 | 1.12 |
| Independent study/homework | 90 | 3.6 |
| **Total** | **148** | **≈6 ECTS** |

The biggest component is therefore **independent work**. The course expects students to continue developing and documenting their project outside scheduled classroom/lab hours.

---

 # 13\. Assessment

 The grading structure is:

 | Component | Weight |
| --- | --- |
| **Laboratories / supervised activities** | **40%** |
| **Individual exercises/activities** | **20%** |
| **Design project report \+ defence** | **40%** |
| **Total** | **100%** |

This means **80% of the grade is tied to practical/project work**.

 There is consequently a strong incentive to keep up with the project throughout the semester rather than relying on a final exam.

---

 # 14\. Passing requirements

 The document states that a final weighted average of **at least 50%** is normally sufficient **provided that the student achieves more than one-third of the available marks in each of the four underlying marks/components**.

 If that minimum condition is not met, the final mark is capped at **4.0**.

 The four-mark requirement is important because simply getting a good overall weighted average is not enough if one component is extremely weak.

---

 # 15\. AI policy

 The course explicitly permits AI, but only as a **support tool**.

 ### Permitted

 AI may be used for things such as:

 - Writing assistance.
- Reviewing text.
- Debugging.
- Finding/understanding code errors.

 ### Mandatory

 Whenever AI is used, students must **declare its use** and explain:

 - **When** it was used.
- **What specific task** it was used for.

 ### Prohibited

 Students may **not use AI to generate an entire assignment or perform the assignment for them**.

 So the intended model is:

 > **AI assists your work; it does not replace your work.**

---

 # 16\. Plagiarism

 The policy is strict:

 - Plagiarism is not tolerated.
- Students involved in a plagiarism activity are automatically failed.
- The document states that the final mark will be **no higher than 30%**.

 This is particularly relevant to the project because groups will inevitably use external libraries, examples, documentation and potentially AI-generated material. Those sources need to be properly handled and acknowledged.

---

 # 17\. Special external-challenge requirements

 The Molins de Rei/organized external challenge has additional requirements, including:

 - Interdisciplinary teams.
- Specific training/ideation sessions.
- Deliverables during the semester.
- A final pitch.
- A public presentation event.

 The document says participating UAB students receive **3 RAC credits**, and that the winning team receives a **€3,000 prize**.

 These conditions apply to the organized external challenge, **not to the ordinary course project generally**.

---

 # 18\. Key dates from the document

 For the **2026/27 schedule shown in your document**, the important milestones are:

 | Date | Event |
| --- | --- |
| **7 Sep 2026** | Course introduction |
| **14 Sep** | SoCs & sensors |
| **21 Sep** | Chip/device connectivity |
| **28 Sep** | IoT restrictions |
| **5 Oct** | Energy/battery considerations |
| **26 Oct** | Partial defence |
| **9 Nov** | Wired/wireless communication |
| **16 Nov** | WBAN/WPAN/WLAN/LPWAN |
| **23 Nov** | Embedded platforms |
| **30 Nov** | Mobile/wearables |
| **14 Dec** | Cloud backend/frontend |
| **7 Jan 2027** | Final lab defence |
| **19 Jan 2027** | Final design defence |

The project itself progresses from **P1 in September through P6 in December**, with the final design and lab defences in January.

---

 # 19\. What the course is really asking you to accomplish

 In practical terms, the course wants every team to answer this sequence of questions:

 **1\. What problem are we solving?**\
 ↓\
 **2\. Is there a real use case/market for it?**\
 ↓\
 **3\. What should the IoT system do?**\
 ↓\
 **4\. What sensors/SoC/MCU do we need?**\
 ↓\
 **5\. How will the devices communicate?**\
 ↓\
 **6\. Where should computation happen — device, edge or cloud?**\
 ↓\
 **7\. Can AI/EdgeAI improve it?**\
 ↓\
 **8\. How much energy will it consume?**\
 ↓\
 **9\. How does the mobile/edge application work?**\
 ↓\
 **10\. How is data transferred to and processed in the cloud?**\
 ↓\
 **11\. How does the user interact with the result?**\
 ↓\
 **12\. What does the prototype cost and how would it be deployed?**\
 ↓\
 **13\. Can we demonstrate the complete system working?**

 ### In one sentence

 **This is essentially an end-to-end IoT engineering course where you design, justify, prototype and defend a real IoT system spanning embedded hardware, communications, mobile/edge computing, cloud and AI—with energy, performance, cost and practical deployment considered throughout.**

 One particularly important takeaway from these guidelines is that **the project and lab are not separate assignments**: they are two sides of the same system. The **design project specifies and justifies the IoT solution**, while the **lab implements a PoC of that same solution**.
