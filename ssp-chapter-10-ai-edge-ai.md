## Chapter 10 plan — AI / EdgeAI

 Chapter 10 should now convert the AI requirements established in Chapters 3–5 and the data architecture in Chapter 9 into a concrete intelligence architecture.

 The key principle should remain:

 > **AI is introduced only where it provides measurable value over an appropriate deterministic or statistical alternative.**

 The chapter should therefore establish **what SSP predicts or classifies, what data it uses, where the model runs, how confidence is handled, how models are trained and deployed, and what happens when AI is unavailable or uncertain.**

 ### Planned structure

 1. **10.1 AI Problem Definition**
   - Define the specific SSP problems suitable for AI.
   - Separate AI problems from deterministic/rule-based functions.
   - Establish the operational objective of each AI function.
2. **10.2 Why AI Is Required**
   - Explain where contextual or predictive intelligence adds value.
   - Compare AI with rule-based alternatives.
   - Avoid introducing AI merely for complexity or demonstration.
3. **10.3 Inputs / Features**
   - Position and position confidence.
   - Motion/inertial information.
   - Proximity.
   - Geofence state.
   - Historical movement.
   - Device/communication state.
   - Event history and contextual features.
4. **10.4 AI Outputs**
   - Trajectory prediction.
   - Event classification.
   - Anomaly score.
   - Risk/severity contribution.
   - Confidence/uncertainty.
   - Clearly distinguish AI output from the final operational decision.
5. **10.5 Candidate Algorithms / Models**
   - Establish candidate model families.
   - Compare lightweight models with more complex alternatives.
   - Consider interpretability, training requirements and computational cost.
6. **10.6 Training Data**
   - Define required datasets.
   - Discuss labelled versus unlabelled data.
   - Address representative environments and edge cases.
   - Include privacy considerations.
7. **10.7 Model Training**
   - Training/validation/test separation.
   - Feature engineering.
   - Evaluation methodology.
   - Avoiding data leakage.
   - Model selection.
8. **10.8 Cloud AI**
   - Training.
   - Fleet-level analytics.
   - Model evaluation.
   - Long-term historical analysis.
   - Model management.
9. **10.9 Edge AI**
   - Real-time contextual inference.
   - Local trajectory/risk analysis.
   - Connectivity-independent operation.
   - Reduced data transmission.
10. **10.10 Device AI**
    - Define whether any inference belongs on the constrained device.
    - Consider motion classification and event pre-processing.
    - Keep device AI lightweight.
11. **10.11 Model Deployment**
    - Model versioning.
    - Deployment.
    - Monitoring.
    - Rollback.
    - Compatibility.
    - Lifecycle management.
12. **10.12 Accuracy / Performance Requirements**
    - Detection/classification metrics.
    - Prediction error.
    - False-positive/false-negative considerations.
    - Inference latency.
    - Confidence thresholds.
    - Resource constraints.
13. **10.13 AI Resource Requirements**
    - CPU/GPU/NPU requirements where applicable.
    - RAM/flash/model size.
    - Inference energy.
    - Communication implications.
14. **10.14 Privacy Implications**
    - Local versus cloud processing.
    - Feature minimization.
    - Raw-data transmission.
    - Model/data governance.
15. **10.15 AI Failure Modes**
    - Low-confidence prediction.
    - Missing sensor data.
    - Distribution shift.
    - Model failure.
    - Connectivity loss.
    - Invalid/out-of-range output.
    - Deterministic fallback.
16. **10.16 AI Decision Architecture**
    - Establish the final relationship between AI outputs and SSP rules.
    - AI should inform operational decisions rather than silently override critical deterministic controls.
17. **10.17 Chapter Conclusion**
    - Consolidate the selected intelligence architecture.
    - Establish what will be quantified in Chapter 11 and tested in Chapter 15.

---

 # 10\. AI / EdgeAI

 ## 10.1 AI Problem Definition

 The SSP architecture does not treat artificial intelligence as a mandatory component of every processing function. Many SSP functions are inherently deterministic and can be implemented more reliably using explicit rules.

 Examples include:

 - checking whether a device is inside or outside a defined geographical zone;
- verifying whether an authenticated device is permitted to communicate;
- detecting loss of communication;
- monitoring battery thresholds;
- enforcing configured notification policies;
- determining whether a received message has valid structure and authentication.

 AI becomes relevant when SSP must interpret **patterns, uncertainty, temporal behaviour or relationships between multiple observations** that are difficult to represent efficiently using fixed rules.

 The principal AI problems considered for SSP are therefore:

 1. movement and trajectory interpretation;
