## Chapter 12 plan

 Chapter 12 should **not redesign the IoT architecture** established in Chapter 5, repeat the detailed data-flow analysis from Chapter 9, or repeat the AI design from Chapter 10. Its role is to turn the already-defined Cloud layer into an implementable backend architecture.

 The chapter will therefore follow this logic:

 1. **Cloud requirements** — derive the cloud responsibilities from Chapters 3, 5, 9, 10 and 11.
2. **Deployment model** — define the cloud as a managed, scalable, security-controlled environment, with  AWS  used as the reference implementation.
3. **API architecture** — distinguish device ingestion, internal service APIs and user-facing APIs.
4. **Backend services** — define ingestion, event processing, device management, alerting, configuration and reporting services.
5. **Database** — establish what operational information belongs in the primary database and how it is organized.
6. **Data storage** — separate operational data from historical/raw/archive data.
7. **Event processing** — define how cloud events are filtered, enriched, persisted and distributed.
8. **AI/cloud processing** — connect Chapter 10's distributed AI architecture to the cloud without moving functions unnecessarily into the cloud.
9. **Authentication** — distinguish human-user authentication from device authentication.
10. **Authorization** — implement role- and resource-based access control.
11. **Security** — define cloud security boundaries, encryption, auditability, secrets, monitoring and device lifecycle security.
12. **Monitoring** — define operational observability for the SSP fleet and cloud platform.
13. **Backup/recovery** — define recovery objectives and mechanisms.
14. **Scalability** — demonstrate how the architecture grows from 10 → 100 → 500 devices and beyond.
15. **Estimated cloud costs** — establish a cost model rather than prematurely fixing a final TCO; detailed business costing remains Chapter 14.

 The key architectural principle will be:

 > **The Cloud is the system-wide coordination, persistence, analytics and management layer; it is not assumed to be the real-time decision layer for every SSP function.**

 That preserves the central **Device → Edge/Mobile → Cloud → User** architecture established earlier.

---

 # 12\. Cloud Architecture

 ## 12.1 Cloud Requirements

 The Cloud layer is responsible for providing system-wide services that cannot efficiently or reliably be performed exclusively by the constrained SSP device or by the Edge/Mobile layer.

 The cloud architecture must therefore support the requirements established in Chapters 3 and 5 while remaining consistent with the data-flow and distributed-intelligence decisions developed in Chapters 9 and 10.

 The principal cloud requirements are:

 - secure ingestion of information from SSP devices and Edge/Mobile nodes;
- device registration and lifecycle management;
- centralized configuration and policy management;
- event processing and persistence;
- historical data storage;
- alert distribution;
- user and operator services;
- API-based integration with authorized external systems;
- fleet monitoring;
- audit logging;
- cloud-side analytics;
- model management and cloud AI where justified;
- backup and recovery;
- scalable processing and storage;
- controlled access to sensitive location and operational information.

 The cloud shall not be used simply because centralized processing is technically possible.

 Functions requiring very low latency, continued operation during connectivity loss, or local privacy-preserving processing should remain at the Device or Edge/Mobile layer.

 The resulting division is:

 **Device**

 → sensing, local preprocessing, immediate local functions

 **Edge/Mobile**

 → local contextual processing, aggregation, fallback operation and selected intelligence

 **Cloud**

 → system-wide persistence, fleet management, centralized event processing, historical analysis, policy management, model management and operational services

 **User**

 → authorized visualization, configuration, investigation and operational response.

 This division preserves the fundamental SSP principle that processing should be performed at the layer where it provides the greatest operational benefit.

---

 ## 12.2 Cloud Deployment Model

 The proposed SSP cloud architecture uses a **managed cloud-services model** rather than requiring the project to operate its own physical server infrastructure.

 Amazon Web Services (AWS)  is selected as the reference cloud implementation for the engineering design because its IoT platform provides managed device connectivity, messaging, authentication mechanisms, rules-based data routing and device-management capabilities.

 AWS IoT Core provides a managed device gateway and message broker for device-to-cloud communication and supports MQTT-based publish/subscribe communication as well as MQTT over WebSockets. AWS documentation also describes authentication and encryption mechanisms for device connections.  Amazon Web Services, Inc.+1

 The selection of AWS at this stage should be understood as a **reference implementation decision**, not as a claim that SSP could only be implemented using AWS.

 The underlying SSP cloud requirements remain vendor-independent.

 The conceptual architecture is therefore:

