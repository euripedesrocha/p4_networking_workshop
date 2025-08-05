# WiFi Remote Architecture

<div class="text-center mb-8">

```
ESP32-P4 (Host)        ESP32-C6 (Co-processor)
┌─────────────────┐    ┌─────────────────────────┐
│  Application    │    │                         │
│  ┌─────────────┐│    │  ┌─────────────────────┐│
│  │WiFi Remote  ││◄──►│  │    ESP-Hosted       ││
│  │   APIs      ││SDIO│  │    Firmware         ││
│  └─────────────┘│    │  └─────────────────────┘│
│  ESP-IDF Stack  │    │   Wi-Fi 6 + Bluetooth  │
└─────────────────┘    └─────────────────────────┘
```

</div>

**Key Benefits:** Transparent WiFi APIs, High-speed SDIO, Pre-programmed firmware