2. contextual event classification;
3. anomaly detection;
4. risk/severity estimation;
5. sensor-fusion support;
6. prediction of near-future movement or state.

 The resulting conceptual chain is:

 **Sensor data → Feature extraction → AI inference → Confidence/uncertainty → Contextual assessment → Operational decision**

 The AI output is therefore one component of the SSP decision process rather than an independent replacement for the system's rules and policies.

---

 ## 10.2 Why AI Is Required

 A basic geofencing implementation can determine whether a monitored device satisfies a geographic condition:

 > **Position → Geofence rule → Boundary condition → Alert**

 This is useful but does not fully exploit the information available to SSP.

 Consider a monitored device approaching a protected zone. The system may have information about:

 - current position;
- position confidence;
- direction of movement;
- velocity;
- acceleration;
- proximity to another device;
- previous trajectory;
- recent boundary crossings;
- communication state;
- device state.

 A deterministic system can incorporate some of these variables through explicit rules. However, when the relationships become sufficiently complex, a trained model may provide a useful mechanism for identifying patterns in historical data.

 The purpose of AI in SSP is consequently not to replace deterministic monitoring, but to provide additional intelligence where measurable benefits can be demonstrated.

 The architecture adopts the following principle:

 > **If a deterministic method provides equivalent performance with lower complexity, lower energy consumption and greater interpretability, the deterministic method should be preferred.**

 AI is justified only when the expected improvement can be measured against an appropriate baseline.

---

 ## 10.3 AI Inputs and Features

 AI functions shall use structured information derived from the data flow established in Chapter 9.

 Potential inputs include:

 ### Position-related features

 - latitude;
- longitude;
- position timestamp;
- estimated positioning accuracy;
- positioning confidence;
- distance to relevant geographic boundaries;
- distance to protected locations;
- historical position sequence.

 ### Motion-related features

 - acceleration;
- angular velocity;
- estimated velocity;
- direction of travel;
- movement state;
- changes in movement state;
- duration of stationary or moving periods.

 ### Proximity-related features

 - distance to associated devices;
- BLE/proximity observations;
- duration of proximity;
- proximity confidence;
- changes in relative distance.

 ### Contextual features

 - current geofence state;
- time of day;
- operational state;
- configured monitoring policy;
- previous events;
- recent communication conditions;
- device health.

 ### Temporal features

 Rather than processing every observation independently, suitable AI models may use temporal information such as:

 - recent position sequence;
- velocity history;
- acceleration history;
- movement-state transitions;
- duration in a zone;
- rate of approach to a boundary;
- previous event sequence.

 The feature set shall remain limited to information that provides measurable value for the intended model.

---

 ## 10.4 AI Outputs

 SSP AI functions may produce several different output types.

 ### 10.4.1 Trajectory prediction

 A trajectory model may estimate the likely short-term movement of a monitored device.

 The output can include:

 - predicted position;
- predicted direction;
- predicted time to a geographic boundary;
- prediction uncertainty.

 The prediction should be treated as probabilistic information rather than as a guaranteed future position.

 ### 10.4.2 Event classification

 An AI model may classify an observed sequence into categories such as:

 - normal movement;
- unusual movement;
- prolonged stationary condition;
- unexpected movement pattern;
- potential abnormal event.

 The precise classes will depend on the training data and operational requirements.

 ### 10.4.3 Anomaly score

 Anomaly detection may provide a numerical indication that an observation or sequence differs from learned normal behaviour.

 An anomaly score shall not automatically be interpreted as proof of a security event.

 ### 10.4.4 Risk or severity contribution

 AI may provide an input to the SSP risk/severity assessment.

 For example:

 **Position + movement + proximity \+ AI output + confidence → contextual event assessment**

 The final operational policy may combine the AI output with deterministic rules and other system information.

 ### 10.4.5 Confidence or uncertainty

 Where the selected model supports confidence or uncertainty estimation, this information shall accompany the AI result where operationally relevant.

 The architecture therefore distinguishes:

 **Prediction**

 from

 **Confidence in prediction**

 This distinction is essential to prevent low-confidence AI outputs from being treated identically to well-supported outputs.

---

 ## 10.5 Candidate Algorithms and Models

 The appropriate algorithm depends on the specific SSP problem, available data and resource constraints.

 The candidate model families include:

 | Problem | Candidate approach | Principal consideration |
