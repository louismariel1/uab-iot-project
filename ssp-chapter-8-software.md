## Chapter 8 plan — Software

 Chapter 8 should translate the frozen SSP architecture and the hardware/communication decisions from Chapters 5–7 into a **software architecture**, without prematurely moving into the detailed data-flow analysis of Chapter 9 or AI design of Chapter 10.

 The key principle will be:

 > **Chapter 5 defined where software functions live; Chapter 6 defined the computing resources available; Chapter 7 defined how those components communicate; Chapter 8 defines how the software implements the functions.**

 ### 8.1 Embedded software

 Define the firmware architecture running on the SSP device:

 - hardware abstraction
- sensor drivers
- positioning interface
- motion processing
- device-state management
- power-management control
- local event detection
- local policy execution
- BLE services
- security functions
- persistent configuration
- diagnostics
- firmware-update mechanism

 ### 8.2 Sensor acquisition

 Define how sensor data is acquired and controlled:

 - sampling
- timestamps
- synchronization
- filtering
- sensor health
- dynamic sampling
- buffering
- confidence information

 The chapter should avoid specifying AI algorithms here; those belong primarily in Chapter 10.

 ### 8.3 Device control logic

 Define the embedded state machine:

 **Boot → Initialization → Normal → Monitoring → Elevated → Critical → Communication-loss → Recovery → Update/Fault**

 This is particularly important because SSP's adaptive-energy and resilience decisions require explicit operating states.

 ### 8.4 BLE communication

 Define the application-level BLE software:

 - device discovery
- pairing/association
- services and characteristics
- telemetry
- configuration
- commands
- acknowledgements
- connection monitoring
- reconnection
- security

 The Android implementation should follow current platform requirements rather than assuming unrestricted Bluetooth access. Android currently requires appropriate Bluetooth permissions for applications targeting recent SDK levels.  Android Developers

 ### 8.5 Mobile/Edge application

 Define the mobile/edge software as an **operational edge node**, not merely a Bluetooth terminal.

 Functions include:

 - BLE gateway
- local event processing
- positioning/context acquisition where applicable
- local rules
- buffering
- connectivity monitoring
- selective forwarding
- local alerts
- configuration
- synchronization

 ### 8.6 Backend services

 Define the logical backend services without duplicating Chapter 12's detailed cloud architecture:

 - device registry
- event ingestion
- policy management
- alert management
- user/service management
- fleet monitoring
- synchronization
- audit services

 ### 8.7 APIs

 Establish two complementary API mechanisms:

 - **MQTT** for event/telemetry messaging
- **HTTPS/REST APIs** for request/response operations

 MQTT is appropriate for decoupled IoT messaging because it uses a lightweight publish/subscribe model and supports differentiated delivery QoS.  OASIS Open+1

 HTTP APIs should be formally described using OpenAPI so that mobile, frontend and backend components share an explicit interface contract. The OpenAPI specification is language-independent and supports documentation, testing and code generation.  OpenAPI Initiative Publications+1

 ### 8.8 Database software

 Define the software responsibility for persistence:

 - device metadata
- configurations
- events
- alerts
- users/roles
- audit information
- operational history

 Detailed database technology selection belongs primarily in Chapter 12.

 ### 8.9 Frontend/dashboard

 Define the operational software:

 - map/context display
- active alerts
- device status
- event history
- device health
- configuration
- audit information
- role-specific views

 ### 8.10 Authentication and authorization

 Define the software security model:

 **Identity → Authentication → Authorization → Action → Audit**

 This should cover both users and devices.

 API authorization must be enforced at object and function level rather than merely at the user-login boundary; this is consistent with the API risks identified by OWASP.  OWASP API Security Top 10+1

 ### 8.11 Software architecture

 Bring the components together using layered architecture:

 **Device software → Edge software → Backend services → APIs → Frontend**

 with cross-cutting:

 **Security + logging + configuration + monitoring + update management**

 ### 8.12 Software technology selection

 Explain the selection criteria and distinguish:

 - architecture decisions already frozen;
- software decisions made in this chapter; deliberately permits local processing to prevent every raw measurement from travellingTT's publish/subscribe architecture provides decoupling between publishers and consumers, while HTTP APIs are appropriate for resource-oriented application operations.
- implementation alternatives;
- decisions deliberately deferred to Chapters 9–12.

 A particularly important boundary is that **the real-world SSP software architecture is specified independently of the laboratory PoC**.

---

 # Chapter 8 — Software

 # 8\. Software

 ## 8.1 Embedded Software

 The SSP embedded software provides the software layer between the physical device hardware and the higher-level Device–Edge/Mobile–Cloud architecture established in Chapter 5.

 The embedded system is responsible for acquiring sensor information, controlling device operation, maintaining the device's operational state, executing time-critical local functions, managing BLE communication, implementing local policies and supporting secure device lifecycle management.

 The embedded software shall therefore not be treated simply as a collection of sensor drivers. It forms the first level of SSP intelligence and control.

 The principal software structure is:

 **Hardware → Drivers/HAL → Sensor and Device Services → Local Decision Logic → Communication Services → Security/Management**

 The firmware shall be designed so that hardware-specific implementation details are separated from application-level monitoring logic. This allows the sensing and processing architecture to evolve without requiring the complete application logic to be rewritten.

 A logical embedded-software decomposition is:

 | Software module | Main responsibility |
