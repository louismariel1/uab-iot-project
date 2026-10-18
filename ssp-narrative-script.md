# SmartSecurePerimeter (SSP)

## Comprehensive Oral Presentation Script

### 1. Introduction: What problem does SSP solve?

Good morning, everyone.

Today I am going to explain our project, SmartSecurePerimeter, or SSP.

I want to start with a simple situation.

Imagine that a person is subject to a legal restriction. For example, this person may be prohibited from approaching a particular house, school, or another protected location. The person wears a small electronic device that monitors their movement and location.

The objective is not simply to know where the person is. The system should also understand when the person's movement creates a risk, warn the person when appropriate, and notify an authorized security operator so that the operator can assess the situation and coordinate a response.

That is the central idea behind SSP.

SSP is an Internet of Things system. This means that physical devices collect information from the real world, communicate that information to other components, and use software to turn it into useful decisions and actions.

Our system combines four main parts.

First, there is a wearable device carried by the monitored individual.

Second, there is an edge gateway that processes information close to the person being monitored.

Third, there is a cloud back-end that stores information and performs broader analysis.

Fourth, there is a user interface that allows authorized security operators and system administrators to interact with the system.

These four parts have different responsibilities. The wearable collects information about the person and their surroundings. The gateway interprets that information in context. The cloud maintains the wider picture over time and across multiple devices. Finally, the user interface presents the relevant information to the people responsible for monitoring the situation.

The key principle is that SSP does not rely on just one component. Its functionality comes from all four parts working together.

Let us now examine each part, starting with the device worn by the monitored individual.

### 2. The wearable: How does SSP sense the real world?

The wearable is the physical component closest to the monitored individual. It needs to be small, relatively lightweight, energy-efficient, and able to operate for several days without requiring the battery to be recharged or replaced.

The wearable contains several important electronic components. Each performs a different function.

#### The microcontroller: The device's local coordinator

The first component is the microcontroller, usually abbreviated as MCU.

Think of the microcontroller as the small coordinator inside the wearable. It controls the operation of the electronic components, reads sensor measurements, executes programmed logic, manages memory, and coordinates communication.

For example, when the motion sensor produces new measurements, the microcontroller reads those measurements. It can filter out irrelevant information, identify useful features, check device status, and decide whether a local event-detection rule has been triggered.

It also controls when different components should be active or enter low-power modes.

This matters because a wearable is powered by a small battery. We cannot leave every sensor, processor, and radio operating continuously at full power if we expect the device to last for days.

The microcontroller therefore coordinates both the monitoring process and the energy-management process.

#### The motion sensor: Understanding movement

The next component is the inertial measurement unit, or IMU.

An IMU commonly contains an accelerometer and a gyroscope.

The accelerometer measures acceleration in different directions. These measurements help describe whether the device is moving, stopping, accelerating, or experiencing a sudden movement.

The gyroscope measures rotational movement. It helps the system understand changes in the orientation and rotation of the wearable.

Together, these measurements provide information about movement patterns.

For instance, the device may detect that the monitored individual has started moving after being stationary, has changed direction, or has experienced a sudden movement that deserves further analysis.

However, there is an important distinction: a motion sensor does not know where a person is. It measures movement of the device. It also cannot determine the meaning of every movement by itself.

A sudden movement might be caused by running, falling, deliberately shaking the device, or simply taking an unusual step. The system needs other information and appropriate analysis to distinguish between these possibilities.

That is why the IMU works together with the other wearable components and the processing performed by the gateway and cloud.

#### GNSS: Determining geographical location

The next component is GNSS, which stands for Global Navigation Satellite System.

GNSS is the general term for satellite-based positioning systems. GPS is one example of a GNSS system.

The GNSS receiver listens for signals transmitted by navigation satellites. By processing signals from multiple satellites, it estimates the device's geographical position.

This allows SSP to determine where the monitored individual is located relative to a configured protection zone or geofence.

A geofence is a virtual boundary defined around a geographical area. It could represent a protected residence, a school, or another location that the monitored individual must not approach or enter under the applicable policy.

