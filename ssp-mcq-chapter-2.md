# SSP Chapter 2 — Assessment Test

 I’ve treated this revised Chapter 2 as the **authoritative baseline for Chapter 2**. The questions focus on actors, operational behavior, use cases, escalation, resilience, privacy-aware monitoring, operator workflow, and the Chapter 2 → Chapter 3 requirements transition.

 As with Chapter 1, **there are no answers below**.

---

 ## Part I — Understanding

 ### 1\. Which actor is primarily responsible for monitoring alerts and operational status?

 A. Protected person\
 B. Monitored person\
 C. Protection operator\
 D. Technical/service operator

 ### 2\. What is the principal distinction between the protected person and the monitored person?

 A. The protected person operates SSP, while the monitored person administers it.\
 B. The protected person is the subject whose protection perimeter is monitored, while the monitored person/device is subject to an authorized monitoring rule.\
 C. The protected person manages devices, while the monitored person manages policies.\
 D. There is no distinction; they are two names for the same actor.

 ### 3\. Which of the following is **not** one of the actors explicitly introduced in Chapter 2?

 A. System administrator\
 B. Authorized organization\
 C. Technical/service operator\
 D. Emergency medical responder

 ### 4\. What is the main purpose of the conceptual use-case model in Section 2.2?

 A. To define the detailed Device–Edge–Cloud architecture.\
 B. To introduce how users and the system interact without prematurely defining technical architecture.\
 C. To specify the hardware components.\
 D. To establish the final communication protocols.

 ### 5\. In the Normal Monitoring scenario, why is continuous transmission of all raw information explicitly avoided as a default assumption?

 A. Raw information is never useful.\
 B. SSP is intended to use adaptive and policy-based monitoring rather than treating every moment identically.\
 C. Cloud systems cannot store raw information.\
 D. Devices cannot collect sensor information continuously.

 ### 6\. Which sequence best represents the intended escalation in the Approach to a Protected Perimeter scenario?

 A. Alert → normal monitoring → prediction → response\
 B. Normal monitoring → increased monitoring → prediction → alert → response\
 C. Cloud processing → device shutdown → alert → response\
 D. Detection → immediate intervention in every case

 ### 7\. What is the main purpose of the Temporary Connectivity Loss use case?

 A. To demonstrate that cloud connectivity is unnecessary.\
 B. To establish that loss of cloud connectivity should not necessarily result in loss of protection functionality.\
 C. To eliminate the need for buffering.\
 D. To demonstrate that all processing should move permanently to the device.

 ### 8\. In the Privacy-Aware Monitoring scenario, what happens to information classified as unnecessary?

 A. It must always be transmitted to the cloud.\
 B. It is automatically deleted in every case.\
 C. It may be retained or processed locally where appropriate.\
 D. It must be sent to the protection operator for manual classification.

 ### 9\. Which information is explicitly identified as something the operator may review?

 A. Status\
 B. Location\
 C. Risk\
 D. Battery\
 E. Connectivity\
 F. Alerts\
 G. All of the above

 ### 10\. What is the main purpose of the consolidated End-to-End SSP Operational Storyboard?

 A. To replace all individual use cases.\
 B. To show SSP as a complete operational system spanning environment, device, intelligence, users, and response.\
 C. To define detailed hardware specifications.\
 D. To prove the PoC has already been validated.

---

 # Part II — Engineering Reasoning

 ### 11\. During normal monitoring, the monitored person remains far from any protected perimeter and the assessed risk is low.

 Should SSP necessarily transmit all available sensor information continuously?

 Explain your answer using the principles established in Chapter 2.

 ### 12\. A monitored person approaches a protected perimeter, and the system detects movement consistent with an increasing risk level.

 Which sequence best reflects the intended SSP behavior?

 A. Maintain exactly the same monitoring policy until a violation occurs.\
 B. Increase monitoring/communication according to policy, perform predictive assessment, and generate a warning if the relevant threshold is reached.\
 C. Immediately disable local processing and transfer all decisions to the operator.\
 D. Immediately trigger the highest-priority response regardless of risk assessment.

 Explain why.

 ### 13\. Why does Chapter 2 introduce the **approach** to a protected perimeter rather than only the final perimeter violation?

 What architectural or operational concept does this enable SSP to demonstrate?

 ### 14\. A cloud connection is lost, but the Edge remains available.

 Based on Chapter 2, which functions should conceptually continue?

 A. Only historical analytics\
 B. Relevant monitoring and detection functions necessary to maintain protection\
 C. No monitoring until the cloud reconnects\
 D. Only battery measurement

 Explain your answer.

 ### 15\. A device detects a possible tamper condition.

 Why does Chapter 2 include **local validation** before the event proceeds to priority communication?

 Give at least two engineering reasons.

 ### 16\. Compare these two scenarios:

 - **Scenario A:** Low-risk normal monitoring.
