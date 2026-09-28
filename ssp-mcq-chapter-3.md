# SSP Chapter 3 — Answer-Included Study & Assessment
 ---

 # Part I — Understanding

 ### 1\. What is the primary purpose of Chapter 3?

 A. To select the final hardware platform\
 B. To define what SSP must achieve and establish measurable criteria for validation\
 C. To implement the SSP prototype\
 D. To compare SSP commercially with competing products

 **Answer: B — To define what SSP must achieve and establish measurable criteria for validation**

 Chapter 3 establishes the **engineering requirements baseline**.

 It defines **what SSP must achieve**, while subsequent chapters determine **how those requirements will be achieved**.

 The key distinction is:

 **Chapter 3 = What**

 **Subsequent chapters = How**

---

 ### 2\. From where are SSP's requirements derived?

 A. Only from available laboratory hardware\
 B. Only from the selected microcontroller\
 C. From the problem definition, application domains, stakeholder interactions, and operational scenarios\
 D. Primarily from cloud-service limitations

 **Answer: C**

 The requirements are derived from the work established in Chapters 1 and 2:

 **Problem definition → Application domains → Stakeholders → Operational scenarios → Requirements**

 This prevents the engineering specification from being driven prematurely by a particular implementation platform.

---

 ### 3\. Why are requirements intentionally defined independently of specific hardware and software?

 A. To avoid having to validate the system\
 B. To prevent premature commitment to a particular implementation platform\
 C. Because hardware is irrelevant to SSP\
 D. To ensure all hardware platforms will perform identically

 **Answer: B**

 The purpose is to prevent the requirements from being constrained prematurely by:

 - a particular microcontroller,
- communication technology,
- sensor,
- cloud platform,
- laboratory resource,
- or other implementation decision.

 The desired engineering progression is:

 **Requirement → Design alternatives → Engineering decision → Implementation → Verification**

---

 ### 4\. What is the fundamental engineering relationship established in Chapter 3?

 A. Hardware → Software → Cloud → User\
 B. Stakeholder need → System requirement → Design decision → KPI → Test → Result\
 C. Sensor → Gateway → Database → Dashboard\
 D. Cost → Hardware → Software → Validation

 **Answer: B**

 This is one of the most important concepts in Chapter 3:

 **Stakeholder need → System requirement → Design decision → KPI → Test → Result**

 It provides the foundation for engineering traceability.

---

 ### 5\. What should happen when a final numerical requirement cannot yet be established?

 A. An arbitrary value should be selected.\
 B. The requirement should be removed.\
 C. It should initially be expressed as a measurable parameter, with the final target established during the relevant design chapter.\
 D. The requirement should automatically be classified as Future.

 **Answer: C**

 For example, alert latency may initially be:

 **≤ TBD**

 rather than assigning an arbitrary number before the communication and processing architecture are known.

 The final value must eventually be established **before validation**.

---

 ### 6\. Which of the following is **not** one of the requirement categories identified in Chapter 3?

 A. Energy requirements\
 B. Security requirements\
 C. Privacy requirements\
 D. Marketing requirements

 **Answer: D — Marketing requirements**

 The chapter covers categories including:

 - System
- Functional
- Performance
- Positioning/sensing/event detection
- Communication
- Intelligence/AI
- Energy
- Security
- Privacy
- Reliability/resilience/availability
- Usability/operations
- Physical/environmental
- Scalability
- Maintainability/lifecycle
- Economic

---

 ### 7\. What does FR-01 require?

 A. Every user must have a unique identity.\
 B. Every deployed SSP device must have a unique identity.\
 C. Every sensor must use GNSS.\
 D. Every device must have a cellular connection.

 **Answer: B**

 FR-01 requires each deployed SSP device to have a **unique identity** that can be securely associated with:

 - its authorized configuration,
- deployment context,
- operational status.

 This is foundational for device management and security.

