 ## 7.1 Communication requirements

 Translate Chapter 3 requirements and Chapter 5 architectural decisions into communication-specific requirements:

 - range
- latency
- bandwidth
- energy
- reliability
- availability
- security
- scalability
- cost
- fallback operation

 ## 7.2 Device-level communication

 Define communication occurring within or immediately around the SSP device:

 - sensor/MCU interfaces
- internal interfaces
- local wireless interfaces
- distinction between sensor buses and external communications

 ## 7.3 Device → Edge communication

 This is the most important link for the wearable architecture.

 We will evaluate:

 - BLE
- Wi-Fi
- direct cellular
- other short-range options

 The architectural decision will be based on the Chapter 5 assumption that the **Mobile/Edge layer is an important local intelligence and connectivity point**.

 ## 7.4 Edge → Cloud communication

 Define the wide-area communication path:

 - cellular as the primary candidate
- IP connectivity
- secure application-layer communication
- event prioritization
- intermittent connectivity behavior

 ## 7.5 Cloud → User communication

 Define how operators receive:

 - status
- events
- alerts
- acknowledgements
- configuration changes

 This will primarily be an application/API communication problem rather than a new radio technology decision.

 ## 7.6 BLE / Wi-Fi / cellular / LoRa / other candidates

 Provide the technology landscape and explain why each candidate is or is not appropriate.

 ### 7.7 WBAN / WPAN / WLAN / LPWAN considerations

 Map the technologies to networking categories and explain the implications for SSP.

 ### 7.8 Protocol comparison

 Compare candidates against:

 - range
- bandwidth
- latency
- energy
- infrastructure
- reliability
- security
- cost
- mobility

 ## 7.9 Selected communication architecture

 Freeze the communication design.

 The proposed baseline is:

 **SSP Device ↔ BLE ↔ Mobile/Edge ↔ Cellular/IP ↔ Cloud ↔ Secure Internet/API ↔ User**

 with Wi-Fi available to the Mobile/Edge layer where appropriate, but **not as the fundamental protection link**.

 ## 7.10 Security

 Define communication security principles:

 - mutual/device authentication
- encryption
- integrity
- credential/key management
- replay protection
- secure provisioning
- application/API security

 ## 7.11 Communication failure modes

 Define what happens when:

 - BLE is lost
- cellular connectivity is lost
- cloud connectivity is lost
- Mobile/Edge fails
- communication quality degrades
- communication is restored

 The key principle will be:

 > **Communication failure must degrade communication capability before it degrades protection capability.**

---

 
