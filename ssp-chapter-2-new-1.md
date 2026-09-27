 ## Revised Chapter 2 — Target Users, Use Cases & Operational Scenarios

 ### 2.1 SSP Actors and Users

 Introduce the main actors without going deeply into responsibilities yet:

 - **Protected person** — the person whose protection perimeter is being monitored.
- **Monitored person** — the person/device whose location or movement is subject to an authorized monitoring rule.
- **Protection operator** — the person who monitors alerts and operational status.
- **System administrator** — manages devices, users, policies and system configuration.
- **Authorized organization** — institution responsible for deploying and operating SSP.
- **Technical/service operator** — maintains devices, connectivity, cloud services and system infrastructure.

 This gives the reader the vocabulary needed for the scenarios that follow.

---

 ### 2.2 Core SSP Use-Case Model

 Rather than immediately presenting abstract stakeholder tables, introduce SSP through a simple use-case view.

 For example:

```
                 ┌─────────────────────┐
                 │ Authorized Operator │
                 └──────────┬──────────┘
                            │
                            ▼
                    Monitor SSP
                            │
                            ▼
Protected Person ──► SSP Monitoring ◄── Monitored Person
                            │
                 ┌──────────┼──────────┐
                 ▼          ▼          ▼
             Location     Risk       Device
             Status      Assessment   Status
                 │          │          │
                 └──────────┼──────────┘
                            ▼
                          Alert
                            │
                            ▼
                    Operational Action
```

 This is deliberately **conceptual**, not yet the technical architecture. The detailed Device–Edge–Cloud architecture belongs in Chapter 5.

---

 ## 2.3 Use Case 1 — Normal Monitoring

 This should be the first operational storyboard because it establishes what SSP does when nothing abnormal happens.

```
Device activated
      ↓
SSP acquires positioning and motion information
      ↓
Local processing evaluates the current state
      ↓
Relevant information is transmitted according to policy
      ↓
Edge/cloud services update the monitored status
      ↓
Authorized operator sees current status
      ↓
System continues adaptive monitoring
```

 The important point is that **normal operation does not necessarily mean continuous transmission of all raw information**.

 That becomes an important design principle later in Chapters 7, 9, 10 and 11.

---

 ## 2.4 Use Case 2 — Approach to a Protected Perimeter

 This is probably one of the most important SSP scenarios.

```
Monitored person moves
        ↓
Device detects movement
        ↓
Position + motion information evaluated
        ↓
Trajectory / proximity assessed
        ↓
Approach to protected perimeter detected
        ↓
Risk level increases
        ↓
Monitoring / communication policy adapts
        ↓
Edge performs predictive assessment
        ↓
Warning generated if threshold is reached
        ↓
Authorized operator / protected person notified
        ↓
Operational response
```

 This illustrates why SSP is more than a simple location tracker.

 The system can potentially move from:

 **normal monitoring → increased monitoring → prediction → alert → response**

 rather than treating every moment identically.

---

 ## 2.5 Use Case 3 — High-Risk / Critical Event

 A second scenario should show the escalation mechanism.

```
Abnormal movement / perimeter violation
                ↓
        Device detection
                ↓
       Local risk assessment
                ↓
       High-risk condition
                ↓
       Priority communication
                ↓
        Edge risk evaluation
                ↓
       Critical event confirmed
                ↓
          Immediate alert
                ↓
      Operator / authorized user
                ↓
         Operational response
```

 This helps establish the concept of **risk-aware operation**, which later becomes a requirement in Chapter 3 and an architectural function in Chapters 5 and 10.

---

 ## 2.6 Use Case 4 — Temporary Connectivity Loss

 This scenario is particularly important because resilience is one of SSP's stated objectives.

```
Normal monitoring
      ↓
Connectivity disruption
      ↓
Device detects communication problem
      ↓
Local functions continue
      ↓
Edge/local policies maintain monitoring
      ↓
Critical events remain detectable
      ↓
Connectivity restored
      ↓
Relevant buffered information synchronized
      ↓
Normal operation resumes
```

 This introduces the reader to the idea that **loss of cloud connectivity should not necessarily mean loss of protection functionality**.

 The exact implementation will be defined later.

---

 ## 2.7 Use Case 5 — Device Tampering or Abnormal Device State

```
Device operating normally
        ↓
Tamper / abnormal device condition detected
        ↓
Local validation
        ↓
Event classified
        ↓
Priority communication
        ↓
Edge/cloud event processing
        ↓
Operator alert
        ↓
Operational response
```

 This connects the physical device to the security architecture.

---

 ## 2.8 Use Case 6 — Privacy-Aware Monitoring

 This scenario can introduce one of SSP's distinctive design principles without getting into technical implementation yet.

