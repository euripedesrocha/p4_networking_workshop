# Resource Management & Cleanup

### Production Resource Management

<div class="grid grid-cols-2 gap-8">

<div>

### Cleanup Principles

**Why Resource Cleanup Matters:**
- **Memory leaks**: FreeRTOS resources not freed
- **Handle leaks**: Event handler instances
- **Task cleanup**: Background tasks still running
- **Hardware state**: WiFi driver in inconsistent state

**Cleanup Order (Reverse of Initialization):**
```
1. Stop application services
2. Cleanup network manager
3. Cleanup WiFi manager  
4. Cleanup base systems (if needed)
```

### Error Handling Strategy
```c
esp_err_t connection_manager_destroy(void) {
    esp_err_t final_result = ESP_OK;
    esp_err_t result;
    
    ESP_LOGI(TAG, "Shutting down connection manager");
    
    // Continue cleanup even if individual steps fail
    result = my_wifi_destroy();
    if (result != ESP_OK) {
        ESP_LOGE(TAG, "WiFi cleanup failed: %s", 
                 esp_err_to_name(result));
        final_result = result; // Remember first error
    }
    
    result = my_network_destroy();
    if (result != ESP_OK) {
        ESP_LOGE(TAG, "Network cleanup failed: %s",
                 esp_err_to_name(result));
        if (final_result == ESP_OK) final_result = result;
    }
    
    return final_result;
}
```

</div>

<div>

### Complete Cleanup Implementation
```c
esp_err_t my_wifi_destroy(void) {
    ESP_LOGI(TAG, "Cleaning up WiFi manager...");
    
    // 1. Stop WiFi operations
    esp_err_t ret = esp_wifi_stop();
    if (ret != ESP_OK && ret != ESP_ERR_WIFI_NOT_INIT) {
        ESP_LOGE(TAG, "WiFi stop failed: %s", esp_err_to_name(ret));
    }
    
    // 2. Unregister event handlers
    unregister_event_handlers();
    
    // 3. Cleanup event groups
    if (s_connection_event_group) {
        vEventGroupDelete(s_connection_event_group);
        s_connection_event_group = NULL;
    }
    
    // 4. Reset state variables
    s_is_connected = false;
    s_retry_config.current_attempt = 0;
    
    ESP_LOGI(TAG, "WiFi manager cleanup complete");
    return ESP_OK;
}
esp_err_t my_network_destroy(void) {
    ESP_LOGI(TAG, "Cleaning up network manager...");
    
    // 1. Reset state
    s_has_ip = false;
    s_user_callback = NULL;
    
    // 2. Unregister IP event handler
    if (instance_ip_any) {
        esp_event_handler_instance_unregister(
            IP_EVENT, ESP_EVENT_ANY_ID, instance_ip_any);
        instance_ip_any = NULL;
    }
    
    ESP_LOGI(TAG, "Network manager cleanup complete");
    return ESP_OK;
}
```

</div>

</div>

### Cleanup Best Practices

- **Continue on errors**: Don't stop cleanup if one step fails
- **Null checks**: Safe cleanup even if initialization was partial
- **State reset**: Clear all static variables
- **Resource accounting**: Track what was allocated
- **Graceful shutdown**: Give operations time to complete