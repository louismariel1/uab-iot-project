## UAB 105075 — Internet of Things (2026/2027)

 ### Topic 1 — IoT architecture and virtualization

 Students start with the overall IoT architecture:

 - Device, edge, cloud and UI.
- IoT value chain.
- AI and IoT.
- How the different layers interact.

 The goal is to understand the complete system rather than isolated IoT components.  UAB Apps

 ### Topic 2 — Selecting IoT chips and sensors

 This covers the physical/device layer:

 - Processors.
- Sensors.
- Actuators.
- Batteries.
- SoCs.
- Component selection.
- Cost.
- Real-time requirements, including latency and throughput.
- Energy efficiency.
- Datasheets and example circuits.
- On-board protocols.
- Nordic Thingy as an example/use case.  UAB Apps

 A key theme is that hardware selection is treated as an **engineering trade-off** among cost, performance/latency and energy consumption.

 ### Topic 3 — Wireless device-to-edge communication

 The communications portion covers:

 - **WBAN** — Wireless Body Area Networks.
- **WPAN** — Wireless Personal Area Networks.
- **WLAN** — Wireless Local Area Networks.
- **LPWAN** — Low-Power Wide-Area Networks.
- Data formats and protocols.
- **Bluetooth / Bluetooth Low Energy (BLE)**.  UAB Apps

 BLE is particularly important because it appears directly in the practical prototype chain.

 ### Topic 4 — Edge platforms and EdgeAI

 Students examine edge-computing choices:

 - Edge platforms with or without an **OS/RTOS**.
- **EdgeAI**, including training and deployment.
- Arduino UNO Q as an example/use case.  UAB Apps

 This is one of the significant 2026/27 changes compared with the previous course guide.

 ### Topic 5 — Virtualization

 The virtualization component covers:

 - Containers.
- Databases.
- Virtual machines.  UAB Apps

---

 ## 3\. The major practical component: an original IoT project

 The course is strongly **project-based**. UAB says the lectures are closely linked to the project and laboratories so that the theory supplies the knowledge needed for actual design and implementation decisions.  UAB Apps

 The guided project has six stages:

 1. **P1 — Idea:** develop an original IoT-system idea and conduct a preliminary market study.
2. **P2 — Requirements:** define functional and performance specifications.
3. **P3 — Architecture:** design the block and communications architecture and consider implementation alternatives.
4. **P4 — Implementation:** select components/platforms and implement the system.
5. **P5 — Planning/business:** estimate schedule, costs and business model.
6. **P6 — Deliverable:** document, present and defend the project.  UAB Apps

 Students can select a project in three ways:

 - Develop their own idea with the group.
- Select a challenge proposed by the teaching staff.
- Select an external challenge.

 For 2026/27, the guide specifically mentions challenges from **Molins de Rei Town Council**, via the UAB Research Park (PRUAB). That particular option involves **6–8 hours of entrepreneurship training** and a public presentation scheduled for **December 11, 2026**; the guide says participants can receive 3 elective credits and be eligible for a prize.  UAB Apps

---

 ## 4\. Laboratory: building the complete IoT chain

 The laboratory is a **six-session, self-paced team project** in which students progressively build an entire IoT system.  UAB Apps

 The chain is essentially:

 **Sensor/MCU → BLE → Edge → JSON/network → Cloud → AI/processing → UI**

 Specifically:

 - **Device:** program the MCU and sensors to capture physical variables.
- **Edge:** transfer data via BLE to a smartphone or processor, process it locally and package it as JSON.
- **Cloud:** build a back-end for data storage and, where appropriate, advanced computation/AI.
- **UI:** develop a front-end through which users can understand the resulting information.
- **Final demonstration:** demonstrate the complete system working in real time from sensor to screen.  UAB Apps

 The stated software/hardware arrangement uses a **Nordic Semiconductor SoC-BLE as the device**, an **Android smartphone as the edge**, and a cloud/server solution selected by the students for the back-end/front-end.  UAB Apps

---

 ## 5\. Learning methodology and workload

 The official workload is:

 | Activity | Hours | ECTS |
| --- | --- | --- |
| Study & homework | 90 | 3.6 |
| Lessons & seminars | 30 | 1.2 |
| Laboratories & design project | 28 | 1.12 |
| **Total** | **148** | **5.92 ≈ 6 ECTS** |

The methodology combines lectures/master classes, supervised activities, project-based learning, use cases, debates/collaboration and laboratory work.  UAB Apps

 A particularly important guideline is that **attendance is mandatory for the design-project and laboratory sessions**. Teams consist of **2–3 students**, potentially from different degree programmes. Absences are expected to be communicated to the responsible lecturer in advance with appropriate justification.  UAB Apps

 The labs are described as **supervised rather than fully guided**, meaning students are expected to work with substantial autonomy while receiving support from the instructors.  UAB Apps