| --- | --- |
| Boot/start-up manager | Device initialization and controlled start-up |
| Hardware abstraction layer | Isolation of hardware-specific interfaces |
| Sensor drivers | Acquisition from physical sensors |
| Positioning service | Acquisition and management of positioning information |
| Motion service | Processing of inertial information |
| Sensor-health service | Detection of sensor faults and abnormal states |
| Time service | Timestamp generation and synchronization |
| Local event engine | Detection of defined local conditions |
| Policy engine | Application of configured monitoring rules |
| Power manager | Control of operating and low-power states |
| BLE service | Device-to-edge communication |
| Security service | Identity, authentication and protected operations |
| Configuration manager | Storage and application of device configuration |
| Diagnostics service | Health, faults and operational telemetry |
| Update manager | Secure firmware update and recovery |

The software architecture shall use well-defined interfaces between these modules.

 For example, the local event engine should consume normalized information from the sensor and positioning services rather than directly accessing individual sensor registers.

 This provides the following conceptual separation:

 **Sensor hardware → Sensor driver → Sensor service → Event engine**

 rather than:

 **Sensor hardware → Application-specific code**

 This separation improves maintainability, testing and future hardware substitution.

 ### 8.1.1 Real-time and non-real-time functions

 Not every SSP function requires identical timing behavior.

 The embedded software should therefore distinguish between:

 - time-sensitive acquisition;
- local event detection;
- communication processing;
- power-management operations;
- configuration;
- diagnostics;
- maintenance functions.

 Time-sensitive functions shall receive appropriate scheduling priority.

 For example, an abnormal device state requiring immediate local action should not be delayed behind a low-priority diagnostic upload.

 The software scheduling model shall consequently support differentiated task priorities and bounded processing times where required by the performance requirements established in Chapter 3.

 ### 8.1.2 Hardware abstraction

 The Hardware Abstraction Layer (HAL) shall isolate the application software from specific microcontroller peripherals and sensor interfaces.

 The HAL should provide common interfaces for functions such as:

 - GPIO;
- I²C;
- SPI;
- UART;
- timers;
- interrupts;
- non-volatile memory;
- power-control signals;
- communication peripherals.

 This is particularly important because Chapter 6 establishes component selections for the proposed real-world device, while the laboratory PoC may use different hardware.

 The software architecture must therefore not assume that the laboratory MCU is the permanent SSP product platform.

 ### 8.1.3 Device identity

 Each SSP device shall possess a software-accessible unique device identity.

 The identity shall be associated with:

 - device identifier;
- product/model identifier;
- firmware version;
- configuration version;
- security credentials or references to protected credentials;
- lifecycle state.

 The device identity shall be used consistently by the communication and backend layers.

 This allows the backend to distinguish:

 **Which device sent the information?**

 from:

 **What information was sent?**

 The distinction is fundamental to device management, auditability and security.

---

 ## 8.2 Sensor Acquisition

 The sensor-acquisition software shall provide a controlled interface between physical sensing components and the rest of SSP.

 The acquisition pipeline is:

 **Sensor → Driver → Sampling → Timestamp → Validation → Filtering → Normalized measurement**

 Raw measurements should not automatically be treated as valid operational information.

 The software shall therefore consider:

 - sensor availability;
- measurement range;
- invalid values;
- missing samples;
- timing irregularities;
- sensor status;
- calibration information;
- confidence or quality indicators where available.

 ### 8.2.1 Sampling control

 Sampling rates shall be configurable within the capabilities of the selected hardware.

 The system should support different acquisition profiles according to operational state.

 For example:

 | Operating state | Sensor behavior |
| --- | --- |
| Low activity | Reduced sampling |
| Normal monitoring | Standard sampling |
| Elevated condition | Increased relevant sensing |
| Critical condition | High-priority sensing and event processing |
| Communication loss | Local sensing maintained according to policy |

This implements the adaptive-monitoring principle established in Chapters 3–5.

 The objective is not simply to maximize sampling frequency.

 Instead:

 **Required information quality → Required sampling → Required computation → Energy consumption**

 ### 8.2.2 Timestamping

 Measurements and events shall be associated with timestamps.

 The software shall distinguish between:

 - sensor acquisition time;
- local processing time;
- event-generation time;
- transmission time;
- backend-reception time.

 This distinction will become important in Chapter 11 when end-to-end latency is measured.

 ### 8.2.3 Sensor validation

 Before measurements are passed to event-processing functions, the software should perform basic validation.

 Examples include:

 - range checks;
- missing-data detection;
- rate-of-change checks;
- sensor-status checks;
- consistency checks with other available measurements.

 These checks are deliberately different from AI-based anomaly detection.

 Basic validation is deterministic and should remain available even if an AI function is unavailable.

 ### 8.2.4 Position-confidence handling

 Position information shall be represented together with an indication of positioning quality where the underlying positioning subsystem provides such information.

 The embedded software shall therefore avoid representing location simply as:

 **latitude + longitude**

 when additional quality information is available.

 A logical positioning object may instead contain:

 - position;