---

 ### 8\. What is the purpose of FR-03, Position Confidence?

 A. To eliminate all positioning errors\
 B. To provide an indication of estimated positioning quality where technically feasible\
 C. To replace GNSS with AI\
 D. To prevent positioning information from reaching the Edge

 **Answer: B**

 SSP should not necessarily treat every positioning result as equally reliable.

 Where available, positioning confidence can become an input to downstream decision-making.

 Conceptually:

 **Position → Position confidence → Decision interpretation**

---

 ### 9\. What does FR-11, Adaptive Monitoring, require?

 A. The system must always operate at maximum sensing intensity.\
 B. The system must continuously transmit all sensor data.\
 C. SSP must support changes in sensing, processing, and communication behavior according to context, policy, system state, and risk.\
 D. Monitoring should be disabled whenever battery energy is low.

 **Answer: C**

 Adaptive monitoring is a central SSP requirement.

 The objective is to avoid unnecessary maximum-intensity operation while preserving critical functions.

---

 ### 10\. What is the purpose of FR-12, Local Decision Capability?

 A. To eliminate the Cloud entirely\
 B. To ensure every decision is made on the Device\
 C. To provide local or near-local decisions where cloud-only processing would not satisfy latency, connectivity, privacy, resilience, or operational-continuity requirements\
 D. To reduce the number of sensors

 **Answer: C**

 The requirement deliberately does **not** dictate that all intelligence must be on the Device.

 Instead, the allocation between:

 **Device ↔ Edge/Mobile ↔ Cloud**

 is determined by engineering considerations.

---

 # Part II — Engineering Reasoning

 ### 11\. Why is "TBD" preferable to an arbitrary numerical target in early requirements?

 **Answer:**

 Because the correct target may depend on engineering decisions that have not yet been finalized.

 For example, alert latency depends on factors such as:

 - sensing architecture,
- local processing,
- communication technology,
- Edge processing,
- cloud processing,
- network conditions,
- application requirements.

 Assigning an arbitrary value too early could create a requirement that is either:

 - unnecessarily restrictive, or
- insufficiently demanding.

 The correct approach is:

 **Initial measurable parameter → Architecture/design analysis → Final target → Validation**

---

 ### 12\. A team selects a microcontroller capable of achieving 5 ms local processing latency before defining the actual system latency requirement.

 What methodological problem could this create?

 **Answer:**

 It risks allowing the available hardware to define the requirement rather than allowing the requirement to drive the engineering design.

 The intended methodology is:

 **Stakeholder/application need → Requirement → Architecture → Component selection**

 not:

 **Available component → Claimed capability → Requirement**

 The latter can lead to **technology-driven requirements**.

---

 ### 13\. Why does SSP need both FR-02 Position Acquisition and FR-03 Position Confidence?

 **Answer:**

 Position acquisition answers:

 > **Where does the system estimate the device to be?**

 Position confidence addresses:

 > **How reliable is that estimate?**

 A location without confidence information can be misleading in situations such as:

 - poor satellite visibility,
- indoor operation,
- multipath,
- interference,
- degraded sensors,
- temporary positioning loss.

 SSP therefore distinguishes the **measurement** from the **quality of the measurement**.

---

 ### 14\. Why is position confidence particularly important for adaptive monitoring?

 **Answer:**

 Because monitoring intensity may depend not only on the estimated position but also on how trustworthy that position is.

 For example:

 **High-confidence position \+ low risk**\
 → normal monitoring may be appropriate.

 **Low-confidence position \+ elevated risk**\
 → the system may need additional sensing, local processing, or alternative positioning/contextual information.

 Therefore:

 **Position → Confidence → Risk interpretation → Monitoring policy**

 is more robust than:

 **Position → Monitoring policy**

---

 ### 15\. Why does Chapter 3 require event generation as a separate functional requirement?

 **Answer:**

 Raw sensor measurements are not necessarily operational events.

 SSP needs a transformation such as:

 **Raw observations → Interpretation → Structured event**

 For example:

 - accelerometer readings,
