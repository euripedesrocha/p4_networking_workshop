# SDIO Communication Verification

## Testing ESP32-P4 ↔ ESP32-C6 Communication

<div class="grid grid-cols-2 gap-8">

<div>

### ESP32-P4 Side Verification
```c
// Check SDIO interface status
esp_err_t sdio_status = esp_sdio_slave_initialize();
if (sdio_status == ESP_OK) {
    ESP_LOGI(TAG, "SDIO interface ready");
}

// Test communication
esp_hosted_tx_test_packet();
```

</div>

<div>

### ESP32-C6 Side Verification  
```c
// Monitor SDIO events
void sdio_event_handler(sdio_event_t event) {
    switch(event) {
    case SDIO_EVENT_HOST_ATTACHED:
        ESP_LOGI(TAG, "Host connected");
        break;
    case SDIO_EVENT_DATA_RECEIVED:
        ESP_LOGI(TAG, "Data from host");
        break;
    }
}
```

</div>

</div>

## Verification Checklist
- ✅ **SDIO clock** signal stable (40MHz)
- ✅ **Data lines** (DAT0-DAT3) functional  
- ✅ **Command/Response** working
- ✅ **Interrupt handling** operational
- ✅ **WiFi commands** responding
- ✅ **Throughput test** passing