- timestamp;
- estimated accuracy/confidence;
- source;
- validity state.

 This allows downstream decision functions to distinguish between high-confidence and uncertain positioning.

---

 ## 8.3 Device Control Logic

 SSP shall use an explicit device operating-state model rather than treating the device as continuously operating in a single mode.

 A preliminary state model is:

 **Boot → Initialization → Normal → Elevated → Critical**

 with additional transitions to:

 **Communication Loss**

 **Fault**

 **Recovery**

 **Update**

 The actual transition conditions shall be defined by the monitoring policy and validated in Chapter 15.

 ### 8.3.1 Normal state

 In the normal state the device shall perform the minimum sensing and communication necessary to satisfy the configured monitoring policy.

 The software should prioritize:

 - energy efficiency;
- routine status;
- normal sensor monitoring;
- periodic synchronization;
- health monitoring.

 ### 8.3.2 Elevated state

 An elevated state may be entered when the system identifies information requiring increased observation but not yet requiring critical intervention.

 Possible triggers include:

 - movement approaching a configured boundary;
- increasing proximity to a protected device;
- deteriorating positioning confidence;
- unusual movement;
- repeated communication degradation;
- device-state anomalies.

 The software may respond by increasing selected sensing or processing activity.

 ### 8.3.3 Critical state

 The critical state represents a condition for which immediate or high-priority action is required according to the configured operational policy.

 The software may:

 - increase relevant sensing;
- execute local event assessment;
- prioritize communication;
- generate a local event;
- preserve additional contextual information;
- request edge processing;
- trigger an alert workflow.

 The precise definition of critical conditions remains application-specific.

 ### 8.3.4 Communication-loss state

 Communication loss shall be treated as an explicit software state.

 The device shall detect relevant communication degradation and transition into a defined fallback behavior.

 Depending on the communication layer affected, the device may:

 - continue local sensing;
- buffer important events;
- attempt reconnection;
- reduce non-essential transmissions;
- preserve critical events;
- increase local decision capability.

 This supports the resilience requirements established in Chapter 3.

 ### 8.3.5 Recovery state

 Following restoration of communication or another subsystem, the device shall not immediately discard its local state.

 The recovery process should include:

 1. verification of communication;
2. synchronization;
3. transmission of buffered events;
4. configuration consistency checking;
5. return to the appropriate operational state.

 The system should avoid generating duplicate events merely because a previously buffered event is retransmitted.

 ### 8.3.6 Fault state

 A fault state shall be entered when the software detects a condition that prevents normal operation.

 The device should distinguish between:

 - recoverable faults;
- degraded operation;
- critical faults.

 Where possible, the software should maintain monitoring functionality despite individual component failures.

---

 ## 8.4 BLE Communication

 BLE provides the principal short-range software interface between the SSP device and the Edge/Mobile layer established in Chapter 5.

 The BLE implementation shall be based on an application-specific GATT structure rather than exposing raw sensor registers to the mobile application.

 A logical SSP BLE service structure may include:

 | BLE service | Example responsibility |
| --- | --- |
| Device Information Service | Device identity and firmware information |
| Telemetry Service | Selected sensor/status information |
| Event Service | Locally generated events |
| Configuration Service | Authorized configuration operations |
| Control Service | Commands from the Edge/Mobile layer |
| Diagnostic Service | Health and diagnostic information |
| Update Service | Controlled firmware-update operations |

The final service UUIDs, characteristic definitions and packet formats shall be specified during implementation.

 ### 8.4.1 BLE data categories

 BLE information should be divided into at least:

 - telemetry;
- events;
- configuration;
- commands;
- acknowledgements;
- diagnostics.

 This separation prevents a high-priority event from being treated as equivalent to routine telemetry.

 ### 8.4.2 Connection management

 The software shall manage:

 - discovery;
- connection;
- authentication/association;
- service discovery;
- characteristic configuration;
- data exchange;
- disconnection;
- reconnection.

 The device shall monitor connection state so that a lost Edge/Mobile connection can be detected.

 ### 8.4.3 BLE buffering

 Important events shall not depend exclusively on the instantaneous BLE connection.

 If the connection is temporarily unavailable, the device shall retain events according to the available local storage and configured retention policy.

 The software should therefore implement a local event queue.

 A conceptual sequence is:

 **Event generated → Local queue → BLE available? → Transmit → Acknowledge → Remove from queue**

 If BLE is unavailable:

 **Event generated → Local queue → Retry later**

 ### 8.4.4 Android interaction

 The mobile application shall use the platform BLE APIs rather than implementing Bluetooth communication through proprietary low-level mechanisms.

 Current Android documentation requires applications targeting recent Android versions to declare appropriate Bluetooth permissions, with the exact permissions depending on the target SDK and the operations performed.  Android Developers

 This is relevant to SSP because the mobile/edge software is part of the real system architecture, not merely a laboratory utility.