```
                    ┌───────────────────────────────┐
                    │       Authorized Users        │
                    │ Web Dashboard / Mobile App    │
                    └───────────────┬───────────────┘
                                    │
                              HTTPS / API
                                    │
                    ┌───────────────▼───────────────┐
                    │        API / Access Layer     │
                    │ Authentication + Authorization│
                    └───────────────┬───────────────┘
                                    │
             ┌──────────────────────┼──────────────────────┐
             │                      │                      │
     ┌───────▼────────┐    ┌────────▼────────┐    ┌────────▼────────┐
     │ Device / Fleet │    │ Event Processing│    │ Configuration / │
     │ Management     │    │ and Alerting    │    │ Policy Services │
     └───────┬────────┘    └────────┬────────┘    └────────┬────────┘
             │                      │                      │
             └──────────────────────┼──────────────────────┘
                                    │
                         ┌──────────▼──────────┐
                         │   Data Services     │
                         │ Operational DB      │
                         │ Object Storage      │
                         │ Event/Log Storage   │
                         └──────────┬──────────┘
                                    │
                         ┌──────────▼──────────┐
                         │ Analytics / Cloud AI│
                         │ Models + Historical │
                         │ Analysis             │
                         └─────────────────────┘

              ▲
              │ Secure IoT messaging
              │
      ┌───────┴────────┐
      │ AWS IoT Layer  │
      │ Device Gateway │
      │ Message Broker │
      │ Rules          │
      └───────┬────────┘
              ▲
              │
       Device / Edge
```

 This architecture separates the **IoT ingestion plane** from the **application/service plane**.

 That separation is important because an IoT device should not be given unrestricted access to application databases or administrative services.

---

 ## 12.3 API Architecture

 The SSP cloud shall use APIs to separate external clients from internal cloud services.

 Three principal API categories are defined.

 ### 12.3.1 Device ingestion interface

 The device and Edge/Mobile layer shall communicate through the IoT communication layer rather than directly accessing the operational database.

 The principal device-facing pattern is:

 **Device/Edge → IoT gateway → message broker → rules/event processing**

 AWS IoT Core supports device communication through its managed device gateway and message broker, with MQTT and MQTT over WebSockets available for device/application communication.  AWS Documentation+1

 This arrangement provides an important security boundary.

 The device does not need direct database credentials.

 Instead, it publishes authenticated messages to authorized topics.

---

 ### 12.3.2 Application API

 The user interface shall communicate with backend services through controlled HTTPS APIs.

 Typical API functions include:

 - authentication;
- device inventory;
- current device status;
- event retrieval;
- alert retrieval;
- historical event queries;
- geographical-rule configuration;
- monitoring-policy configuration;
- user administration;
- reporting;
- operational acknowledgements.

 The API layer shall validate:

 - identity;
- authorization;
- request structure;
- requested resource;
- permitted operation;
- data scope.

 The API shall not expose unrestricted database operations to the frontend.

---

 ### 12.3.3 Administrative and integration APIs

 Separate interfaces may be provided for authorized institutional or enterprise integrations.

 Examples include:

 - external case-management systems;
- authorized emergency-response systems;
- institutional monitoring platforms;
- reporting systems;
- device-management systems.

 Such integrations shall be explicitly authorized and shall not receive unrestricted access to SSP's internal data.

 The integration architecture should use versioned APIs so that future changes do not require simultaneous modification of every connected system.

---

 ## 12.4 Backend Services

 The SSP backend is logically decomposed into several services.

 The initial service decomposition is:

 | Service | Main responsibility |
| --- | --- |
| Device Management Service | Registration, inventory, status and lifecycle |
| Ingestion Service | Reception and validation of device/Edge data |
| Event Service | Creation, enrichment and persistence of events |
| Alert Service | Alert generation and notification management |
| Policy Service | Geofences, thresholds and monitoring policies |
| Configuration Service | Device and system configuration |
| User Service | User profiles and role information |
| Reporting Service | Historical and operational reports |
| Analytics Service | System-wide analysis and KPIs |
| Model Service | AI model metadata, versions and deployment status |
| Audit Service | Security and operational audit records |