The GNSS receiver provides location estimates, but it does not make the final risk decision by itself. Positioning accuracy can vary depending on satellite visibility, buildings, the environment, and other factors. It can also take time to obtain or update a position.

For this reason, SSP combines positioning information with movement measurements, recent history, configured boundaries, and the current monitoring context.

This combination makes it possible to assess more than just the person's current position.

It can help the system estimate whether the person is moving towards a protected area, how quickly they are approaching it, and whether a possible boundary violation is becoming more likely.

GNSS is therefore the source of geographical positioning information, while other parts of SSP interpret what that position means.

#### Bluetooth Low Energy: Communicating with the gateway

The wearable also includes a short-range wireless communication interface. Our selected baseline uses Bluetooth Low Energy, usually called BLE.

BLE is designed for communication between nearby electronic devices while keeping energy consumption relatively low.

The wearable uses BLE to exchange selected information with the edge gateway. This may include sensor-derived information, detected events, battery status, device health, and other relevant data.

Instead of constantly transmitting every raw sensor measurement, the wearable can filter information and send selected measurements or summaries when needed.

This reduces unnecessary communication and can help conserve battery energy.

It is important to distinguish BLE from GNSS.

GNSS helps the wearable estimate its geographical location. BLE allows the wearable to communicate locally with another device. They have different purposes.

BLE is not, by itself, a long-distance connection to the cloud. The gateway provides the next stage of communication.

#### Local memory: What happens when communication is interrupted?

The wearable also has local memory, such as internal flash storage.

Its purpose is to retain selected data and events when they cannot immediately be transmitted or when temporary buffering is useful.

Imagine that the wearable detects a relevant event while its connection to the gateway is temporarily unavailable. The device may retain information about that event so that it can be transmitted when communication becomes available again.

The wearable's memory is limited, so it is not intended to replace the cloud's persistent storage. It provides local continuity for the information the device is designed to retain.

This is one of the ways SSP can remain functional during temporary communication interruptions.

#### The battery and power-management circuitry

Another essential component is the power subsystem.

The battery supplies electrical energy to the microcontroller, motion sensor, positioning receiver, memory, and wireless interface. Power-management circuitry regulates the supply and helps monitor the battery's state.

The microcontroller and sensors can enter low-power modes when their full activity is not required. Positioning updates and wireless transmissions can be scheduled or grouped to reduce unnecessary power consumption.

The system can also increase sensing or processing activity when a higher-risk situation is detected.

This is called adaptive power management: the device adjusts its activity to the situation rather than always operating at the same level.

Our design targets a minimum battery autonomy of seven days under the defined nominal monitoring profile, with fourteen days as an extended engineering objective. These are targets to be verified, not yet demonstrated battery-life results.

#### Two wearable configurations

Our project considers two wearable configurations.

SSP Standard uses the core wearable hardware: the microcontroller, motion and positioning sensors, memory, BLE, and power-management components. It can perform essential local processing and communicate with the gateway.

SSP with AI-wearable adds a dedicated hardware module that supports selected artificial-intelligence functions directly on the wearable.

The distinction is important. The device-AI module is modular, but artificial intelligence is not optional in the overall SSP system. Both configurations use edge AI and cloud AI. The enhanced wearable adds another place where selected AI functions can execute.

The reason for offering two configurations is to balance cost, energy consumption, and the level of processing performed directly on the device.

That explains the wearable. But the wearable alone cannot do everything required by SSP. It needs another component that can combine information and assess risk.

That brings us to the edge gateway.

### 3. The edge gateway: Turning measurements into contextual decisions

The edge gateway is the local processing unit that connects the wearable to the cloud.

For our baseline design, imagine a dedicated, externally powered gateway built around a Linux-capable embedded computer. It has a processor, memory, local storage, communication interfaces, and software that manages the SSP functions assigned to the edge.

The gateway receives selected information from the wearable and combines different sources of information.

The wearable might report a geographical position, movement measurements, a detected event, and its own device status. The gateway can combine this information with recent observations, configured geofences, monitoring rules, and the current situation.