| --- | --- | --- |
| Movement classification | Decision tree, random forest, lightweight neural network | Accuracy versus computational cost |
| Anomaly detection | Statistical model, isolation-based method, autoencoder | Availability of labelled abnormal data |
| Trajectory prediction | Kalman/filter-based approach, regression, recurrent/temporal model | Prediction accuracy and latency |
| Sensor fusion | Kalman/filter methods, probabilistic models, ML | Interpretability versus adaptability |
| Risk/severity estimation | Rule-based baseline, logistic/regression model, tree-based model | Explainability and calibration |
| Temporal event classification | Temporal statistical model, sequence model | Model size and training-data requirements |

The table represents the candidate engineering space rather than a final algorithm selection.

 A simple deterministic or statistical baseline shall be established before a more complex model is adopted.

 This provides an objective comparison:

 > **Baseline method → AI method → Measured improvement → Engineering justification**

---

 ## 10.6 Training Data

 AI performance depends fundamentally on the quality and representativeness of the training data.

 SSP training data should represent the operational conditions under which the system is expected to function.

 Potential data sources include:

 - controlled laboratory measurements;
- simulated trajectories;
- representative field measurements;
- anonymized historical movement data where legally and ethically permissible;
- device sensor recordings;
- communication-state observations;
- manually labelled operational events.

 The dataset should contain sufficient variation in:

 - movement patterns;
- environments;
- positioning quality;
- device orientation;
- communication conditions;
- normal behaviour;
- abnormal conditions.

 Particular attention shall be given to cases where positioning confidence is low or sensor information is incomplete.

 A model trained only on ideal laboratory measurements may perform poorly when deployed in environments containing:

 - buildings;
- urban canyons;
- intermittent positioning;
- communication interruptions;
- sensor noise;
- unexpected movement patterns.

 Training data shall therefore be treated as an engineering requirement rather than as an afterthought.

---

 ## 10.7 Model Training

 The model-development process shall separate data used for training from data used to evaluate the final model.

 A representative process is:

 **Data acquisition → Data cleaning → Feature preparation → Training set → Validation set → Model selection → Independent test set → Deployment candidate**

 Data leakage must be avoided.

 For example, movement observations belonging to the same individual or trajectory should not be distributed carelessly across training and test datasets in a way that allows the model to learn the identity or exact trajectory rather than the generalizable behaviour.

 The evaluation methodology shall therefore be designed around the intended deployment conditions.

 Where sufficient data exists, the project should evaluate:

 - cross-environment performance;
- cross-device performance;
- temporal robustness;
- missing-data behaviour;
- low-confidence positioning;
- communication interruptions.

 The selected model shall not be considered production-ready solely because it performs well on the dataset used during development.

---

 ## 10.8 Cloud AI

 The Cloud layer is the preferred location for AI functions requiring substantial historical data or computational resources.

 Potential Cloud AI functions include:

 - model training;
- fleet-level behavioural analysis;
- long-term anomaly analysis;
- model comparison;
- model evaluation;
- model calibration;
- model management;
- historical trajectory analysis;
- population-level analytics where legally authorized.

 The Cloud is particularly appropriate for training because the computational resources can be scaled independently of the constrained device.

 The Cloud may therefore provide the model-development cycle:

 **Data → Training → Evaluation → Model version → Deployment candidate**

 The resulting model can subsequently be deployed to the appropriate Edge or Device layer.

 Cloud processing should not, however, be assumed to be necessary for every operational inference.

 Critical low-latency functions should not depend exclusively on Cloud availability when the requirements specify local fallback capability.

---

 ## 10.9 Edge AI

 The Edge/Mobile layer is the principal location for AI inference that requires relatively rapid response while benefiting from more computational resources than the wearable/device layer.

 Potential Edge AI functions include:

 - trajectory prediction;
- contextual event classification;
- anomaly detection;
- multi-source sensor interpretation;
- short-term risk assessment;
- local event prioritization.

 The Edge layer provides an important compromise:

 **More computational capability than the Device**

 while retaining:

 **Lower latency and greater connectivity resilience than Cloud-only processing**

 For example:

 **Device**

 → acquires position, motion and proximity observations

 **Edge/Mobile**

 → combines observations and performs contextual inference

 **Cloud**

 → performs historical analysis, model management and system-wide analytics

 This allocation is consistent with the distributed intelligence principle established in Chapter 5.

---

 ## 10.10 Device AI

 The constrained device shall not be required to perform computationally expensive AI unless a measurable benefit justifies the additional energy, memory and processor requirements.

 Potential Device AI functions include:

 - lightweight movement classification;