These services may initially be implemented as a relatively small number of deployable applications.

 The logical separation is more important than creating a large number of independently deployed microservices from the beginning.

 This avoids unnecessary architectural complexity while preserving the ability to separate services as system scale increases.

---

 ### 12.4.1 Device management

 The cloud shall maintain a representation of each authorized SSP device.

 Information associated with a device may include:

 - device identifier;
- hardware model;
- firmware version;
- configuration version;
- deployment status;
- assigned operational group;
- last communication time;
- battery status;
- communication status;
- security state;
- lifecycle state.

 AWS IoT Device Management provides capabilities for registering, organizing, monitoring and remotely managing IoT devices, including fleet organization and OTA update mechanisms.  AWS Documentation+1

 This aligns directly with the device-lifecycle requirements established in Chapter 3.

---

 ### 12.4.2 Event processing

 Incoming information shall not automatically become an operational alert.

 The cloud event-processing chain should be:

 **Receive → Validate → Normalize → Enrich → Evaluate → Persist → Notify if required**

 For example, a received position message can be associated with:

 - device identity;
- timestamp;
- position confidence;
- current monitoring policy;
- relevant geographical rule;
- recent event history;
- communication state.

 The resulting structured event can then be evaluated according to the applicable policy.

 This prevents the cloud from treating every incoming telemetry message as an operational event.

---

 ### 12.4.3 Alert service

 The Alert Service converts qualifying events into operational notifications.

 An alert record should contain at least:

 - alert identifier;
- associated device;
- event identifier;
- timestamp;
- severity;
- event type;
- relevant location;
- position confidence;
- processing status;
- acknowledgement status;
- escalation state.

 The alert service should also support deduplication and correlation.

 For example, repeated telemetry messages indicating the same continuing condition should not necessarily generate a new operator notification for every message.

---

 ## 12.5 Database

 The primary operational database shall store structured information required for real-time and near-real-time application operation.

 For the reference AWS architecture, **Amazon DynamoDB** is proposed as the primary operational NoSQL database.

 This is appropriate for the SSP workload because much of the application data is naturally represented as device-, event-, alert-, configuration- and user-related records accessed through defined keys.

 DynamoDB provides on-demand capacity mode with pay-per-request operation and automatic scaling, making it suitable for an initial deployment where traffic may be uncertain and progressively increase.  AWS Documentation+1

 The database should contain logically separated entities such as:

 ### Device

 - device ID;
- device type;
- firmware;
- configuration;
- lifecycle state;
- deployment assignment.

 ### Device state

 - current operational state;
- battery state;
- connectivity state;
- last contact;
- security state.

 ### Event

 - event ID;
- device ID;
- timestamp;
- event type;
- location;
- confidence;
- severity;
- processing state.

 ### Alert

 - alert ID;
- event ID;
- severity;
- notification state;
- acknowledgement;
- escalation status.

 ### Geographical rule

 - zone ID;
- geometry;
- rule type;
- activation status;
- associated policy.

 ### Monitoring policy

 - policy ID;
- sampling policy;
- event thresholds;
- communication policy;
- escalation rules.

 ### User and role information

 - user identifier;
- role;
- organizational scope;
- authorization scope.

 ### Model metadata

 - model ID;
- version;
- deployment status;
- evaluation status;
- applicable device/edge class.

 The database design should avoid storing large volumes of raw high-frequency sensor data in the primary operational tables.

---

 ## 12.6 Data Storage

 SSP requires more than one category of storage.

 The architecture therefore distinguishes between:

 **Operational data**

 and

 **Historical/raw/archival data**

 ### 12.6.1 Operational storage

 Operational data supports functions such as:

 - current device status;
- active alerts;
- current configuration;
- recent events;
- user operations;
- fleet management.

 DynamoDB is proposed for this role.

---

 ### 12.6.2 Object storage

 Large or infrequently accessed data should be stored separately.

 Amazon S3 is proposed as the reference object-storage service for:

 - historical exports;
