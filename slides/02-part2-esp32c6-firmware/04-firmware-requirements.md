# Custom Firmware Requirements

## Development Environment Setup

<div class="grid grid-cols-2 gap-8">

<div>

### Prerequisites
- **ESP-IDF v5.1+** for ESP32-C6
- **ESP-Hosted repository** cloned
- **Toolchain** configured
- **ESP-Prog** or UART cable
- **ESP32-P4 Function EV Board**

</div>

<div>

### Key Components
- **esp_hosted_fg** - Foreground app
- **esp_hosted_ng** - Next generation  
- **SDIO interface** drivers
- **WiFi configuration** modules
- **Communication protocol** handlers

</div>

</div>

## Firmware Architecture
```
ESP32-C6 Custom Firmware
├── WiFi/BT Stack
├── ESP-Hosted Protocol Handler  
├── SDIO Communication Interface
├── Custom Feature Modules
└── Application Layer
```