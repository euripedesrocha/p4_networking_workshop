# Disconnect Reason Codes: Essential Mapping

<div class="grid grid-cols-2 gap-8">

<div>

### Essential Reason Codes
```c
const char *wifi_reason_to_string(uint16_t reason) {
    switch (reason) {
        // Auth/Security issues (don't retry)
        case WIFI_REASON_AUTH_FAIL: 
            return "Wrong password";
        case WIFI_REASON_4WAY_HANDSHAKE_TIMEOUT: 
            return "Handshake failed";
        case WIFI_REASON_MIC_FAILURE: 
            return "Encryption error";
        case WIFI_REASON_CIPHER_SUITE_REJECTED: 
            return "Cipher rejected";
        // Network issues (retry with backoff)
        case WIFI_REASON_BEACON_TIMEOUT: 
            return "Signal lost";
        case WIFI_REASON_NO_AP_FOUND: 
            return "AP not found";
        case WIFI_REASON_ASSOC_TOOMANY: 
            return "AP overloaded";
        case WIFI_REASON_CONNECTION_FAIL: 
            return "Connection failed";
        default: return "Unknown";
    }
}
```

</div>

<div>

### Usage in Disconnect Handler
```c
static void handle_disconnect(
    wifi_event_sta_disconnected_t *event) {
    
    const char *reason = wifi_reason_to_string(event->reason);
    ESP_LOGW(TAG, "Disconnect: %s (code %d)", 
             reason, event->reason);
    
    // Use should_retry() logic
    if (should_retry(event->reason)) {
        // Implement retry with backoff
    } else {
        // Report permanent failure
    }
}
```

</div>

</div>