This process is called sensor fusion or contextual processing.

For example, consider two movement situations.

In the first situation, the monitored individual is moving quickly but is travelling away from a protected location.

In the second situation, the individual is moving at a similar speed but is heading directly towards that location.

Speed alone does not tell us which situation represents the greater concern. The direction of movement, current location, distance from the boundary, recent trajectory, and relevant rules all contribute to the assessment.

The gateway can bring this information together to produce a more meaningful risk estimate.

The gateway also performs local event validation. Rather than treating every unusual sensor reading as a confirmed incident, it can evaluate whether the available information supports the event and whether it meets the configured conditions for an alert.

#### What does edge AI do?

The gateway is a primary location for the system's contextual AI.

Its AI functions may process motion and location together, analyze trajectories, estimate the likelihood of an approaching geofence violation, and support contextual risk scoring.

AI can be particularly useful when interpreting patterns that are difficult to describe using a single simple threshold.

However, AI does not replace all conventional software logic. Straightforward operations, such as checking a configured boundary or determining whether a numerical threshold has been crossed, can remain deterministic. These functions behave according to explicit programmed rules.

AI supplements those functions by interpreting selected patterns and assisting with prediction or classification.

SSP therefore combines deterministic processing and distributed AI.

The design targets inference latency of no more than 200 milliseconds for selected latency-critical AI tasks. Total edge event processing has a target of no more than 500 milliseconds. These values are engineering targets to be verified during implementation and testing.

#### Why should processing happen at the edge?

There are three main reasons.

First, it reduces dependence on the cloud for time-sensitive decisions. The gateway can interpret information locally instead of waiting for every measurement to travel to a remote service and return.

Second, it can reduce unnecessary communication. The gateway can forward meaningful events and relevant summaries rather than indiscriminately transmitting every raw measurement.

Third, it helps the system continue operating when cloud connectivity is interrupted. The gateway can retain local processing and buffering functions even when it temporarily cannot communicate with the cloud.

This brings us to another critical gateway responsibility: communication and resilience.

### 4. How does the gateway communicate with the outside world?

The gateway needs a connection to the cloud back-end.

Our baseline uses Ethernet as the primary connection when a wired network is available. Wi-Fi is also supported where wired access is impractical.

But what happens if the primary connection fails?

The baseline includes cellular connectivity, using a suitable 4G or 5G service, as a failover path. The gateway monitors link availability and can switch to an alternative connection when the primary link becomes unavailable, provided the alternative is available and functioning.

This is called automatic failover.

The system can also accommodate compatible satellite backhaul for deployments where suitable terrestrial connectivity is unavailable. Satellite connectivity is an alternative for specific environments, not a requirement for every installation.

These communication options allow SSP to support different deployment conditions.

It is important, however, not to confuse communication redundancy with guaranteed uninterrupted service. Failover depends on equipment compatibility, coverage, power, link-monitoring software, and the availability of the alternative network.

#### What if every connection is lost?

Suppose the gateway temporarily loses access to the cloud.

The wearable can continue its available local monitoring and buffering functions. The gateway can continue performing its designated local analysis and buffering selected data. The system may lose access to cloud-only capabilities during the interruption, but latency-critical monitoring does not have to stop simply because the cloud connection is unavailable.

The current design specifies gateway buffering for up to twenty-four hours. When connectivity returns, queued records are synchronized with the cloud, with urgent events given priority.

Once again, the idea is to distribute responsibilities. The wearable handles local sensing and selected local functions. The gateway handles contextual processing close to the source. The cloud provides the wider, persistent, and more computationally intensive services.

Let us now examine those cloud services.

### 5. The cloud back-end: Maintaining the wider picture

The cloud back-end is the part of SSP responsible for receiving, storing, and analyzing information across time and across multiple devices.

The selected baseline uses managed public-cloud services. This means that the project intends to use cloud services for functions such as message ingestion, storage, analytics, AI, identity management, monitoring, and scaling, rather than building every infrastructure component from scratch.