- sensor-quality assessment;
- event pre-classification;
- simple anomaly detection;
- sensor pre-processing.

 Device-level intelligence can reduce communication requirements by transmitting structured events rather than continuous raw sensor data.

 For example:

 **Raw inertial data → Device classification → Movement state → Edge**

 rather than:

 **Raw inertial data → continuous transmission → Edge processing**

 However, this optimization must be evaluated against the possibility that local classification errors could remove information required by higher-level processing.

 The architecture therefore permits Device AI but does not make it mandatory for all sensing functions.

---

 ## 10.11 Model Deployment and Lifecycle Management

 AI models shall be treated as controlled software assets.

 Each production model should have:

 - a unique model version;
- defined input and output specifications;
- documented training data characteristics;
- evaluation results;
- deployment status;
- compatibility information;
- rollback capability.

 The lifecycle is:

 **Train → Evaluate → Approve → Deploy → Monitor → Update/Roll back**

 Model updates shall be authenticated and integrity protected.

 The system should also monitor operational model performance where sufficient information is available to identify degradation.

 Possible causes of degradation include:

 - changes in device hardware;
- changes in sensor characteristics;
- environmental differences;
- new movement patterns;
- changes in communication conditions;
- differences between training and deployment populations.

 This is particularly important for an IoT system because the physical environment can change substantially after deployment.

---

 ## 10.12 Accuracy and Performance Requirements

 AI evaluation shall use metrics appropriate to the specific function.

 ### Classification

 Potential metrics include:

 - precision;
- recall/sensitivity;
- specificity;
- F1 score;
- confusion matrix;
- false-positive rate;
- false-negative rate.

 ### Prediction

 Potential metrics include:

 - mean position error;
- median position error;
- prediction error distribution;
- prediction horizon;
- confidence-interval coverage.

 ### Anomaly detection

 Potential metrics include:

 - detection rate;
- false-alarm rate;
- detection latency;
- precision and recall where labelled data exists.

 ### Operational performance

 AI shall also be evaluated according to:

 - inference latency;
- memory consumption;
- CPU utilization;
- energy consumption;
- communication reduction;
- behaviour under missing data.

 The AI requirement is therefore not simply:

 > **"The model must be accurate."**

 It is:

 > **"The model must provide sufficient operational performance under defined conditions while remaining compatible with the resource and safety constraints of SSP."**

 The final numerical thresholds shall be established through the requirements and validation process.

---

 ## 10.13 AI Resource Requirements

 AI deployment must respect the resource limitations of each processing layer.

 ### Device

 The primary constraints are:

 - RAM;
- flash/storage;
- CPU cycles;
- inference time;
- energy consumption;
- thermal conditions.

 ### Edge/Mobile

 The constraints are less severe but still include:

 - processor availability;
- memory;
- battery consumption for mobile devices;
- concurrent application workload;
- local storage.

 ### Cloud

 The principal constraints become:

 - compute cost;
- storage;
- data-transfer cost;
- scalability;
- service availability.

 The architecture therefore follows:

 > **Place inference at the lowest practical layer that satisfies performance, resource, privacy and reliability requirements.**

 This principle prevents unnecessary transmission while avoiding excessive computational requirements on the constrained device.

---

 ## 10.14 Privacy Implications

 AI can increase privacy risks because models may process detailed information about movement, behaviour and location.

 The SSP architecture therefore adopts data minimization principles.

 Where an Edge model can produce the required result without transmitting raw sensor information, the raw information should remain local where practical.

 For example:

 **Raw sensor data → Edge inference → Event/confidence → Cloud**

 may be preferable to:

 **Raw sensor data → Cloud → inference**

 when both provide equivalent operational performance.

 However, retaining raw information locally may sometimes reduce the ability to investigate events or retrain models.

 The architecture must therefore balance:

 - operational requirements;
- privacy;
- data retention;
- model-development needs;
- forensic requirements;
- legal obligations.

 Privacy decisions shall remain linked to the data-flow architecture established in Chapter 9 and the cloud architecture developed in Chapter 12.

---

 ## 10.15 AI Failure Modes

 AI shall not become an uncontrolled single point of failure for critical SSP functions.

 The principal AI failure conditions include:

 ### Low-confidence inference

 If confidence falls below an operational threshold, the AI result shall be marked uncertain and handled according to the configured policy.

 ### Missing input data

 If required sensor information is unavailable, the model shall either:

 - operate using an explicitly supported reduced feature set; or