---

 ## 8.5 Mobile / Edge Application

 The mobile/edge application is an important SSP software component because it provides processing between the constrained device and the cloud.

 It shall not be designed merely as a BLE-to-Internet forwarding application.

 Its principal responsibilities are:

 **Device connectivity → Local context → Local processing → Data selection → Cloud communication**

 The mobile/edge software shall provide:

 - BLE device management;
- local event processing;
- temporary data storage;
- connectivity monitoring;
- local policy execution;
- local notification;
- synchronization;
- cloud communication;
- configuration management;
- device status monitoring.

 ### 8.5.1 Edge processing

 Functions that can benefit from local execution may include:

 - geofence evaluation;
- proximity interpretation;
- event filtering;
- sensor correlation;
- basic trajectory assessment;
- anomaly pre-processing;
- communication prioritization.

 The exact AI functions are intentionally not fixed in this chapter. Chapter 10 defines the AI architecture.

 ### 8.5.2 Local data buffering

 The mobile/edge layer shall provide temporary persistent storage for information that cannot immediately be forwarded.

 This allows SSP to continue operating during temporary cloud connectivity loss.

 The local store should distinguish between:

 - data that can be discarded;
- data that should be retained temporarily;
- important events that must be preserved until confirmed as delivered.

 ### 8.5.3 Data-selection logic

 The edge application shall implement the SSP principle of selective information transmission.

 For example:

 **Routine condition → summarized status**

 **Elevated condition → additional context**

 **Critical condition → event + required contextual information**

 This reduces unnecessary communication while maintaining the information required for operational decisions.

 ### 8.5.4 Local notifications

 Where the mobile/edge device is part of the operational workflow, it may generate local notifications before cloud processing completes.

 This is particularly relevant where latency or temporary cloud unavailability makes exclusive cloud-based alerting inappropriate.

---

 ## 8.6 Backend Services

 The backend software provides the centralized services required by the SSP architecture.

 The logical backend shall be decomposed into independently manageable services or modules.

 A preliminary decomposition is:

 - device registry service;
- device configuration service;
- event ingestion service;
- event processing service;
- alert service;
- user and role service;
- policy service;
- fleet-management service;
- audit service;
- notification service;
- analytics interface;
- model-management interface.

 The implementation may use a modular monolith or distributed services depending on deployment scale.

 The project does not assume that microservices are automatically preferable.

 For a small deployment, excessive service decomposition could introduce unnecessary operational complexity.

 The architecture shall therefore follow:

 > **Separate functions logically first; distribute them physically only when there is a measurable engineering benefit.**

 ### 8.6.1 Device registry

 The device registry shall maintain information such as:

 - device identifier;
- device type;
- deployment status;
- firmware version;
- configuration version;
- communication status;
- last known activity;
- lifecycle state.

 ### 8.6.2 Event ingestion

 The event-ingestion service shall receive information from Edge/Mobile nodes and make it available to downstream processing.

 It shall validate:

 - device identity;
- message structure;
- timestamps;
- message integrity;
- authorization;
- schema version.

 Malformed or unauthorized messages shall not be passed directly into operational processing.

 ### 8.6.3 Event processing

 The backend event-processing layer shall correlate incoming information with:

 - configured rules;
- device state;
- historical context;
- operational policies.

 This does not replace local processing.

 Instead, it provides system-wide processing where centralized information is beneficial.

 ### 8.6.4 Alert service

 The alert service shall transform qualifying events into operational notifications.

 It shall manage:

 - severity;
- priority;
- notification state;
- acknowledgement;
- escalation;
- delivery status;
- audit information.

---

 ## 8.7 APIs

 SSP requires two complementary API mechanisms.

 ### 8.7.1 MQTT messaging

 MQTT shall be used as a candidate primary messaging mechanism for asynchronous IoT telemetry and event exchange between suitable SSP components.

 MQTT is a lightweight client/server publish-subscribe protocol designed for environments where constrained devices and limited bandwidth are relevant considerations. It also supports multiple delivery QoS levels.  OASIS Open+1

 The conceptual SSP message structure is:

 **Device/Edge → MQTT broker → Backend consumers**

 and, where required:

 **Backend → MQTT broker → Edge/Device**

 MQTT topics should be organized according to device identity and information type.

 A conceptual hierarchy is:

```
ssp/{tenant}/{device}/telemetry
ssp/{tenant}/{device}/event
ssp/{tenant}/{device}/status
ssp/{tenant}/{device}/config
ssp/{tenant}/{device}/command
```

 The exact topic namespace shall be finalized during implementation.

 ### 8.7.2 MQTT quality of service

 Different information types should use different delivery policies.

 For example:

 | Information | Candidate treatment |
| --- | --- |
| Routine telemetry | QoS appropriate to loss tolerance |
| Device status | Reliable delivery where operationally required |
| Critical event | Reliable delivery with acknowledgement |
| Configuration command | Reliable delivery |
| Diagnostic information | Policy-dependent |

The actual QoS selection shall be validated against latency, energy and reliability measurements in Chapter 11.

 MQTT QoS selection should therefore not be made solely according to the importance label. It must also consider retransmission overhead and communication conditions.

 ### 8.7.3 HTTPS/REST API

 HTTPS/REST APIs shall be used for request/response operations that are more naturally represented as resources and transactions.

 Typical operations include:

 - user authentication;
