# Building Custom Firmware

## Configuration and Build Process

<div class="grid grid-cols-2 gap-8">

<div>

### Menuconfig Key Settings
```bash
# Enable custom features
Component config → ESP-Hosted
├── Enable custom AT commands
├── SDIO interface configuration  
├── WiFi advanced features
├── Performance optimizations
└── Security enhancements
```

</div>

<div>

### Build Output
```bash
idf.py build

# Generated files:
build/
├── esp_hosted_ng.bin
├── bootloader.bin
├── partition-table.bin
└── flash_download.config
```

</div>

</div>

## Custom Features Example
```c
// Custom AT command implementation
esp_err_t custom_wifi_mesh_start(void) {
    // Enable WiFi mesh functionality
    wifi_mesh_config_t config = {...};
    return esp_mesh_start(&config);
}
```

**Next:** Programming the ESP32-C6 with new firmware