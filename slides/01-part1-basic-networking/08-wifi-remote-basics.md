# The Magic: WiFi Remote Component

<div class="grid grid-cols-2 gap-8">

<div>

Your `idf_component.yml` added:
```yaml
espressif/esp_wifi_remote: "^0.14.4"
```

### The Magic Architecture
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

### Why This Works
- **ESP32-C6** handles all wireless operations
- **WiFi Remote** bridges ESP32-P4 ↔ ESP32-C6
- **Standard WiFi APIs** work unchanged

### The Result
```c
esp_wifi_connect(); // Just works! ✨
```

### This architecture means your system will:
- ✅ Use standard `esp_wifi_*` APIs
- ✅ Handle events as usual
- ✅ Work with any ESP32-P4 board setup

</div>

</div>
