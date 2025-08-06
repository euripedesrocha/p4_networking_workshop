# WiFi Events: Implementation

<div class="grid grid-cols-2 gap-8">

<div>

### Basic Event Handler Structure
```c
static void wifi_event_handler(void *arg, 
                              esp_event_base_t event_base,
                              int32_t event_id, 
                              void *event_data) {
    if (event_base == WIFI_EVENT) {
        switch (event_id) {
            case WIFI_EVENT_STA_START:
                ESP_LOGI(TAG, "WiFi started, connecting...");
                esp_wifi_connect();
                break;
            case WIFI_EVENT_STA_CONNECTED:
                ESP_LOGI(TAG, "WiFi connected to AP");
                s_is_connected = true;
                break;
            case WIFI_EVENT_STA_DISCONNECTED:
                handle_disconnect(event_data);
                break;
            default:
                ESP_LOGI(TAG, "Unhandled WiFi event: %ld", event_id);
        }
    }
}
```

</div>

<div>

### Disconnect Handling with Reason Codes
```c
static void handle_disconnect(void *event_data) {
    wifi_event_sta_disconnected_t *event = 
        (wifi_event_sta_disconnected_t *)event_data;
    const char *reason = wifi_reason_to_string(event->reason);
    ESP_LOGW(TAG, "Disconnected from %s, reason: %s", 
             event->ssid, reason);
    s_is_connected = false;
    // Smart retry logic
    if (should_retry(event->reason) && 
        s_retry_count < s_max_retry) {
        
        vTaskDelay(pdMS_TO_TICKS(1000)); // Brief delay
        esp_wifi_connect();
        s_retry_count++;
    } else {
        ESP_LOGE(TAG, "Connection failed permanently");
        xEventGroupSetBits(s_event_group, WIFI_FAIL_BIT);
    }
}
```

</div>

</div>

