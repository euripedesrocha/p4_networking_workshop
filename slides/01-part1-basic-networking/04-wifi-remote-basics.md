# The Magic: WiFi Remote Component

<div class="grid grid-cols-2 gap-8">

<div>

## How Did WiFi Work on ESP32-P4?
**ESP32-P4 has no WiFi radio!**

Your `idf_component.yml` added:
```yaml
espressif/esp_wifi_remote: "^0.4.0"
```

## The Magic Architecture
```
ESP32-P4          ESP32-C6-MINI-1
┌─────────────┐   ┌─────────────────┐
│ Your App    │   │                 │
│ esp_wifi_*  │   │                 │
│ APIs        │   │  WiFi 6 Radio   │
├─────────────┤   │  Bluetooth 5    │
│ WiFi Remote │◄──┤  ESP-Hosted     │
│ Component   │   │  Firmware       │
└─────────────┘   └─────────────────┘
      │ SDIO                    │
      └─────────────────────────┘
```

</div>

<div>

## Why This Works
- **ESP32-C6** handles all wireless operations
- **WiFi Remote** bridges ESP32-P4 ↔ ESP32-C6
- **Standard WiFi APIs** work unchanged
- **SDIO interface** provides high-speed connection

## Pre-configured SDIO Pins
ESP32-P4 Function EV Board:
- CLK: GPIO 43, CMD: GPIO 44
- Data: GPIO 39-42, INT: GPIO 47

## The Result
```c
esp_wifi_connect(); // Just works! ✨
```

**Your ESP32-P4 gained WiFi superpowers!**

</div>

</div>