- GNSS position,
- communication state,
- battery state,
- tamper signal

 may be combined into a structured event containing:

 - event type,
- timestamp,
- relevant location,
- severity/context,
- device identity,
- supporting information.

 This makes subsequent risk assessment and operational handling more systematic.

---

 ### 16\. Why is risk/severity assessment separated from event generation?

 **Answer:**

 Because detecting an event and determining its significance are different functions.

 For example:

 **Event:** Device enters a defined geographical zone.

 That does not automatically determine the final operational response.

 The significance could depend on:

 - position confidence,
- proximity,
- movement state,
- historical information,
- configured rules,
- device state,
- communication state,
- event history.

 Therefore:

 **Event detection ≠ risk assessment**

---

 ### 17\. Why does COM-03 require communication prioritization?

 **Answer:**

 Because SSP does not treat all information as equally urgent.

 The requirement establishes a conceptual hierarchy:

 **Routine status → Normal priority**

 **Elevated condition → Higher priority**

 **Critical event → Immediate/high priority**

 This supports:

 - lower latency for critical events,
- more efficient communication,
- better energy management,
- reduced network congestion,
- appropriate operational response.

---

 ### 18\. Why does COM-05 Data Minimization belong in the communication requirements?

 **Answer:**

 Because the system should not automatically transmit everything it generates.

 The receiving layer should receive the information necessary to perform its function.

 This supports both:

 - **privacy**, by reducing unnecessary exposure of sensitive information;
- **efficiency**, by reducing communication volume and associated energy consumption.

 Thus:

 **Data minimization → Privacy \+ communication efficiency \+ energy efficiency**

---

 ### 19\. Why does SSP treat AI as a capability rather than an objective in itself?

 **Answer:**

 Chapter 3 explicitly states that AI should be introduced only where it provides a **measurable benefit** compared with an appropriate deterministic, statistical, or rule-based alternative.

 Therefore, the engineering question is not:

 > "Can we use AI?"

 but:

 > "Does AI provide a measurable operational advantage for this function?"

 Possible advantages could include:

 - better prediction,
- improved anomaly detection,
- trajectory prediction,
- sensor fusion,
- improved risk assessment.

 But these benefits must be demonstrated quantitatively.

---

 ### 20\. Why is AI confidence/uncertainty important in SSP?

 **Answer:**

 A prediction is not necessarily equivalent to a confirmed operational condition.

 If an AI model reports:

 **Prediction A — confidence 0.98**

 and another reports:

 **Prediction B — confidence 0.42**

 the system should not necessarily treat them identically.

 AI-07 requires SSP to use confidence or uncertainty information where appropriate so that **low-confidence predictions do not automatically receive the same treatment as high-confidence decisions**.

 This is particularly important when AI output can influence:

 - risk,
- alerts,
- monitoring intensity,
- communication,
- operational action.

---

 # Part III — Design Challenges

 ### 21\. Design Challenge — Adaptive Energy Management

 An SSP wearable has limited battery capacity.

 The system can operate in three conceptual states:

 - Normal
- Elevated
- Critical

 Using Chapter 3, design a conceptual monitoring strategy.

 **Answer:**

 A suitable conceptual strategy would be:

 **Normal**\
 → low-power sensing\
 → reduced communication intensity\
 → routine monitoring.

 **Elevated**\
 → increase relevant sensing\
 → increase processing\
 → increase communication priority\
 → perform more detailed assessment.

 **Critical**\
 → prioritize protection-critical sensing and communication\
 → local/Edge decision capability\
 → high-priority transmission\
 → minimize energy savings that could compromise critical protection.

 The underlying relationship is:

 **Risk → Monitoring intensity → Processing intensity → Communication intensity → Energy consumption**

 The exact numerical thresholds should be defined later.