- return an invalid/uncertain result.

 ### Model execution failure

 If the model cannot execute because of software or resource failure, the system shall invoke an appropriate fallback.

 ### Out-of-range output

 Outputs outside the model's valid operational range shall not be accepted without validation.

 ### Distribution shift

 If deployment conditions differ substantially from the training conditions, model performance may deteriorate.

 The system should therefore provide mechanisms for monitoring and reviewing model performance.

 ### Connectivity failure

 AI functions deployed at the Edge or Device should continue where required by the operational scenario.

 Cloud-only AI should not be the sole mechanism supporting a function whose requirements demand local continuity.

---

 ## 10.16 AI Decision Architecture

 The resulting SSP intelligence architecture is:

 **Sensors**

 ↓

 **Device preprocessing**

 ↓

 **Device AI where justified**

 ↓

 **Edge/Mobile contextual processing**

 ↓

 **Edge AI**

 ↓

 **Confidence / uncertainty assessment**

 ↓

 **Deterministic system rules \+ AI output + contextual information**

 ↓

 **Operational event assessment**

 ↓

 **Alert / action**

 ↓

 **Cloud historical analysis and model management**

 This architecture deliberately separates **AI inference** from **operational authority**.

 For example, an AI model may produce:

 > **Predicted boundary crossing: high probability**

 The operational system can then combine this with:

 - actual measured position;
- position confidence;
- geofence rules;
- movement state;
- proximity;
- device state.

 The resulting operational decision is therefore based on multiple evidence sources rather than on an AI prediction alone.

 This is especially important for SSP because the consequences of false positives and false negatives can be operationally significant.

---

 ## 10.17 AI Design Decision Summary

 The principal AI decisions established by this chapter are:

 | Decision | Rationale |
| --- | --- |
| AI is selective rather than universal | Avoid unnecessary complexity and resource consumption |
| Deterministic methods remain the baseline | They are appropriate for explicit system rules |
| AI focuses on pattern, context and prediction | These are areas where learning-based methods can provide additional value |
| Confidence accompanies AI output where available | Prevents uncertain predictions from being treated as definitive |
| Device AI is lightweight and optional | Constrained energy and memory resources |
| Edge AI performs time-sensitive contextual inference | Reduces latency and cloud dependency |
| Cloud AI performs training and system-wide analytics | Provides greater computational and historical-data resources |
| Models are version-controlled | Supports controlled lifecycle management |
| AI has deterministic fallback behaviour | Prevents AI from becoming a critical single point of failure |
| AI performance is measured against a baseline | Ensures that AI provides demonstrable engineering value |
| Privacy influences inference location | Avoids unnecessary transmission of sensitive raw information |

These decisions extend the architecture established in Chapter 5 without changing its fundamental **Device → Edge/Mobile → Cloud → User** structure.

---

 ## 10.18 Relationship to Previous Chapters

 Chapter 10 is directly derived from earlier engineering decisions.

 | Previous chapter | Input to Chapter 10 |
| --- | --- |
| Chapter 3 — Requirements | AI confidence, local processing, performance, privacy, resilience and energy requirements |
| Chapter 4 — Market/Context | Need for contextual interpretation, adaptive monitoring and distributed intelligence |
| Chapter 5 — Architecture | Device → Edge/Mobile → Cloud allocation |
| Chapter 6 — Hardware | Processor, memory, sensor and energy constraints |
| Chapter 7 — Communication | Communication cost, latency and connectivity constraints |
| Chapter 8 — Software | Application, API and processing framework |
| Chapter 9 — Data Flow | Available raw data, processed data, events and contextual information |

The AI architecture therefore does not introduce an independent technology layer. It is a processing capability integrated into the existing SSP architecture.

---

 ## 10.19 Chapter 10 Conclusion

 The SSP AI architecture is based on a selective and distributed use of intelligence.

 The fundamental design principle is:

 > **Use deterministic methods where deterministic methods are sufficient; use AI where measurable predictive, classification or contextual benefits justify its additional complexity.**

 The resulting intelligence distribution is:

 **Device**

 - sensor preprocessing;
- lightweight classification where justified;
- local event preparation.

 **Edge/Mobile**

 - sensor fusion;
- trajectory prediction;
- contextual event interpretation;
- anomaly detection;
- short-term risk assessment.

 **Cloud**

 - historical analytics;
- model training;
- model evaluation;
- fleet-level analysis;
- model management.

 AI outputs are accompanied by confidence or uncertainty information where available, and critical operational decisions are not permitted to depend exclusively on an uncontrolled AI prediction.

 The architecture consequently remains:

 **Sense → Process → Infer → Assess → Communicate → Act → Learn**

 with intelligence distributed according to:

 **Latency + Energy + Privacy \+ Connectivity + Computational resources + Reliability**