- large datasets;
- AI training datasets;
- model artifacts;
- diagnostic files;
- archived event data;
- reports;
- system backups where appropriate.

 This separation prevents the operational database from becoming a repository for every raw artifact generated by the fleet.

---

 ### 12.6.3 Retention tiers

 SSP shall apply retention policies according to data purpose.

 A conceptual policy is:

```
Recent operational data
        ↓
Frequently accessed historical data
        ↓
Long-term archive
        ↓
Deletion according to policy
```

 Retention periods must ultimately be determined by the deployment context, legal requirements, operational needs and organizational policy.

 The design therefore does not assume that all location data should be retained indefinitely.

---

 ## 12.7 Event Processing

 The cloud event-processing architecture is based on asynchronous processing wherever immediate synchronous processing is not required.

 AWS IoT Rules can filter and route MQTT messages to other AWS services. AWS documents use cases including filtering or augmenting incoming data, storing information in databases or object storage, invoking functions, sending notifications and feeding analytics services.  AWS Documentation+1

 The SSP processing pattern is therefore:

```
Device / Edge
      │
      ▼
IoT Gateway
      │
      ▼
MQTT Message Broker
      │
      ▼
IoT Rules / Routing
      │
      ├──────────► Operational database
      │
      ├──────────► Object storage
      │
      ├──────────► Event processing
      │
      ├──────────► Alert service
      │
      └──────────► Analytics / AI
```

 The rules layer should perform lightweight routing and filtering rather than becoming the location for all business logic.

 More complex event interpretation should be implemented in dedicated backend services.

---

 ### 12.7.1 Event categories

 The cloud should distinguish at least four broad information categories:

 **Telemetry**

 Routine device and sensor information.

 **Status**

 Battery, communication, firmware and device-health information.

 **Events**

 Meaningful conditions generated by device, Edge or cloud processing.

 **Alerts**

 Operational notifications requiring attention.

 This distinction is important because transmitting or storing every telemetry record as an alert would create unnecessary communication, storage and operator load.

---

 ## 12.8 AI and Cloud Processing

 Chapter 10 established that SSP uses distributed intelligence.

 The Cloud therefore provides the computational environment for AI functions that benefit from:

 - historical data;
- fleet-wide information;
- larger computational resources;
- centralized model management;
- model training;
- model evaluation;
- cross-device analysis.

 Cloud AI should not automatically replace Device or Edge AI.

 The conceptual division remains:

 | Processing location | Typical AI function |
| --- | --- |
| Device | Lightweight motion/event preprocessing |
| Edge/Mobile | Low-latency contextual inference |
| Cloud | Historical analytics, training and fleet-level models |

The cloud should also maintain model metadata including:

 - model identifier;
- model version;
- training dataset version;
- evaluation results;
- deployment status;
- intended device/edge target;
- rollback version;
- approval status.

 This ensures that an AI result can be associated with the model version that produced it.

---

 ### 12.8.1 Model lifecycle

 The cloud AI lifecycle is:

 **Collect → Prepare → Train → Evaluate → Approve → Deploy → Monitor → Update/Roll back**

 A model shall not be deployed simply because training completed successfully.

 It must first satisfy the applicable performance and operational requirements established in Chapters 10, 11 and 15.

---

 ## 12.9 Authentication

 SSP has two fundamentally different authentication domains.

 ### Device authentication

 Devices must authenticate as authorized SSP devices before they can participate in the cloud IoT environment.

 The reference AWS architecture uses the device identity and authentication mechanisms provided by AWS IoT Core. AWS documents certificate-based device authentication and encrypted device communication through its IoT connectivity services.  AWS Documentation+1

 Each device should have an identity that is unique to that device.

 Shared credentials across the complete fleet should not be used.

---

 ### User authentication

 Human users shall authenticate through a dedicated identity-management mechanism.

 Amazon Cognito is selected as the reference user-identity service.

 The user authentication layer should support:

 - account management;