---

 ### 22\. Design Challenge — Connectivity Loss

 The Device loses communication with the Cloud, but the Device and Edge remain operational.

 Which functions should conceptually continue?

 **Answer:**

 Where required by the operational scenario, selected functions should continue locally, including:

 - relevant sensing,
- event detection,
- selected risk/decision functions,
- monitoring,
- event preservation.

 The system should preserve important events locally or at the Edge until secure forwarding becomes possible.

 The key principle is:

 **Cloud unavailability should not automatically imply complete loss of protection functionality.**

---

 ### 23\. Design Challenge — Positioning Uncertainty

 Suppose SSP reports a position close to a restricted zone, but the estimated positioning confidence is poor.

 What should the system avoid doing?

 **Answer:**

 It should avoid automatically treating the uncertain position as equivalent to a high-confidence position.

 Instead, the system should potentially:

 - consider the confidence level,
- use additional contextual information,
- use motion information,
- consider alternative positioning sources where available,
- perform additional Edge assessment,
- adapt monitoring intensity.

 This is the purpose of PS-06:

 **Position confidence must be capable of propagating into relevant decision functions.**

---

 ### 24\. Design Challenge — Sensor Fusion

 SSP has:

 - GNSS,
- inertial sensing,
- BLE proximity,
- Wi-Fi information.

 What does PS-07 require?

 **Answer:**

 Where multiple sensing sources are used, SSP must provide a **defined mechanism for combining or correlating relevant information**.

 The mechanism could be:

 - deterministic,
- statistical,
- machine-learning based.

 Chapter 3 intentionally does not prescribe which method must be selected.

 That decision belongs to the subsequent engineering design.

---

 ### 25\. Design Challenge — AI Failure

 An AI-based trajectory prediction model becomes unavailable during operation.

 What should SSP do?

 **Answer:**

 The AI model must not become an uncontrolled single point of failure for critical functions.

 AI-08 requires defined fallback behavior for cases such as:

 - model unavailable,
- insufficient confidence,
- execution failure,
- unacceptable output.

 Possible conceptual fallback mechanisms include:

 - deterministic rules,
- existing geofence logic,
- local sensing,
- conventional risk assessment,
- Edge processing.

 The exact fallback mechanism should be defined later according to the specific function.

---

 ### 26\. Design Challenge — Privacy-Aware Communication

 A device generates extensive raw movement data every second, but the Edge only needs a summarized state to perform its current function.

 What should SSP conceptually do?

 **Answer:**

 SSP should avoid automatically transmitting the complete raw dataset.

 A possible flow is:

 **Raw sensing → Local processing → Relevant information extraction → Transmit necessary information → Edge assessment**

 This supports:

 - data minimization,
- privacy,
- reduced communication load,
- reduced communication energy.

 Additional information could be transmitted when operational conditions require it.

---

 # Part IV — Critical Assessment

 ### 27\. Critical Assessment — Is a "TBD" Requirement Weak?

 Some engineers might argue that a requirement such as:

 > Alert latency ≤ TBD

 is not a real requirement.

 Is that criticism justified?

 **Answer: Partially, but only at the current development stage.**

 A TBD numerical target is incomplete as a **final acceptance requirement**.

 However, Chapter 3 explicitly uses TBD values where the final target depends on subsequent engineering decisions.

 The important condition is that the value must eventually be:

 - defined,
- measurable,
- justified,
- established before validation,
- traceable to the application scenario.

 Therefore:

 **TBD during early engineering = acceptable**

 **TBD at final validation = unacceptable**

---

 ### 28\. Critical Assessment — Does Adaptive Monitoring Risk Reducing Security?

 Could adaptive monitoring actually make SSP less secure?

 **Answer: Yes, if poorly designed.**

 Adaptive monitoring creates a potential trade-off.

 For example:

 **Lower risk → reduced sensing/communication**

 could improve:

 - energy efficiency,
