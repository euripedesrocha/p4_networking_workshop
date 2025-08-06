# IP Events: Network Status API

<div class="grid grid-cols-2 gap-8">

<div>

### Network Status Functions
```c
esp_err_t my_network_get_ip_string(char *ip_str) {
    if (!ip_str) return ESP_ERR_INVALID_ARG;
    
    if (!s_has_ip) {
        strcpy(ip_str, "0.0.0.0");
        return ESP_ERR_INVALID_STATE;
    }
    
    // Get current IP from netif
    esp_netif_t *netif = esp_netif_get_handle_from_ifkey("WIFI_STA_DEF");
    if (!netif) return ESP_FAIL;
    
    esp_netif_ip_info_t ip_info;
    ESP_ERROR_CHECK(esp_netif_get_ip_info(netif, &ip_info));
    
    snprintf(ip_str, 16, IPSTR, IP2STR(&ip_info.ip));
    return ESP_OK;
}

bool my_network_has_ip(void) {
    return s_has_ip;
}
```

</div>

<div>

### Production Usage

```c
// Quick connectivity check
if (my_network_has_ip()) {
    // Safe to start network operations
    start_http_client();
}

// Get IP for logging/debugging
char ip_str[16];
if (my_network_get_ip_string(ip_str) == ESP_OK) {
    ESP_LOGI(TAG, "Device IP: %s", ip_str);
}
```

</div>

</div>