- secure authentication;
- password policies where applicable;
- multi-factor authentication where required;
- token issuance;
- session management;
- account recovery;
- integration with organizational identity systems where required.

 Cognito pricing is based on active users and identity operations, with additional costs possible for services such as SMS-based verification or MFA delivery.  Amazon Web Services, Inc.

 The precise authentication policy will depend on the deployment environment and organizational security requirements.

---

 ## 12.10 Authorization

 Authentication answers:

 > **Who are you?**

 Authorization answers:

 > **What are you allowed to do?**

 SSP therefore requires authorization after successful authentication.

 A role-based model is proposed, with possible roles including:

 - system administrator;
- security administrator;
- operational operator;
- supervisor;
- technical support;
- auditor;
- read-only user.

 Authorization should also consider **resource scope**.

 For example, an operator may be authorized to view devices assigned to a particular operational group but not devices belonging to another organization.

 The authorization model should therefore combine:

 **User → Role → Organization/Scope → Resource → Permitted operation**

 AWS IoT policies similarly provide resource-level access control over operations such as connecting, publishing and subscribing to IoT resources.  AWS Documentation

 The same least-privilege principle shall be applied to backend services and human users.

---

 ## 12.11 Security

 Cloud security is treated as an end-to-end system property.

 The major SSP cloud security boundaries are:

```
Device
  │
  │ authenticated + encrypted
  ▼
IoT Gateway
  │
  │ controlled routing
  ▼
Backend Services
  │
  ├── Operational Database
  ├── Object Storage
  ├── AI Services
  └── Monitoring
  │
  ▼
Authorized User
```

 ### 12.11.1 Encryption in transit

 Communications between devices and the cloud shall use secure transport.

 AWS IoT Core requires encrypted communication to its device gateway and supports TLS-based protection. Current AWS documentation describes TLS 1.2 and TLS 1.3 support for IoT Core communication.  AWS Documentation+1

---

 ### 12.11.2 Encryption at rest

 Sensitive stored information should be encrypted at rest using the security mechanisms provided by the selected cloud services.

 Encryption keys shall be managed separately from application data and shall be subject to appropriate access controls.

---

 ### 12.11.3 Least privilege

 Cloud identities should receive only the permissions required to perform their functions.

 For example:

 - ingestion services should not administer users;
- reporting services should not modify device credentials;
- ordinary operators should not modify security policies;
- devices should not access arbitrary cloud databases.

---

 ### 12.11.4 Secrets management

 Application secrets, credentials and cryptographic material should not be embedded directly into application source code.

 They should be stored using an appropriate managed secrets/key-management mechanism.

---

 ### 12.11.5 Auditability

 Security-sensitive actions should generate audit records, including:

 - authentication events;
- authorization failures;
- configuration changes;
- device registration;
- credential changes;
- firmware/model deployment;
- administrative operations;
- access to sensitive information.

 The audit system should itself be protected against unauthorized modification.

---

 ### 12.11.6 IoT security monitoring

 Fleet security must also be monitored.

 AWS IoT Device Defender provides cloud services for auditing IoT configurations and monitoring connected-device security characteristics. AWS describes capabilities for identifying configuration issues and detecting anomalous device behavior.  AWS Documentation+1

 However, the current AWS documentation notes an important lifecycle consideration: the Device Defender Detect feature is no longer available to new customers, while Audit remains available.  AWS Documentation

 Therefore SSP shall not make its security architecture dependent on a single vendor-specific anomaly-detection feature.

 The broader architectural requirement remains:

 **Device security state → Cloud security monitoring → Security event → Investigation/response**

---

 ## 12.12 Monitoring

 The cloud platform shall monitor both **application behavior** and **infrastructure behavior**.

 ### Application monitoring

 Metrics should include:

 - events received per second;
- alerts generated;
- alert processing latency;
- API response time;
- failed requests;
- authentication failures;
- event-processing failures;
- notification failures.

 ### Device/fleet monitoring

 Metrics should include:

 - connected devices;
- inactive devices;
- communication interruptions;
- battery warnings;
- firmware versions;
- configuration versions;
- abnormal message rates;
- device security status.

 ### Cloud infrastructure monitoring

 Metrics should include:

 - compute utilization;