When the gateway sends information to the cloud, it uses the established communication interfaces.

MQTT over TLS is the baseline for telemetry and event ingestion. MQTT is a messaging protocol suitable for sending structured information between connected components. TLS protects communication in transit.

HTTPS REST APIs support authenticated application requests and configuration functions.

After information is received, the cloud validates it and stores it in the appropriate form.

Telemetry may be stored in a time-series database, which is designed for measurements associated with timestamps. Structured records can be kept in relational storage, while object storage can retain suitable archives or larger files.

The cloud also supports alert-management services, historical analysis, device and user management, and authorized access to the information through the user interface.

#### What does cloud AI do?

Cloud AI has a different role from device-level and edge-level AI.

The cloud has access to longer-term records and can perform broader analyses that may be too demanding or unnecessary for the wearable to perform continuously.

For example, cloud AI can support historical movement analysis, spatial risk analysis, heatmaps, cross-device correlation, aggregate risk analysis, and model evaluation.

Imagine that a particular event happens once. The edge may be able to assess that event in its immediate context.

Now imagine that a security operator needs to understand patterns over several weeks or compare relevant events from multiple authorized devices. That is the kind of task for which the cloud is particularly useful.

The cloud can bring historical information together, run broader analysis, and make the resulting information available to authorized users.

This is the logic of distributed AI in SSP.

The wearable, where configured, can perform selected device-level inference. The edge performs contextual and latency-sensitive inference. The cloud performs historical, spatial, and multi-device intelligence.

These functions complement one another. They are not three unrelated AI systems.

Our initial cloud capacity target is at least one hundred active devices and at least one hundred telemetry messages per second, with a scaling path towards ten thousand active devices. The design also sets targets for API response time, event processing, and service availability. These targets must be verified through implementation and testing.

The cloud is therefore not simply a place to save data. It is a persistent information and analysis layer that helps SSP manage the wider monitoring operation.

But a system is useful only if authorized people can understand its outputs and act on them.

That is the role of the user interface.

### 6. The user interface: Putting useful information in front of people

The user interface allows authorized security operators and system administrators to interact with SSP.

Our baseline uses a React-based web dashboard. If a dedicated mobile application is required, Flutter is the selected cross-platform development approach.

The interface can present current device status, available location information, alerts, historical records, and configuration settings.

The dashboard does not make sensors or position measurements by itself. It displays information that has been collected and processed by the other components and made available through the cloud services.

For example, the operator may see the monitored device's last reported location, whether a high-priority event has been detected, relevant movement information, and the current status of the connection.

WebSockets can provide real-time updates to the dashboard. Push notifications can support mobile alert delivery where applicable.

The interface also separates different roles.

The monitored individual is the person wearing the device.

The protected person is the individual whom the arrangement is intended to protect.

A protected entity or location may be a residence, school, church, or other designated place.

The security operator or authorized authority monitors information and coordinates an appropriate response. The system administrator is responsible for authorized device, user, and policy configuration.

These roles should not be confused. The person wearing the device is not necessarily the person intended to be protected.

The user interface helps ensure that the right information reaches authorized people. It must also control who can access that information and what each user is permitted to do.

### 7. Security, privacy, and reliability across the system

Before we follow a full example, there are three important principles that apply across all the components.

The first is security.

Devices must have appropriate identities, protected communications, and authorization controls. Sensitive information must be protected in transit and at rest. Access to monitoring functions and records should be limited according to the user's role.

For example, a security operator may need to review alerts and device status, while a system administrator may also need permission to configure devices or policies. Those permissions should not automatically be identical.

The second principle is privacy.

Location and movement data can be highly sensitive. SSP should collect and transmit information required for its authorized monitoring purpose while avoiding unnecessary transfer of raw sensor data when processed or summarized information can provide the required functionality.

The third principle is reliability.

The system must handle communication interruptions, retain relevant buffered data, recover connections, identify duplicate or missing messages where possible, and prioritize urgent events.

Messages include timestamps and sequence numbers to help order records and identify gaps or duplicates.