- communication efficiency,
- battery autonomy.

 But if risk is incorrectly assessed as low, excessive reduction in monitoring could delay detection.

 Potential causes include:

 - incorrect positioning,
- low-quality sensor information,
- incorrect risk classification,
- AI prediction errors,
- communication-state misinterpretation.

 Therefore, EN-07 explicitly establishes that energy-saving mechanisms must not compromise critical security/protection functions beyond defined limits.

 Adaptive behavior therefore requires:

 **Risk assessment + safeguards \+ measurable validation**

---

 ### 29\. Critical Assessment — Why Isn't "More AI" Automatically Better?

 **Answer:**

 Because AI introduces its own engineering costs and risks.

 Potential disadvantages include:

 - computational requirements,
- energy consumption,
- latency,
- model failure,
- uncertainty,
- maintenance requirements,
- model-management complexity,
- potentially difficult validation.

 Chapter 3 therefore requires every AI function to have:

 **Defined operational purpose \+ measurable performance objective**

 AI should be selected when it provides a measurable benefit over an appropriate alternative.

---

 ### 30\. Critical Assessment — Is Local Processing Always Better for Privacy?

 **Answer: No.**

 Local processing can reduce unnecessary transmission of sensitive information, which can improve privacy.

 However, privacy depends on the complete system, including:

 - local storage,
- device security,
- Edge processing,
- cloud storage,
- access control,
- retention,
- communication security,
- auditability.

 Local processing may reduce data transmission but does not automatically guarantee privacy.

 The correct principle is:

 **Privacy by design across the complete information lifecycle.**

---

 ### 31\. Critical Assessment — Is High Availability the Same as Resilience?

 **Answer: No.**

 They are related but distinct.

 **Availability** concerns whether the system is operational and accessible.

 **Resilience** concerns the system's ability to continue providing appropriate functionality despite:

 - failures,
- disruptions,
- communication loss,
- subsystem degradation.

 For example, SSP could maintain some critical monitoring during cloud failure.

 That demonstrates **resilience**, even if some cloud-dependent functionality is temporarily unavailable.

---

 ### 32\. Critical Assessment — Does Device–Edge–Cloud Mean Every Function Must Exist at All Three Layers?

 **Answer: No.**

 The three layers are complementary processing domains, not a requirement that every function be duplicated everywhere.

 The allocation depends on:

 - latency,
- energy,
- privacy,
- connectivity,
- computational resources,
- scalability.

 For example:

 **Device**\
 → sensing and lightweight local inference.

 **Edge**\
 → predictive geofencing and risk assessment.

 **Cloud**\
 → historical analytics, fleet management, model management.

 The architecture should avoid unnecessary duplication while maintaining appropriate resilience.

---

 # Part V — Requirements Traceability

 ### 33\. A stakeholder requires "timely protection."

 Translate this need into the Chapter 3 engineering chain.

 **Answer:**

 A possible traceability chain is:

 **Stakeholder need**\
 → Timely protection

 **Requirement**\
 → Critical-event alert latency must remain below a defined maximum.

 **Architecture element**\
 → Device/Edge event-processing and communication chain.

 **KPI**\
 → End-to-end alert latency.

 **Verification**\
 → Performance test under defined operating/network conditions.

 **Result**\
 → Measured latency versus acceptance threshold.

 This illustrates:

 **Stakeholder → Need → Requirement → Architecture → Component → Implementation → KPI → Test**

---

 ### 34\. A stakeholder requires long autonomous operation.

 Construct the corresponding traceability chain.

 **Answer:**

 **Stakeholder need**\
 → Long autonomous operation

 **Requirement**\
 → Battery autonomy appropriate to the intended application.

 **Design element**\
 → Power-management architecture, sensing strategy, communication strategy, hardware.

 **KPI**\
 → Battery life / daily energy consumption / energy per event.

 **Verification**\
 → Controlled energy/autonomy test under a defined operating profile.

 The operating profile is important because battery autonomy cannot be meaningfully evaluated without defining how the device is being used.