- database utilization;
- storage growth;
- queue depth where applicable;
- API errors;
- service availability;
- processing latency.

 The monitoring architecture should distinguish between:

 **Operational fault**

 and

 **Security event**

 because the response to the two conditions may be different.

---

 ## 12.13 Backup and Recovery

 Cloud services must be designed so that a failure of an individual component does not result in unacceptable loss of SSP operational information.

 The recovery architecture should protect:

 - device configuration;
- monitoring policies;
- user and role information;
- event history;
- alert history;
- model metadata;
- important system logs;
- required historical data.

 DynamoDB supports point-in-time recovery and on-demand backup capabilities, while AWS Backup can be used for centralized backup strategies across supported AWS services.  Amazon Web Services, Inc.

 The exact backup strategy should be determined by the criticality and retention requirements of each data class.

---

 ### 12.13.1 Recovery objectives

 The final deployment should define:

 **RPO — Recovery Point Objective**

 The maximum acceptable amount of data that could be lost following a serious failure.

 **RTO — Recovery Time Objective**

 The maximum acceptable time required to restore the affected service.

 These values shall be derived from the operational requirements rather than selected arbitrarily.

 For example, loss of a temporary telemetry record may have a different recovery requirement from loss of a critical alert or security audit record.

---

 ### 12.13.2 Cloud outage behavior

 Cloud failure shall not automatically imply complete SSP failure.

 The architecture established in Chapter 5 provides local and Edge/Mobile fallback.

 Therefore:

```
Normal:
Device → Edge/Mobile → Cloud → User

Cloud unavailable:
Device → Edge/Mobile
             ↓
       Local decisions
       Local event storage
       Local alerts where applicable

Cloud restored:
Edge/Mobile → Secure synchronization → Cloud
```

 This is an important consequence of the distributed architecture.

 Cloud resilience is therefore complemented by **system-level resilience**.

---

 ## 12.14 Scalability

 The SSP cloud architecture shall support progressive deployment from:

 **10 devices → 100 devices → 500 devices → larger operational fleets**

 without requiring a fundamental architectural redesign.

 The primary scaling dimensions are:

 - connected devices;
- message rate;
- event rate;
- API requests;
- database operations;
- storage;
- AI processing;
- dashboard users;
- historical queries;
- device-management operations.

---

 ### 12.14.1 Device scaling

 Device registration and fleet organization should be centrally managed.

 AWS IoT Device Management provides fleet registration, organization, monitoring and remote management capabilities, including device groups and OTA-related lifecycle operations.  AWS Documentation+1

 This supports the SSP requirement that scaling device numbers should not require manually configuring every device independently.

---

 ### 12.14.2 Message scaling

 The cloud ingestion layer should be decoupled from downstream processing where necessary.

 This allows incoming device messages to be accepted and routed without requiring every backend service to process every message synchronously.

 The architecture can therefore evolve toward:

```
Device traffic
      ↓
IoT ingestion
      ↓
Message routing
      ↓
Asynchronous processing
      ├── Events
      ├── Alerts
      ├── Storage
      ├── Analytics
      └── AI
```

 This is particularly important as the fleet grows.

---

 ### 12.14.3 Database scaling

 DynamoDB on-demand capacity is proposed for the initial architecture because it removes the need to establish fixed read/write capacity before the workload is well characterized and automatically adjusts to workload changes.  AWS Documentation+1

 As the operational workload becomes predictable, the deployment can be reassessed for cost optimization.

 The important design principle is:

 > **Scale the cloud according to measured workload rather than designing the initial deployment for the maximum theoretical fleet.**

---

 ## 12.15 Estimated Cloud Costs

 Cloud cost is strongly dependent on actual usage.

 Consequently, SSP should not present a single fixed monthly cloud cost as though it were independent of fleet size and operating profile.

 The main cost drivers are expected to be:

 - device messaging;
- data transfer;
- compute execution;
- database reads/writes;
- database storage;
- object storage;
- historical-data retrieval;
- API requests;
- authentication users;
- notifications;
- AI inference;
- AI training;
- monitoring;
- backup and recovery;
- log storage.

 DynamoDB, for example, provides on-demand pricing based on consumed read/write requests and storage, while Cognito user-pool costs depend on active users and selected features.  Amazon Web Services, Inc.+1

 Therefore the cost model should be parameterized as:

 $$