- **Scenario B:** High-risk/critical event.

 Identify at least **three ways** in which SSP's operational behavior should differ between them according to Chapter 2.

 ### 17\. Why is the operator workflow important to the overall SSP system rather than being merely a user-interface concern?

 Consider the relationship between:

 **Status → Location → Risk → Battery → Connectivity → Alerts → Operational procedure**

---

 # Part III — Design Challenges

 ### 18\. Adaptive Monitoring Policy

 Design a conceptual monitoring policy for the following states:

 | System state | Expected monitoring behavior |
| --- | --- |
| Low risk / normal conditions | ? |
| Person approaching protected perimeter | ? |
| Elevated risk | ? |
| Critical event | ? |
| Connectivity loss | ? |
| Device tampering | ? |

For each state, describe how sensing, processing, communication, and operator notification should conceptually change.

 Do **not** specify technologies that Chapter 2 has not yet established.

---

 ### 19\. Approach Detection Challenge

 Suppose SSP receives the following progression:

 1. Monitored person is far from the protected perimeter.
2. Person moves toward the perimeter.
3. Predicted trajectory indicates continued approach.
4. Risk assessment increases.
5. Person enters the warning zone.
6. Person enters the restricted zone.

 Design a conceptual response for each stage.

 The important issue is to show **progressive escalation rather than a single binary "inside/outside" decision**.

---

 ### 20\. Connectivity Loss Challenge

 Assume:

 - Cloud connectivity is unavailable.
- The device remains operational.
- The Edge remains available.
- A potentially critical event occurs during the outage.

 Describe how SSP should behave from detection through eventual synchronization.

 Your answer should address:

 - Local detection
- Edge processing
- Alert handling
- Data retention/buffering
- Restoration of connectivity
- Synchronization

---

 ### 21\. Privacy-Aware Monitoring Challenge

 Suppose the device generates:

 - Position information
- Motion information
- Device-health information
- Raw sensor information
- A derived risk state

 Design a conceptual information-flow policy.

 For each category, explain whether it should primarily be:

 - processed locally,
- sent to the Edge,
- sent to the Cloud,
- made available to the operator,
- or retained only when necessary.

 Your answer should explain the **reasoning**, rather than assuming that all information must follow the same path.

---

 ### 22\. Tamper Detection Challenge

 A monitored device detects a possible physical tampering event, but the initial sensor indication is uncertain.

 Design a conceptual decision sequence based on Chapter 2:

 **Detection → ? → ? → ? → Operational response**

 Explain where validation and classification should occur and why.

---

 ### 23\. Operator Workflow Challenge

 Design the minimum information an operator should receive when SSP generates a high-priority alert.

 Use only information categories explicitly established in Chapter 2.

 Then explain how the operator should progress from:

 **Alert → Assessment → Procedure → Event closure**

---

 # Part IV — Critical Assessment

 ### 24\. Critical Assessment of Risk-Aware Operation

 Chapter 2 proposes that SSP can transition from:

 **normal monitoring → increased monitoring → prediction → alert → response**

 What are the potential advantages of this approach?

 Then identify **two possible risks or weaknesses** in relying on progressive risk-aware escalation.

---

 ### 25\. Critical Assessment of Connectivity Resilience

 Chapter 2 states that loss of cloud connectivity should not necessarily mean loss of protection functionality.

 Critically assess this assumption.

 What capabilities must exist elsewhere in the system for this principle to be meaningful?

 What could happen if the architecture depends too heavily on cloud services?