- device registration;
- configuration management;
- policy management;
- historical event queries;
- dashboard data;
- administrative operations;
- reporting.

 The API shall use structured JSON representations unless a different representation is justified.

 ### 8.7.4 OpenAPI

 The SSP HTTP API shall be described using an OpenAPI document.

 OpenAPI provides a language-independent description of HTTP APIs and can support documentation, client/server code generation and testing.  OpenAPI Initiative Publications

 The API specification should therefore become a controlled engineering artifact rather than informal documentation.

 It shall define, as applicable:

 - endpoints;
- request schemas;
- response schemas;
- authentication requirements;
- authorization requirements;
- error responses;
- versioning;
- status codes;
- pagination;
- filtering.

 ### 8.7.5 API versioning

 The software architecture shall support API evolution without immediately breaking deployed clients.

 A versioning mechanism shall therefore be established before operational deployment.

 For example:

```
/api/v1/...
```

 The precise versioning strategy may evolve, but incompatible interface changes shall not be introduced without an explicit migration mechanism.

---

 ## 8.8 Database Software

 Database software provides persistent storage for SSP operational information.

 The software layer shall separate the logical information model from the specific database technology.

 The principal logical entities include:

 - devices;
- users;
- roles;
- policies;
- zones;
- events;
- alerts;
- configurations;
- firmware versions;
- audit records;
- deployment information.

 Detailed database technology and infrastructure selection are deferred to Chapter 12.

 ### 8.8.1 Event persistence

 Events shall contain sufficient information to reconstruct the relevant operational context.

 A conceptual event record includes:

 - event identifier;
- device identifier;
- event type;
- timestamp;
- position;
- position confidence;
- relevant movement state;
- severity;
- processing source;
- event status;
- associated policy;
- processing/version information.

 The actual schema will be defined in Chapter 9.

 ### 8.8.2 Configuration persistence

 Configurations shall be versioned.

 This allows the system to determine which policy was active when an event occurred.

 This is important because interpreting historical events against the current configuration could produce an incorrect reconstruction of the operational state.

 ### 8.8.3 Audit persistence

 Security-sensitive and operationally significant actions should generate audit records.

 Examples include:

 - login;
- configuration change;
- policy change;
- device registration;
- privilege modification;
- firmware update;
- event acknowledgement;
- alert escalation.

---

 ## 8.9 Frontend / Dashboard

 The SSP frontend provides authorized operational users with access to system information.

 The interface shall emphasize operational context rather than exposing unnecessary technical detail.

 The principal dashboard functions are:

 - active alerts;
- device status;
- map/context visualization;
- event history;
- device health;
- communication status;
- battery status;
- configuration;
- audit information.

 ### 8.9.1 Alert presentation

 An alert should provide sufficient information for the authorized operator to understand:

 - what happened;
- which device is involved;
- when it occurred;
- where it occurred;
- confidence/quality where relevant;
- severity;
- current processing state;
- available contextual information.

 The dashboard should not force the operator to reconstruct an event from multiple unrelated sensor records.

 ### 8.9.2 Map visualization

 Where geographical monitoring is applicable, the interface should support:

 - current position;
- relevant zones;
- device relationships;
- historical tracks where authorized;
- confidence/accuracy representation where useful;
- event locations.

 The presentation of sensitive historical location information shall follow the access and retention policies defined elsewhere in the SSP architecture.

 ### 8.9.3 Role-specific interface

 Different users shall see different information according to their role.

 For example:

 **Operator → alerts and operational context**

 **Administrator → configuration and device management**

 **Security administrator → security/audit information**

 **Technical support → diagnostics**

 This supports the role-based authorization requirements established in Chapter 3.

---

 ## 8.10 Authentication and Authorization

 Security is implemented across the complete software stack.

 The SSP software security model is:

 **Identity → Authentication → Authorization → Execution → Audit**

 ### 8.10.1 Device authentication

 Devices shall authenticate to the communication infrastructure using device-specific credentials or cryptographic identity mechanisms defined by the security architecture.

 The backend shall not trust a device merely because its identifier is syntactically valid.

 ### 8.10.2 User authentication

 Users shall authenticate before accessing protected SSP functions.

 The final authentication mechanism will be selected according to deployment requirements and the cloud architecture defined in Chapter 12.

 ### 8.10.3 Role-based authorization

 Authorization shall be based on defined roles and permissions.

 The system should enforce both:

 - function-level authorization;
- object-level authorization.

 For example, permission to access a device-management function does not automatically imply permission to access every device.

 This distinction is important because OWASP identifies broken object-level and function-level authorization among major API security risks.  OWASP API Security Top 10

 ### 8.10.4 Least privilege

 Software components should operate with only the permissions necessary for their functions.

 This principle applies to:

 - embedded tasks;
- mobile application permissions;
- backend services;
- database accounts;
- API clients;
- administrative users.

 ### 8.10.5 Session and token management

 Where token-based authentication is used, the software shall provide:

 - controlled token lifetime;
