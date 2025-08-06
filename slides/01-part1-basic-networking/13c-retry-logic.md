# Smart Retry: Logic Implementation

<div class="grid grid-cols-2 gap-8">

<div>

### Retry Configuration
```c
static struct {
    uint8_t current_attempt;
    uint8_t max_attempts;
    uint32_t base_delay_ms;
} s_retry = {0, 5, 1000};
```

### Decision Logic
```c
static bool should_retry(uint8_t reason) {
    switch (reason) {
        // Retry these network issues
        case WIFI_REASON_BEACON_TIMEOUT:
        case WIFI_REASON_NO_AP_FOUND:
        case WIFI_REASON_CONNECTION_FAIL:
        case WIFI_REASON_ASSOC_TOOMANY:
            return true;
        // Don't retry auth/security failures
        case WIFI_REASON_AUTH_FAIL:
        case WIFI_REASON_4WAY_HANDSHAKE_TIMEOUT:
        case WIFI_REASON_MIC_FAILURE:
            return false;
        default:
            return true; // Conservative
    }
}
```

</div>

<div>

### Disconnect Handler
```c
static void handle_disconnection(
    wifi_event_sta_disconnected_t *event) {
    ESP_LOGW(TAG, "Disconnected: reason %d", event->reason);
    s_is_connected = false;
    if (!should_retry(event->reason)) {
        ESP_LOGE(TAG, "Permanent failure");
        xEventGroupSetBits(s_event_group, WIFI_FAIL_BIT);
        return;
    }
    if (s_retry.current_attempt >= s_retry.max_attempts) {
        ESP_LOGE(TAG, "Max retries reached");
        xEventGroupSetBits(s_event_group, WIFI_FAIL_BIT);
        return;
    }
    // Exponential backoff: 1s, 2s, 4s, 8s, 16s
    uint32_t delay = s_retry.base_delay_ms << s_retry.current_attempt;
    ESP_LOGI(TAG, "Retry %d in %lu ms", 
             s_retry.current_attempt + 1, delay);
    vTaskDelay(pdMS_TO_TICKS(delay));
    esp_wifi_connect();
    s_retry.current_attempt++;
}
```

</div>

</div>
