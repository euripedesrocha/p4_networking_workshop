# Disconnect Reason Codes: Diagnostic Categories

<div class="grid grid-cols-2 gap-8">

<div>

**🔐 Security/Auth Issues** → Don't retry

**📡 Network Issues** → Retry with backoff  

**⚠️ Security Alerts** → Log and investigate

</div>

<div>

### Production Implementation

```c
typedef enum {
    WIFI_FAILURE_AUTH,      // Don't retry
    WIFI_FAILURE_NETWORK,   // Retry with backoff
    WIFI_FAILURE_SECURITY,  // Log and alert
    WIFI_FAILURE_UNKNOWN    // Conservative retry
} wifi_failure_category_t;

wifi_failure_category_t categorize_failure(uint8_t reason) {
    switch (reason) {
        case WIFI_REASON_AUTH_FAIL:
        case WIFI_REASON_4WAY_HANDSHAKE_TIMEOUT:
        case WIFI_REASON_MIC_FAILURE:
            return WIFI_FAILURE_AUTH;
        case WIFI_REASON_BEACON_TIMEOUT:
        case WIFI_REASON_NO_AP_FOUND:
        case WIFI_REASON_ASSOC_TOOMANY:
            return WIFI_FAILURE_NETWORK;
        default:
            return WIFI_FAILURE_UNKNOWN;
    }
}
```

</div>

</div>