- secure storage;
- revocation/expiry mechanisms;
- authorization checks;
- protection against replay where applicable.

 The exact identity architecture is specified further in Chapter 12.

 ### 8.10.6 API security

 The API layer shall validate:

 - authentication;
- authorization;
- input structure;
- object ownership/permission;
- resource limits;
- request validity.

 OWASP's API security guidance emphasizes that APIs expose sensitive application logic and data and therefore require security controls specifically addressing API-level risks.  OWASP API Security Top 10+1

---

 ## 8.11 Software Architecture

 The complete SSP software architecture can be represented as:

```
┌─────────────────────────────────────────────────────┐
│                    USER SOFTWARE                    │
│                                                     │
│  Operational Dashboard / Mobile Interface / Admin   │
└───────────────────────┬─────────────────────────────┘
                        │ HTTPS / API
                        │
┌───────────────────────▼─────────────────────────────┐
│                  CLOUD SOFTWARE                     │
│                                                     │
│ API Gateway / Backend Services / Event Processing   │
│ Device Management / Alerting / Policy / Audit       │
│ Persistence / Analytics / Integration Interfaces    │
└───────────────────────┬─────────────────────────────┘
                        │ MQTT / HTTPS
                        │
┌───────────────────────▼─────────────────────────────┐
│                 EDGE / MOBILE SOFTWARE              │
│                                                     │
│ BLE Gateway / Local Processing / Buffering           │
│ Connectivity Management / Local Policy / Alerts     │
│ Synchronization / Selective Data Forwarding         │
└───────────────────────┬─────────────────────────────┘
                        │ BLE
                        │
┌───────────────────────▼─────────────────────────────┐
│                 DEVICE SOFTWARE                     │
│                                                     │
│ HAL / Drivers / Sensor Services / Positioning       │
│ Motion Processing / Event Engine / Power Manager     │
│ BLE / Security / Configuration / Diagnostics        │
└───────────────────────┬─────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────┐
│                     HARDWARE                        │
│                                                     │
│ Sensors / MCU / Memory / Radio / Power / Battery    │
└─────────────────────────────────────────────────────┘
```

 This software structure directly implements the frozen SSP architectural principle:

 **Device → Edge/Mobile → Cloud → User**

 while allowing feedback and control information to travel in the opposite direction.

 ### 8.11.1 Control path

 The system shall support a reverse control path:

 **User → Cloud → Edge/Mobile → Device**

 for authorized functions such as:

 - configuration;
- policy changes;
- device commands;
- operational acknowledgements;
- software-update instructions.

 ### 8.11.2 Data path

 The primary information path is:

 **Device → Edge/Mobile → Cloud → User**

 However, the software architecture deliberately permits local processing to prevent every raw measurement from travelling through the complete chain.

 The resulting principle is:

 > **Data should travel only as far as necessary for the function being performed.**

 ### 8.11.3 Cross-cutting software services

 The following functions span multiple layers:

 - authentication;
- authorization;
- logging;
- monitoring;
- configuration;
- software updates;
- time synchronization;
- error handling;
- version management.

 They shall therefore be treated as cross-cutting architecture elements rather than isolated application features.

---

 ## 8.12 Software Technology Selection

 The software technology selection follows the same engineering principle established in Chapter 4:

 > A technology is selected because it satisfies the SSP requirements, not because it is fashionable or widely used.

 The principal selection criteria are:

 - reliability;
- energy consumption;
- latency;
- maintainability;
- security;
- interoperability;
- development effort;
- ecosystem maturity;
- scalability;
- testing capability;
- lifecycle support.

 ### 8.12.1 Embedded software technology

 The embedded software shall use a resource-appropriate firmware architecture.

 Depending on the selected MCU/SoC and workload, this may use:

 - a lightweight bare-metal architecture;
- a real-time operating system;
- vendor-supported SDK components;
- a combination of these.

 The final choice shall be validated against the hardware selected in Chapter 6.

 For SSP, the principal requirement is deterministic and maintainable control of:

 - sensing;
- power;
- BLE;
- local processing;
- security;
- device state.

 ### 8.12.2 Mobile software technology

 The mobile/edge application shall be implemented using the platform-native Android software stack for the target deployment where Android is selected as the Edge/Mobile platform.

 This provides access to:

 - BLE APIs;
- local storage;
- network APIs;
- background processing mechanisms;
- notification mechanisms;
- device connectivity management.

 The Android platform imposes explicit permission and lifecycle constraints that must be incorporated into the design rather than treated as implementation details.  Android Developers

 ### 8.12.3 Backend technology

 The backend shall use a technology stack capable of supporting:

 - concurrent event ingestion;
- secure APIs;
- asynchronous processing;
- database access;
- authentication;
- observability;
- automated testing.

 The precise programming language and framework should be selected after the cloud deployment model is established in Chapter 12.

 ### 8.12.4 API technology

 The SSP software architecture shall use:

 **MQTT → asynchronous IoT messaging**

 **HTTPS/REST → request/response application API**

 This separation prevents a single protocol from being forced to satisfy fundamentally different communication patterns.

 MQTT's publish/subscribe architecture provides decoupling between publishers and consumers, while HTTP APIs are appropriate for resource-oriented application operations.  OASIS Open+1

 ### 8.12.5 Frontend technology

 The frontend shall use a web-based application architecture unless a deployment-specific requirement justifies a native application.

 The important architectural requirements are:

 - responsive operational interface;