C_{cloud}=C_{iot}+C_{compute}+C_{database}+C_{storage}+C_{api}+C_{identity}+C_{ai}+C_{monitoring}+C_{backup}+C_{transfer}
$$

 where each term depends on the deployment workload.

 A preliminary engineering model can be structured as:

 | Cost driver | Main variable |
| --- | --- |
| IoT ingestion | Messages/device/day |
| Compute | Function execution volume and duration |
| Database | Read/write operations and stored data |
| Object storage | GB stored and retrieved |
| API | Requests/month |
| Identity | Active users/month |
| AI | Inference/training workload |
| Monitoring | Metrics, logs and retention |
| Backup | Protected data volume |
| Network | Data transferred |

For the representative deployment scenarios, the cost analysis should initially consider:

 | Deployment | Primary purpose |
| --- | --- |
| 10 devices | Prototype/reference deployment |
| 100 devices | Small operational deployment |
| 500 devices | Pilot/medium deployment |
| Larger fleet | Production scaling analysis |

Detailed monetary estimates and total cost of ownership will be consolidated in Chapter 14 after the device, communication and workload assumptions have been finalized.

---

 ## 12.16 Cloud Architecture Decision Summary

 The principal cloud decisions established by this chapter are summarized below.

 | Decision | Selected approach | Rationale |
| --- | --- | --- |
| Cloud model | Managed cloud services | Reduces infrastructure-management burden |
| Reference provider | AWS | Strong IoT, device-management and managed-service ecosystem |
| Device ingestion | AWS IoT Core | Managed IoT gateway and message broker |
| Messaging | MQTT-oriented pub/sub | Appropriate for IoT telemetry and event communication |
| Device identity | Per-device identity | Prevents shared fleet credentials |
| Operational database | DynamoDB | Serverless NoSQL model and scalable request handling |
| Large-data storage | Object storage | Separates large/historical data from operational records |
| User identity | Cognito reference architecture | Dedicated user authentication layer |
| API architecture | Controlled HTTPS APIs | Separates frontend from backend/data stores |
| Event processing | Rules + backend services | Enables routing without coupling devices directly to databases |
| AI | Distributed | Preserves Device/Edge low-latency functions and cloud-scale training |
| Device management | Managed fleet-management layer | Supports provisioning and lifecycle management |
| Security | Identity + encryption + least privilege + audit | End-to-end security model |
| Monitoring | Application + device + cloud observability | Supports reliability and security operations |
| Backup | Managed backup/recovery mechanisms | Supports defined RPO/RTO objectives |
| Scaling | Managed/asynchronous architecture | Supports 10 → 100 → 500+ devices |

These decisions are implementation choices derived from the architecture and requirements rather than isolated technology selections.

---

 ## 12.17 Relationship with Previous Chapters

 Chapter 12 does not introduce an independent architecture.

 It implements decisions already established throughout the report.

 ### From Chapter 3 — Requirements

 The cloud architecture provides:

 - authentication;
- authorization;
- event storage;
- alerting;
- configuration;
- fleet management;
- scalability;
- resilience;
- security;
- privacy-aware storage and retention.

 ### From Chapter 4 — Market/Context

 The market analysis identified the importance of:

 - centralized monitoring;
- lifecycle management;
- privacy;
- security;
- resilience;
- integration;
- scalable fleet operation.

 These characteristics are reflected in the cloud design.

 ### From Chapter 5 — IoT Architecture

 The primary architecture remains:

 **Device → Edge/Mobile → Cloud → User**

 The cloud is therefore one layer in the complete system rather than the complete system itself.

 ### From Chapter 7 — Communication

 The cloud provides the termination point for the selected secure wide-area communication architecture and the message-ingestion mechanisms.

 ### From Chapter 8 — Software

 The backend services, APIs, authentication and frontend interfaces defined in Chapter 8 are implemented through the cloud architecture described here.

 ### From Chapter 9 — Data Flow

 The cloud provides the principal locations for:

 - operational persistence;