These principles are not the responsibility of just one box in the architecture. They apply across the wearable, gateway, cloud, communication channels, and user interface.

Now that we have described the individual components, let us put them together in one example.

### 8. A complete example: A monitored individual approaches a protected location

Imagine that SSP is being used to monitor an individual who must not approach a particular residence.

For our example, that residence has been configured as a protected location. The system has a geofence representing the relevant boundary, and an authorized operator is responsible for monitoring alerts.

Let us follow the process step by step.

#### Step one: Normal monitoring

The monitored individual is moving through the neighbourhood.

The wearable's GNSS receiver estimates the device's geographical position. The IMU measures movement. The microcontroller reads these measurements, performs local processing, monitors device status, and applies the configured monitoring policy.

During normal monitoring, the system uses low-power operating modes and sends selected information over BLE to the edge gateway.

The gateway receives the information and checks it against the current location, configured geofence, recent trajectory, and other relevant context.

The information is also sent to the cloud as required by the system's messaging and reporting policy. The cloud stores the relevant records, maintains historical information, and makes authorized status information available to the operator.

At this stage, the monitored individual is not approaching the restricted boundary. The system continues normal monitoring.

#### Step two: The person starts moving towards the protected location

Now suppose the monitored individual changes direction and begins travelling towards the residence.

The GNSS receiver continues providing location estimates. The IMU provides movement measurements. Together, they help characterize the person's current movement.

The wearable sends relevant information to the gateway through BLE.

The gateway combines the reported position and movement with recent observations and the configured geofence.

The important point is that SSP does not need to wait until a boundary has already been crossed before considering whether a risk is emerging.

It can assess the direction and speed of movement, the estimated distance from the boundary, and the likely trajectory.

#### Step three: Predicting a potential violation

The gateway's contextual processing and edge AI assess whether the current trajectory indicates a likely geofence violation.

Suppose the system estimates that the individual may reach the restricted boundary within the next five minutes.

The five-minute period is a prediction about the possible future event. It is not a guarantee that the event will happen.

The system compares the available evidence with the configured risk and alert thresholds. If the required threshold is met, SSP generates a high-priority predictive alert for the security operator.

That alert may include the available location, movement direction, estimated risk, and predicted violation window.

This is more useful than simply reporting that the individual is somewhere near the residence. It gives the operator an indication of why the movement is considered relevant and how the situation may develop.

The cloud can receive the event and associated data, retain the record, and make the alert available through the authorized interface.

#### Step four: Warning the monitored individual

If the configured local warning condition is met, the wearable provides a haptic warning.

A haptic warning is a physical sensation generated by the device, such as vibration. It can notify the wearer without relying entirely on a screen or audible sound.

The purpose is to provide a timely reminder or warning to the monitored individual.

At the same time, the security operator receives the corresponding alert when the configured threshold and delivery conditions are satisfied.

This illustrates why the wearable, gateway, cloud, and user interface must work together.

The wearable can provide a local warning. The gateway provides contextual assessment. The cloud supports persistent records and broader services. The user interface informs the operator.

The system does not replace the operator's responsibility to assess the event and coordinate an appropriate response.

#### Step five: The operator reviews the alert

The operator receives the high-priority alert in the dashboard or through the supported notification channel.

The information may include the event type, timestamp, available location, movement information, and urgency.

The operator can review the current event alongside relevant historical information and the monitoring context.

If additional relevant events occur, the gateway can continue updating its local assessment, while the cloud retains the event history and makes it available to authorized users.

This helps the operator understand the situation and make an informed decision.

SSP provides information and decision support. It does not itself issue legal orders, guarantee that a violation will be prevented, or guarantee that every alert will be delivered under every possible network condition.

#### Step six: What happens if connectivity fails?

Let us add one complication.

Suppose the gateway temporarily loses its cellular connection to the cloud while the individual is approaching the boundary.

The gateway can continue its available local processing and risk assessment. The wearable can continue the local sensing and warning functions supported by its operating state and available connection. The gateway buffers selected information for later synchronization.