- role-based access;
- secure API integration;
- map support;
- real-time or near-real-time event updates;
- historical visualization;
- auditability.

 The specific frontend framework is therefore an implementation choice rather than an architectural requirement.

---

 ## 8.13 Software Update and Lifecycle Management

 Software lifecycle management is a fundamental SSP requirement.

 The software architecture shall support controlled updates for:

 - device firmware;
- Edge/Mobile software;
- backend services;
- frontend software;
- configuration;
- AI models where applicable.

 ### 8.13.1 Firmware updates

 Device firmware updates shall be authenticated and integrity-protected.

 The update process should support:

 1. update availability;
2. authorization;
3. package verification;
4. installation;
5. validation;
6. activation;
7. rollback or recovery where required.

 NIST IoT guidance identifies software-update capability as an important cybersecurity mechanism because updates enable vulnerabilities and operational defects to be remediated after deployment.  NIST Publications

 ### 8.13.2 Configuration versioning

 Configuration shall be version-controlled independently of firmware where possible.

 This allows the same firmware to support different authorized operational configurations.

 ### 8.13.3 Model versioning

 AI models shall also be versioned.

 A later chapter will define the model-management process in greater detail, but the software architecture must already support:

 **Model identity → Version → Deployment → Monitoring → Rollback**

 ### 8.13.4 Compatibility management

 Software components shall communicate using versioned interfaces.

 The system should detect incompatible versions rather than silently accepting malformed or semantically incompatible messages.

---

 ## 8.14 Logging, Diagnostics and Observability

 Operational software shall generate sufficient information to determine whether SSP is functioning correctly.

 The software shall distinguish between:

 - operational events;
- security events;
- diagnostic events;
- communication events;
- system errors;
- performance measurements.

 ### 8.14.1 Embedded diagnostics

 The device should expose:

 - battery state;
- firmware version;
- sensor status;
- communication status;
- fault state;
- reset information;
- configuration version.

 ### 8.14.2 Edge diagnostics

 The Edge/Mobile layer should expose:

 - BLE connection state;
- connected devices;
- synchronization state;
- cloud connectivity;
- local queue depth;
- processing failures;
- application health.

 ### 8.14.3 Backend observability

 Backend software should monitor:

 - API availability;
- event-ingestion rate;
- processing latency;
- queue depth;
- database health;
- service failures;
- authentication failures;
- alert-delivery state.

 These measurements will provide the evidence required for the performance and reliability evaluation in Chapter 11.

---

 ## 8.15 Software Error Handling

 Software failures shall not automatically result in complete system failure.

 The software architecture shall distinguish between:

 **Error → Recovery → Degraded operation → Critical failure**

 Examples include:

 - temporary BLE disconnection;
- temporary cloud disconnection;
- malformed sensor measurement;
- invalid configuration;
- backend service failure;
- unavailable AI model;
- database interruption.

 Where a function is not essential to immediate protection, it may be temporarily disabled while critical monitoring remains operational.

 For example, failure of a historical analytics service should not prevent the device from generating a critical local event.

 This reflects the SSP principle of graceful degradation.

---

 ## 8.16 Relationship Between Software and the AI Layer

 AI is intentionally separated from the basic software architecture.

 The software architecture must remain operational even if a machine-learning model is unavailable.

 The relationship is therefore:

 **Core software → provides reliable sensing and deterministic control**

 **AI layer → provides additional interpretation where justified**

 This separation prevents AI from becoming an uncontrolled single point of failure.

 The AI subsystem defined in Chapter 10 may consume features produced by:

 - device software;
- Edge/Mobile software;
- backend preprocessing.

 It may return:

 - classification;
- anomaly score;
- prediction;
- confidence/uncertainty;
- contextual assessment.

 The core software shall then decide how that output is used according to defined policies.

 A low-confidence AI output shall not automatically override a deterministic safety or security rule.

---

 ## 8.17 Relationship Between Software and Data Flow

 Chapter 8 defines the software components responsible for processing information.

 Chapter 9 will define the information itself.

 The distinction is:

 **Chapter 8: Who/what software performs the operation?**

 **Chapter 9: What information moves through the system?**

 For example:

 **Device software**

 acquires an accelerometer measurement.

 **Chapter 9**

 defines the measurement's representation, processing, transmission and storage.

 Similarly:

 **Edge software**

 executes a geofence evaluation.

 **Chapter 9**

 defines the input data, derived event and resulting transmitted information.

 This separation prevents duplication between the two chapters.

---

 ## 8.18 Relationship Between Software and Cloud Architecture

 Chapter 8 defines the logical software responsibilities.

 Chapter 12 will define the detailed cloud implementation.

 Therefore, Chapter 8 specifies:

 - backend responsibilities;
- API roles;
- service boundaries;
- software interactions;
- security principles;
- data-processing responsibilities.

 Chapter 12 will subsequently specify:

 - cloud deployment model;
