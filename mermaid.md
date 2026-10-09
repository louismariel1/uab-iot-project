mermaid
```

flowchart TB
    CLOUD["☁️ CLOUD TIER<br/>Historical Analytics • Cloud AI • Storage • Alert Services<br/>Spatial Heatmaps • Multi-device Correlation • APIs"]

    EDGE["⚙️ EDGE TIER<br/>Event Fusion • Edge AI • Geofence Evaluation • Buffering<br/>Offline Operation • Risk Scoring • Data Filtering"]

    DEVICE["📡 DEVICE TIER<br/>Motion/Position Sensors • ULP MCU • Local Processing<br/>Local AI • Event Detection • Temporary Storage<br/>Adaptive Sensing • Device-State Monitoring"]

    PERSON(["🛡️ Protected Person / Environment"])

    CLOUD <-->|"🔒 Secure wide-area connection"| EDGE
    EDGE <-->|"📶 Low-power local connection"| DEVICE
    DEVICE --> PERSON

    classDef cloud fill:#D6EAF8,stroke:#2471A3,stroke-width:2px,color:#154360
    classDef edge fill:#D5F5E3,stroke:#239B56,stroke-width:2px,color:#145A32
    classDef device fill:#FCF3CF,stroke:#D4AC0D,stroke-width:2px,color:#7D6608
    classDef person fill:#F5B7B1,stroke:#C0392B,stroke-width:2px,color:#78281F

    class CLOUD cloud
    class EDGE edge
    class DEVICE device
    class PERSON person

    linkStyle 0 stroke:#2471A3,stroke-width:2px
    linkStyle 1 stroke:#239B56,stroke-width:2px
    linkStyle 2 stroke:#C0392B,stroke-width:2px
```