---

 ### 26\. Critical Assessment of Privacy

 The privacy-aware scenario asks:

 > "What information is necessary?"

 Critically assess this principle.

 Why is **data minimization based on necessity** useful, and what ambiguity remains when deciding what information is actually necessary?

---

 ### 27\. Critical Assessment of Actor Definitions

 Chapter 2 introduces six actors before going deeply into their responsibilities.

 Why is this ordering useful?

 What problems could arise if actor responsibilities were defined too early, before the use cases and operational scenarios were established?

---

 ### 28\. Critical Assessment of Use Cases

 Chapter 2 contains several use cases:

 - Normal monitoring
- Approach to protected perimeter
- High-risk/critical event
- Temporary connectivity loss
- Device tampering
- Privacy-aware monitoring
- Operator workflow

 Which **relationships between these use cases** are particularly important?

 For example, explain how one use case can trigger, modify, or constrain another.

---

 ### 29\. Requirements Derivation Challenge

 Chapter 2 ends by stating that the use cases provide the basis for Chapter 3 requirements.

 Take the following scenario:

 > A monitored person approaches a protected perimeter while connectivity is temporarily disrupted.

 Identify at least **five different categories of requirements** that could be derived from this scenario.

 For each category, give one example requirement.

 Possible categories include, but are not limited to:

 - Functional
- Performance
- Security
- Privacy
- Reliability/resilience
- Scalability
- Energy

---

 # Part V — Chapter 1 ↔ Chapter 2 Integration

 ### 30. Connecting the Design Philosophy to Operational Behavior

 Chapter 1 established four principles:

 1. Distributed intelligence
2. Adaptive monitoring
3. Security and privacy by design
4. Measurable engineering

 Show how **each principle appears operationally in Chapter 2**.

 Complete the following:

 | Chapter 1 principle | Chapter 2 operational manifestation |
| --- | --- |
| Distributed intelligence | ? |
| Adaptive monitoring | ? |
| Security/privacy by design | ? |
| Measurable engineering | ? |

For the last one, identify what Chapter 2 would need to expose or define so that the behavior can later be measured.

---

 ### 31\. Chapter 1 ↔ Chapter 2 Architecture Consistency

 Chapter 1 described:

 **Sense → Interpret → Assess → Predict → Decide → Communicate → Act → Learn**

 Chapter 2 describes scenarios involving:

 **Detection → Assessment → Prediction → Communication → Alert → Operational response**

 Explain how the Chapter 2 use cases instantiate the broader Chapter 1 design philosophy.

 Identify any stage of the Chapter 1 sequence that is **not yet sufficiently represented in Chapter 2**.

---

 # Final Challenge — Chapter 2 System Thinking

 ### 32\. End-to-End Operational Scenario

 Consider this complete situation:

 > A monitored person is initially operating normally. The person begins moving toward a protected perimeter. The system detects the movement and assesses an increasing risk. The Edge predicts continued approach. Before the warning threshold is reached, cloud connectivity is lost. The device and Edge continue operating. The device then reports an abnormal/tamper condition while the person continues approaching the perimeter. The system must minimize unnecessary disclosure of sensitive information while maintaining protection functionality.

 Using **only the concepts established in Chapters 1 and 2**, describe the complete SSP response.

 Your answer should connect:

 - Actors
- Normal monitoring
- Movement detection
- Position/motion information
- Risk escalation
- Adaptive monitoring
- Predictive assessment
- Connectivity loss
- Local/Edge resilience
- Tamper detection and validation
- Privacy-aware information handling
- Operator notification
- Operational response
- Restoration/synchronization

 The goal is not to invent detailed implementation mechanisms. The goal is to demonstrate that you understand **how the operational scenarios fit together into one coherent SSP behavior model**.

---

 ## Suggested answer format

 You can answer exactly as before:

 > **1\. C**\
>  **2\. B**\
>  **3\. D**\
>  ...\
>  **11.** \[reasoning\]\
>  \*\*12. B — explanation\]\
>  ...\
>  **32.** \[end-to-end reasoning\]

 For Questions **18–32**, I’ll assess not only whether the answer is consistent with Chapter 2, but also whether your reasoning exposes any **missing requirement, ambiguity, contradictory assumption, or architectural issue** that should potentially be carried into Chapter 3.