- infrastructure;
- database technology;
- API gateway;
- compute services;
- storage;
- monitoring;
- backup;
- scaling;
- cloud cost.

 This preserves the distinction between **software architecture** and **cloud infrastructure architecture**.

---

 ## 8.19 Software Design Decisions

 The principal software decisions resulting from this chapter are summarized below.

 | Decision | Rationale |
| --- | --- |
| Use layered embedded firmware | Separates hardware dependencies from application logic |
| Use explicit device operating states | Supports adaptive monitoring and resilience |
| Perform deterministic local processing | Provides low-latency functions without cloud dependency |
| Use BLE as the device application interface | Matches the Device–Edge/Mobile architecture |
| Implement an Edge/Mobile software layer | Supports local processing, buffering and selective communication |
| Use MQTT for asynchronous IoT messaging | Suitable for decoupled, lightweight IoT communication  OASIS Open |
| Use HTTPS/REST for application APIs | Appropriate for request/response operations |
| Describe HTTP APIs with OpenAPI | Provides a machine-readable interface contract  OpenAPI Initiative Publications |
| Use role-based authorization | Controls access according to operational responsibility |
| Enforce object-level authorization | Prevents authorization from being limited to endpoint access |
| Implement local event buffering | Supports communication-loss operation |
| Version configurations and interfaces | Supports controlled lifecycle evolution |
| Support secure software updates | Required for lifecycle security and vulnerability remediation  NIST Publications |
| Keep AI separate from core control | Prevents AI failure from becoming a critical system failure |
| Separate software architecture from PoC implementation | Preserves the real-world design independently of laboratory resources |

---

 ## 8.20 Software Architecture and the Frozen SSP Design

 The software decisions in this chapter are a direct consequence of the architectural decisions established previously.

 The resulting chain is:

 **Chapter 4 — Context**

 Existing systems demonstrate the value of positioning, BLE, centralized monitoring, contingency behavior and connected devices.

 ↓

 **Chapter 5 — Architecture**

 SSP adopts:

 **Device → Edge/Mobile → Cloud → User**

 ↓

 **Chapter 6 — Hardware**

 The device therefore requires sufficient embedded processing, sensing, memory, BLE and power-management capability to execute its local software responsibilities.

 ↓

 **Chapter 7 — Communication**

 BLE provides the local device connection, while wide-area/network communication provides the Edge/Mobile–Cloud path.

 ↓

 **Chapter 8 — Software**

 The software now implements these architectural boundaries through:

 **Embedded firmware → Mobile/Edge application → Backend services → APIs → Frontend**

 The important point is that the software architecture was not selected independently.

 It is the software realization of the decisions already established by the system architecture.

---

 ## 8.21 Laboratory PoC Relationship

 The software defined in this chapter describes the **real-world SSP system**.

 The laboratory PoC in Chapter 13 may implement only a subset of this software architecture.

 For example, the real system may contain:

 **Specialized SSP device → Edge/Mobile → MQTT/HTTPS backend → operational dashboard**

 while the PoC may implement:

 **Generic MCU/SoC → BLE → Android application → simplified server**

 The PoC is therefore permitted to substitute implementation technologies while preserving the same conceptual chain.

 The mapping will be explicitly documented in Chapter 13.

 This prevents the laboratory implementation from becoming an accidental definition of the final product.

---

 ## 8.22 Chapter 8 Conclusion

 The SSP software architecture implements the distributed Device–Edge/Mobile–Cloud architecture established in Chapter 5.

 The resulting software chain is:

 **Embedded Firmware → BLE → Mobile/Edge Software → MQTT/HTTPS → Backend Services → Database/API → Frontend**

 The principal design principle is that processing should occur at the layer where it provides the greatest measurable benefit.

 Accordingly:

 - device software performs time-sensitive and resource-aware local functions;
- Edge/Mobile software performs local interpretation, buffering and selective communication;
- backend software performs centralized processing, fleet management and system-wide coordination;
- frontend software provides authorized operational interaction.

 The architecture also establishes a deliberate separation between deterministic system functions and AI-based functions.

 AI can enhance event interpretation, prediction and anomaly detection, but the core SSP software shall remain capable of maintaining critical monitoring functions when AI is unavailable or uncertain.

 The communication architecture is similarly reflected in the software design:

 **BLE → local device communication**

 **MQTT → asynchronous IoT messaging**

 **HTTPS/REST → application/API operations**

 **OpenAPI → API contract**

 MQTT provides a lightweight publish/subscribe mechanism appropriate to IoT communication, while OpenAPI provides a formal description of the HTTP API surface.  OASIS Open+1

 Security is treated as a software-wide property encompassing device identity, authentication, authorization, API protection, configuration, logging and software updates. This is particularly important because APIs expose application logic and potentially sensitive information and therefore require dedicated authorization and security controls.  OWASP API Security Top 10+1

 **Generated → Acquired → Processed → Transmitted → Stored → Analyzed → Presented → Acted upon**

 Chapter 9 will therefore describe not primarily which software performs each function, but **what information moves through the SSP system, how it is transformed, where it is stored and how privacy and information minimization are maintained throughout the complete lifecycle**.\
 :::