---

 ### 35\. A stakeholder requires reduced exposure of sensitive location information.

 What requirement and KPIs could address this?

 **Answer:**

 Possible requirement:

 **PRV-01 — Data Minimization**

 The system shall collect and transmit only information required for the authorized function.

 Supporting requirement:

 **PRV-06 — Privacy-Aware Communication**

 The information transmitted should vary according to operational conditions and requirements.

 Possible KPIs include:

 - sensitive data transmitted,
- local-processing ratio,
- data-minimization ratio,
- access-control events,
- retention compliance.

 Verification could include a **data-flow/privacy test**.

---

 # Part VI — Integrated Engineering Scenarios

 ### 36\. Integrated Scenario

 A monitored device is approaching a protected perimeter.

 At the same time:

 - GNSS confidence decreases.
- Motion indicates elevated activity.
- Battery level is low.
- Cellular connectivity is intermittent.
- The Edge is available.
- The event may be operationally significant.

 Using Chapter 3, describe how the requirements interact.

 **Answer:**

 A suitable conceptual response is:

 **1\. Position acquisition — FR-02 / PS-01**

 The device continues acquiring position information.

 **2\. Position confidence — FR-03 / PS-06**

 The reduced GNSS confidence must be considered in downstream decisions.

 **3\. Motion monitoring — FR-04 / PS-04**

 Motion information contributes to state/event interpretation.

 **4\. Event generation — FR-08**

 Relevant observations are converted into a structured event.

 **5\. Risk assessment — FR-09**

 Risk can incorporate:

 - position,
- confidence,
- movement,
- geographical rules,
- device state,
- communication state,
- event history.

 **6\. Adaptive monitoring — FR-11 / EN-01**

 Elevated risk may justify increased monitoring despite low battery.

 **7\. Communication prioritization — COM-03**

 If the event becomes critical, communication priority increases.

 **8\. Communication resilience — COM-04**

 Intermittent cellular connectivity requires appropriate fallback behavior.

 **9\. Local decision capability — FR-12**

 The Edge can perform relevant assessment without relying exclusively on cloud processing.

 **10\. Privacy — COM-05 / PRV-01 / PRV-06**

 Only necessary information should be transmitted.

 **11\. Energy protection — EN-07**

 Energy-saving behavior must not compromise critical protection functionality beyond defined limits.

 This scenario demonstrates that SSP requirements are **interdependent rather than isolated checkboxes**.

---

 # Part VII — Higher-Level Assessment

 ### 37\. Why is the distinction between requirements and design especially important in SSP?

 **Answer:**

 Because SSP contains many possible implementation choices.

 For example, the requirement may be:

 > The system shall acquire positioning information appropriate to the deployment scenario.

 That does **not** yet dictate:

 - which GNSS receiver,
- which microcontroller,
- which positioning algorithm,
- whether Wi-Fi is used,
- whether BLE is used,
- which fusion algorithm is selected.

 Those decisions belong to subsequent chapters.

 This separation allows the project to compare alternatives objectively rather than designing the requirements around the first implementation that happens to be available.

---

 ### 38\. Which Chapter 3 requirement most directly protects against the possibility that an AI model becomes a critical single point of failure?

 A. AI-01 Meaningful AI Use\
 B. AI-05 Cloud Intelligence\
 C. AI-07 AI Confidence and Uncertainty\
 D. AI-08 AI Failure Handling

 **Answer: D — AI-08 AI Failure Handling**

 AI-08 explicitly requires fallback behavior when a model:

 - is unavailable,
- has insufficient confidence,
- fails to execute,
- produces unacceptable output.

 It also explicitly states that AI should not create an **uncontrolled single point of failure** for critical functions.