---

 ## 6\. Assessment — very important

 There is **no single-assessment/exam system** for this course. It is based on continuous assessment.  UAB Apps

 The official weighting is:

 | Component | Weight |
| --- | --- |
| Individual activities/exercises | **20%** |
| IoT design project — report & defence | **40%** |
| Laboratory activities and reports | **40%** |
| **Total** | **100%** |

The individual exercises are associated with groups of lectures. The project requires **partial reports approximately every two weeks**, while the laboratory component requires two partial reports, one around mid-semester and another at the end. All activities require submission through the UAB virtual campus.  UAB Apps

 ### Passing conditions

 A weighted final grade of at least **50%** is normally sufficient, **but both the project component (B) and laboratory component (C) must individually exceed one-third of their respective ranges**. If that condition is not met, the course grade is capped at **4.0** according to the guide.  UAB Apps

 There is also a particularly important laboratory requirement:

 > You need **more than 5/10 in the laboratory component** to pass the course.  UAB Apps

 So, practically, the course is **not something you can pass simply by doing well on the individual exercises**.

---

 ## 7\. AI, plagiarism and use of existing code

 ### AI

 AI use is **explicitly allowed** in 2026/27. However, UAB warns that AI can produce serious errors and recommends validating its output before submitting reports. Students are required to **report which AI tools they used and what they used them for**.  UAB Apps

 ### Open-source code

 Open-source code and existing libraries **may be used**, but they must be appropriately referenced in the corresponding reports.  UAB Apps

 ### Plagiarism

 The policy is strict:

 - Plagiarism results in automatic failure of the involved activity/course consequences specified by the guide.
- The guide states that the final mark in such a case will be **no higher than 30%**.  UAB Apps

 This makes proper attribution of code, libraries and AI assistance especially important.

---

 ## 8\. Remedial/recovery rules

 A student who does not obtain a sufficient final weighted average may apply for remedial activities, potentially involving individual work or an additional synthesis examination, **provided that**:

 - They participated in the laboratory and design project.
- Their final weighted average is **above 30%**.
- They have not failed an activity because of plagiarism.  UAB Apps

 The course can be recorded as **"Not Evaluable"** if, among other things, the student:

 - Cannot be evaluated in the labs because of unjustified absence/non-submission.
- Completes less than **50% of the proposed activities**.
- Does not complete the design project.  UAB Apps

---

 ## 9\. What UAB expects you to be able to do

 The formal learning outcomes are broader than simply "know IoT." By the end, students are expected to be able to:

 The formal learning outcomes are broader than simply "know IoT." By the end, students are expected to be able to:

 - Identify security requirements of embedded systems.
- Design systems meeting functional and application requirements, including embedded/real-time systems.
- Compare platforms against application requirements.
- Select an appropriate platform and microprocessor.
- Design and develop the corresponding solution.
- Communicate technical results orally and in writing.
- Assess technological developments and future trends.
- Recognize relevant computer-engineering technologies.
- Produce innovative proposals.  UAB Apps

 English is also explicitly listed as a professional communication learning outcome.  UAB Apps

---

 ## 10\. 2026/27 course structure in one picture

 **Theory**

 → IoT architecture\
 → Device/edge/cloud value chain\
 → SoCs + sensors + actuators\
 → Cost/performance/energy trade-offs\
 → WBAN/WPAN/WLAN/LPWAN\
 → Bluetooth/BLE\
 → Edge platforms + RTOS\
 → EdgeAI\
 → Containers/databases/VMs

 **Project**

 → Idea + market study\
 → Requirements\
 → Architecture\
 → Component/platform selection\
 → Implementation\
 → Cost/business model\
 → Report + presentation \+ defence

 **Lab**

 → MCU + sensors\
 → BLE\
 → Edge processing\
 → JSON\
 → Cloud back-end\
 → AI/advanced processing where applicable\
 → Front-end/UI\
 → Real-time end-to-end demonstration  UAB Apps

 For **2026/27**, UAB 105075 is best understood as a **hands-on, end-to-end IoT engineering course**, rather than a conventional theory-heavy networking course. The central deliverable is an original working IoT concept/prototype spanning **embedded hardware, wireless communication, edge processing, cloud services and UI**, with **EdgeAI and energy consumption receiving increased emphasis this year**. The assessment is entirely continuous, with **60% coming from the project and labs**, mandatory participation in those practical components, and no conventional single final exam.  UAB Apps

 **Official source:**  UAB 2026/2027 Course Guide for 105075