- historical storage;
- event processing;
- data analysis;
- data retrieval.

 ### From Chapter 10 — AI / EdgeAI

 The cloud provides:

 - model training;
- model evaluation;
- model management;
- historical analytics;
- fleet-level intelligence.

 It does not replace Edge AI where local inference is required.

 ### From Chapter 11 — Energy / Performance

 The cloud architecture supports the decision to avoid unnecessary communication and processing.

 The device and Edge layers should perform filtering and local interpretation where doing so reduces:

 - communication energy;
- communication volume;
- latency;
- cloud processing requirements.

---

 ## 12.18 Cloud-to-User Operational Flow

 The complete operational flow can now be represented as:

```
SSP Device
    │
    │ telemetry / event
    ▼
Edge / Mobile
    │
    │ filtered / contextualized information
    ▼
Secure IoT Connectivity
    │
    ▼
Cloud IoT Gateway
    │
    ▼
Message Routing
    │
    ├──► Event Processing
    │
    ├──► Operational Database
    │
    ├──► Historical Storage
    │
    ├──► Analytics / AI
    │
    └──► Device Management
              │
              ▼
        Alert / Decision Services
              │
              ▼
          Application API
              │
              ▼
        Authorized User
```

 Control information can travel in the opposite direction:

```
Authorized User
      │
      ▼
Application API
      │
      ▼
Policy / Configuration Service
      │
      ▼
Cloud IoT Layer
      │
      ▼
Edge / Mobile
      │
      ▼
SSP Device
```

 This bidirectional architecture is necessary because SSP is not merely a telemetry collection system.

 The cloud must also support controlled configuration, policy distribution, device lifecycle management and operational feedback.

---

 ## 12.19 Architectural Principle: Cloud as System-Wide Coordination Layer

 A key conclusion of this chapter is that the SSP cloud should not be understood simply as a remote database.

 It provides five major system-wide functions:

 ### 1\. Persistence

 The cloud maintains information that must survive device and Edge disconnection.

 ### 2\. Coordination

 The cloud provides centralized policies, configuration and fleet management.

 ### 3\. Aggregation

 The cloud combines information across devices and operational contexts.

 ### 4\. Intelligence

 The cloud provides historical analytics, model training and system-wide AI capabilities.

 ### 5\. Operational interface

 The cloud exposes authorized information and controls to users and external systems.

 The resulting principle is:

 > **Device and Edge provide local intelligence and resilience; Cloud provides system-wide coordination, persistence and intelligence; User interfaces provide authorized operational interaction.**

 This principle is consistent with the SSP architecture established in Chapter 5 and prevents the cloud from becoming an unnecessary single point of operational dependency.

---

 ## 12.20 Chapter 12 Conclusion

 The SSP Cloud architecture converts the conceptual Cloud layer into a concrete backend design capable of supporting the complete IoT system.

 The reference implementation uses managed AWS services to provide:

 **Secure IoT ingestion → Message routing → Event processing → Operational storage → Historical storage → AI/analytics → Device management → APIs → Authentication → Authorization → User services**

 The architecture deliberately separates device connectivity from application services and application services from databases.

 This produces several important engineering properties:

 - devices do not require direct database access;
- users do not access device infrastructure directly;
- device identity is separated from human identity;
- operational and historical data can use different storage mechanisms;
- event processing can be scaled independently;
- cloud AI can operate on system-wide information;
- Edge processing can continue when cloud connectivity is temporarily unavailable;
- fleet management can support progressive deployment;
- security controls can be applied at multiple architectural boundaries.

 The cloud architecture therefore implements the broader SSP principle:

 **Sense locally → Interpret locally → Communicate selectively → Coordinate centrally → Analyze globally → Act through authorized interfaces**

 The final cloud configuration, exact service sizing and monetary cost remain subject to workload validation. Those values will be refined through the performance and scalability analysis in Chapter 11 and consolidated into the business and total-cost analysis of Chapter 14.

 The next stage is therefore not to redesign the cloud, but to demonstrate how the complete SSP system can be implemented and exercised through the **laboratory PoC**, while maintaining the distinction between the real-world architecture and the resources available in the laboratory.

 **Requirements → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Business/Costs → Validation**

 :::