---

 ### 39\. Which requirement most directly supports operation when cloud connectivity is temporarily unavailable?

 A. FR-13 Cloud Processing\
 B. FR-18 Communication-Loss Operation\
 C. COM-02 Communication Technology Selection\
 D. PRV-05 Retention Control

 **Answer: B — FR-18 Communication-Loss Operation**

 FR-18 directly requires defined behavior for temporary communication loss between:

 - Device and Edge/Mobile,
- Device and Cloud,
- Edge/Mobile and Cloud.

 It also requires selected functions to continue locally where the operational scenario requires this.

---

 ### 40\. Which requirement most directly establishes that energy-saving mechanisms must not undermine critical protection?

 A. EN-01\
 B. EN-03\
 C. EN-05\
 D. EN-07

 **Answer: D — EN-07**

 EN-07 establishes the **Energy–Performance Trade-off** principle:

 > Energy-saving mechanisms shall not compromise critical security or protection functions beyond the limits defined by the applicable requirements.

 This is an important SSP design constraint.

---

 ### 41\. Which statement best describes the relationship between Chapter 3 and later chapters?

 A. Chapter 3 defines the final hardware architecture.\
 B. Chapter 3 defines what SSP must achieve; later chapters define how it will achieve those requirements.\
 C. Chapter 3 is independent of validation.\
 D. Later chapters can change requirements without traceability.

 **Answer: B**

 This is the central methodological principle of the chapter:

 **Chapter 3 = WHAT**

 **Chapters 5 onward = HOW**

 The requirements must remain traceable into:

 **Architecture → Components → Implementation → KPI → Test → Result**

---

 # Chapter 3 — Core Concepts to Retain

 For the eventual **17-chapter integrated examination**, these are the concepts from Chapter 3 that are particularly important to retain:

 1. **Chapter 3 defines what SSP must achieve.**
2. Requirements originate from:\
    **Problem → Applications → Stakeholders → Use cases → Requirements**
3. Requirements should initially remain **implementation-independent**.
4. The fundamental engineering chain is:
    **Stakeholder need → Requirement → Design decision → KPI → Test → Result**
5. **TBD is acceptable during early design** when the final value depends on subsequent engineering decisions.
6. TBD values must be finalized **before validation**.
7. SSP requirements cover:
   - functionality,
   - performance,
   - positioning,
   - sensing,
   - communication,
   - AI,
   - energy,
   - security,
   - privacy,
   - reliability,
   - usability,
   - physical/environmental conditions,
   - scalability,
   - maintainability,
   - economics.
8. **Position confidence is distinct from position itself.**
9. **Event detection is distinct from risk assessment.**
10. Communication should be **prioritized according to operational importance**.
11. Communication should follow **data minimization** principles.
12. AI is a **capability, not an objective in itself**.
13. AI must provide a **measurable benefit** over an appropriate alternative.
14. AI confidence/uncertainty should influence decisions where appropriate.
15. AI must have **fallback behavior** and must not become an uncontrolled single point of failure.
16. Energy management must be adaptive.
17. Energy savings must not compromise critical protection beyond defined limits.
18. Security and privacy are **end-to-end system requirements**.
19. Resilience means retaining appropriate functionality during failures/disruptions.
20. Requirements must remain traceable throughout the project.
21. Every critical requirement ultimately needs:\
     **Test condition → Measurement → Acceptance threshold → Result → Status**
22. The overall Chapter 3 philosophy is:

 **Requirements → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Cost → Validation**

 ### The three distinctions to remember especially well

 **Requirement vs. Design**

 > What SSP must achieve vs. how SSP achieves it.

 **Event vs. Risk**

 > Detecting something happened vs. determining how significant it is.

 **AI prediction vs. Decision**

 > A model can provide an uncertain prediction; the system must determine how that prediction is safely used.

 These three distinctions are likely to become important when Chapter 3 is later integrated with the architecture, AI, security, energy, and validation chapters.