```
Sensor information generated
        ↓
Local processing
        ↓
Information classified
        ↓
What information is necessary?
        ↓
┌───────────────┬────────────────┐
│ Necessary     │ Not necessary  │
│ information   │ information    │
└───────┬───────┴───────┬────────┘
        ↓               ↓
   Transmit         Retain/process
   according to     locally where
   policy            appropriate
        ↓               ↓
        └───────┬───────┘
                ↓
          SSP monitoring
```

 The point here is not yet to specify the privacy mechanism. It establishes the **user/system behavior** that later Chapters 3, 7, 9, 10 and 12 will formalize.

---

 ## 2.9 Use Case 7 — Operator Workflow

 We should also show SSP from the operator's perspective:

```
Operator logs into SSP
        ↓
System displays monitored devices
        ↓
Operator reviews:
   • Status
   • Location
   • Risk
   • Battery
   • Connectivity
   • Alerts
        ↓
No critical event?
   ├── Yes → Continue monitoring
   │
   └── No
        ↓
Review alert
        ↓
Assess available information
        ↓
Apply operational procedure
        ↓
Record / close event
```

 This makes the eventual dashboard and cloud platform much easier to understand.

---

 ## 2.10 End-to-End SSP Operational Storyboard

 After the individual scenarios, I would introduce **one consolidated storyboard**.

 This could become one of the most important figures in Chapter 2:

```
┌─────────────┐
│ Environment │
└──────┬──────┘
       ↓
┌─────────────┐
│ SSP Device  │
│ Sense       │
│ Position    │
│ Motion      │
└──────┬──────┘
       ↓
┌─────────────┐
│ Local       │
│ Intelligence│
└──────┬──────┘
       ↓
┌─────────────┐
│ Edge        │
│ Prediction  │
│ Risk        │
│ Privacy     │
└──────┬──────┘
       ↓
┌─────────────┐
│ Cloud       │
│ Intelligence│
│ Analytics   │
│ Management  │
└──────┬──────┘
       ↓
┌─────────────┐
│ Authorized  │
│ User        │
└──────┬──────┘
       ↓
┌─────────────┐
│ Operational │
│ Response    │
└─────────────┘
```

 And alongside it, we can show the **feedback loop**:

```
Operational response
        ↓
Policy / configuration
        ↓
Device + Edge
        ↓
New monitoring behavior
```

 That makes SSP look like a **complete operational system**, rather than simply a collection of IoT components.

---

 ## 2.11 Stakeholder Interaction Summary

 Only after the storyboards do we introduce the stakeholder analysis.

 A concise table would now make much more sense:

 | Actor | Interaction with SSP | Main information consumed/generated |
| --- | --- | --- |
| Protected person | Receives relevant protection notifications | Alerts, protection status |
| Monitored person | Carries/uses monitored device | Position, motion, device status |
| Protection operator | Monitors events and responds to alerts | Location, risk, alerts, device status |
| Administrator | Configures users, devices and policies | Device/configuration information |
| Organization | Deploys and manages the service | Operational and management information |
| Technical operator | Maintains infrastructure | Device, connectivity and system health |

This table is now **supporting the use cases**, rather than being the chapter itself.

---

 ## 2.12 Chapter 2 → Chapter 3 Transition

 I would finish Chapter 2 with a short bridge:

 > The use cases presented in this chapter define how SSP is expected to operate from the perspective of its users and operational environment. They identify the principal interactions, events, decisions and responses that the system must support. These scenarios provide the basis for translating the expected behavior into measurable functional, performance, security, privacy, reliability and scalability requirements in Chapter 3.

 That gives us a very clean progression:

 **Chapter 1:** Why SSP is needed and what it is\
 ↓\
 **Chapter 2:** How SSP is used and how the system behaves\
 ↓\
 **Chapter 3:** What SSP must therefore be capable of doing\
 ↓\
 **Chapter 4:** How existing solutions address these needs\
 ↓\
 **Chapter 5:** How we architect SSP to satisfy them

 ### One important structural point

 I **would not rename Chapter 2 to "System Architecture" or "Data Flow."** That would start encroaching on Chapters 5 and 9.

 Instead, I recommend freezing Chapter 2 as:

 > **2\. Target Users, Use Cases & Operational Scenarios**

 This preserves the original 17-chapter structure and its course alignment while making the chapter much more useful to the reader.

 The overall report then has a very natural narrative:

 **Problem → Users → Usage → Requirements → Existing Solutions → Architecture → Implementation Design → Validation**

 That is closer to the storyboard-oriented structure you have seen in other successful IoT projects, while still preserving our frozen SSP architecture.
