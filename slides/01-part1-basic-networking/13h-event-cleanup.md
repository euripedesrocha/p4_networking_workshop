# Event Handler Cleanup & Integration

<div class="grid grid-cols-2 gap-8">

<div>

### Handler Cleanup
```c
esp_err_t unregister_event_handlers(void) {
    esp_err_t ret = ESP_OK;
    
    // Unregister WiFi handler
    if (instance_wifi_any) {
        ret = esp_event_handler_instance_unregister(
            WIFI_EVENT, ESP_EVENT_ANY_ID, instance_wifi_any);
        if (ret != ESP_OK) {
            ESP_LOGE(TAG, "Failed to unregister WiFi handler");
        }
        instance_wifi_any = NULL;
    }
    
    // Unregister IP handler
    if (instance_ip_any) {
        ret = esp_event_handler_instance_unregister(
            IP_EVENT, ESP_EVENT_ANY_ID, instance_ip_any);
        if (ret != ESP_OK) {
            ESP_LOGE(TAG, "Failed to unregister IP handler");
        }
        instance_ip_any = NULL;
    }
    
    ESP_LOGI(TAG, "Event handlers unregistered");
    return ret;
}
```

</div>

<div>

### Complete Manager Integration
```c
esp_err_t my_wifi_init(const my_wifi_config_t *config) {
    // ... initialization steps ...
    
    // Register event handlers
    ESP_ERROR_CHECK(register_event_handlers());
    
    return ESP_OK;
}

esp_err_t my_wifi_destroy(void) {
    // Unregister handlers first
    unregister_event_handlers();
    
    // Then cleanup WiFi
    esp_wifi_deinit();
    esp_netif_deinit();
    
    return ESP_OK;
}
```

### Cleanup Best Practices

- **Null checks**: Safe cleanup even if registration failed
- **Set to NULL**: Prevent double-unregister attempts
- **Error handling**: Log but continue cleanup
- **Order matters**: Unregister before WiFi deinit

</div>

</div>