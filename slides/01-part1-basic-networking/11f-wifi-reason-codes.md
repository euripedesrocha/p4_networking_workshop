# WiFi Disconnect Reason Codes

<div class="grid grid-cols-2 gap-8">

<div>

### Reason Code Mapping (Essential 15)

```c
static const char* wifi_reason_to_string(uint8_t reason) {
    switch (reason) {
        case WIFI_REASON_AUTH_FAIL: return "Auth failed";
        case WIFI_REASON_ASSOC_FAIL: return "Assoc failed";
        case WIFI_REASON_BEACON_TIMEOUT: return "Beacon timeout";
        case WIFI_REASON_NO_AP_FOUND: return "No AP found";
        case WIFI_REASON_CONNECTION_FAIL: return "Connection failed";
        case WIFI_REASON_4WAY_HANDSHAKE_TIMEOUT: return "Handshake timeout";
        case WIFI_REASON_MIC_FAILURE: return "MIC failure";
        case WIFI_REASON_ASSOC_TOOMANY: return "Too many stations";
        case WIFI_REASON_ASSOC_EXPIRE: return "Assoc expired";
        case WIFI_REASON_HANDSHAKE_TIMEOUT: return "Handshake timeout";
        case WIFI_REASON_CIPHER_SUITE_REJECTED: return "Cipher rejected";
        case WIFI_REASON_802_1X_AUTH_FAILED: return "802.1X failed";
        case WIFI_REASON_AUTH_EXPIRE: return "Auth expired";
        case WIFI_REASON_ROAMING: return "Roaming";
        default: return "Unknown";
    }
}
```

</div>

<div>

### Smart Retry Logic

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
        case WIFI_REASON_CIPHER_SUITE_REJECTED:
            return false;

        default:
            return true; // Conservative
    }
}
```

</div>

</div>