Cloud-dependent functions may be delayed during the interruption, but the latency-critical part of the system is designed not to depend exclusively on continuous cloud access.

When the network connection returns, the gateway synchronizes queued records with the cloud, prioritizing urgent events. Timestamps and sequence numbers help the system order records and identify gaps or duplicate messages.

The operator can then access the synchronized history through the interface, subject to the system's notification and recovery behaviour.

This example demonstrates the value of distributing functions across the system. If everything depended exclusively on the cloud, a lost connection could interrupt the entire decision process. By retaining local sensing, processing, and buffering capabilities, SSP is designed to maintain important functions during temporary disruptions.

### 9. How do all the components work together?

Let us summarize the entire sequence in words.

The GNSS receiver estimates geographical position.

The IMU measures movement.

The microcontroller coordinates the sensors, performs local processing, manages the device, and controls energy use.

The local memory retains selected information when buffering is needed.

Bluetooth Low Energy sends relevant information from the wearable to the gateway.

The edge gateway combines movement, location, recent history, and configured rules. It performs contextual processing, executes designated edge-AI functions, validates events, and can continue local processing during cloud interruptions.

Ethernet, Wi-Fi, cellular connectivity, and—where necessary—satellite backhaul provide paths between the gateway and the cloud, with failover behaviour where configured and supported.

The cloud receives messages through the defined interfaces, stores relevant records, performs historical and multi-device analysis, runs cloud-AI functions, and provides alert and application services.

The user interface presents status, events, location information, and historical records to authorized operators and administrators. Security and privacy controls govern access across the complete system.

The functionality is produced by the interaction of all these components, not by any one sensor, processor, AI model, or communication link.

### 10. Performance, battery life, and engineering trade-offs

Before concluding, it is worth explaining why some design choices involve trade-offs.

First, there is the trade-off between fast response and battery life. Increasing sensor sampling, GNSS activity, computation, and communication can improve the availability of information, but it also consumes more energy. Adaptive sensing and low-power modes are intended to balance these demands.

Second, there is the trade-off between local and cloud processing. Local processing can support faster decisions and continued operation during cloud connectivity interruptions. Cloud processing provides more storage and resources for historical, spatial, and multi-device analysis.

Third, there is the trade-off between the two wearable configurations. Adding dedicated AI hardware can enable more on-device inference, but may increase the device's cost, power consumption, and physical constraints. That is why SSP separates the modular device-AI capability from the mandatory edge and cloud AI functions.

Finally, all performance figures must be treated appropriately. For example, the wearable targets at least seven days of autonomy under the defined nominal monitoring profile, and the selected edge AI tasks target inference latency of no more than 200 milliseconds. The edge event-processing target is no more than 500 milliseconds, while the system has a high-priority end-to-end alert target of no more than five seconds.

These are engineering targets, not claims that a finished prototype has already demonstrated them. The project must verify them through component analysis, software integration, power measurements, and end-to-end testing.

### 11. Conclusion

To conclude, SmartSecurePerimeter is a distributed monitoring and risk-assessment system designed to support the monitoring of individuals and the protection of designated people and locations.

Its wearable collects movement, positioning, and device-state information while managing its limited battery energy.

The edge gateway combines those measurements with context and performs time-sensitive analysis.

The cloud provides persistent records, broader AI analysis, and services that support monitoring over time and across multiple devices.

The user interface presents useful information to authorized people, while security, privacy, and reliability mechanisms apply across the complete architecture.

The most important idea to remember is that SSP is not simply a GPS tracker.

GNSS tells the system where the device is estimated to be. The motion sensor helps describe how it is moving. The gateway combines these measurements with context. Distributed AI assists with selected classification and prediction tasks. The cloud maintains the wider picture, and the interface delivers relevant information to the operator. The wearable can also provide a local warning when the configured conditions are met.

By combining these functions, SSP is designed to move from collecting location and movement measurements towards contextual risk assessment, predictive alerts, local continuity, and coordinated human response.

Thank you for listening.
