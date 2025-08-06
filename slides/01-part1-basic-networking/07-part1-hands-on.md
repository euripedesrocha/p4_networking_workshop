# Hands-On: Build on Your Success!

## Extend Your Working WiFi Project

<div class="grid grid-cols-2 gap-8">

<div>

### Task 1: Add Connection Info Display
Extend your working code:
```c
void app_main(void)
{
    // Your existing initialization...
    ESP_ERROR_CHECK(example_connect());
    
    // NEW: Show what you achieved
    esp_netif_t *netif = esp_netif_get_default_netif();
    esp_netif_ip_info_t ip_info;
    esp_netif_get_ip_info(netif, &ip_info);
    
    ESP_LOGI(TAG, "Connected!");
    ESP_LOGI(TAG, "IP: " IPSTR, IP2STR(&ip_info.ip));
    ESP_LOGI(TAG, "Gateway: " IPSTR, IP2STR(&ip_info.gw));
}
```

</div>

<div>

### Task 2: Prove It Works - HTTP Request
Add simple HTTP GET to verify internet:
```c
#include "esp_http_client.h"

void test_http_connection(void)
{
    esp_http_client_config_t config = {
        .url = "http://httpbin.org/get",
    };
    esp_http_client_handle_t client = esp_http_client_init(&config);
    esp_err_t err = esp_http_client_perform(client);
    
    if (err == ESP_OK) {
        ESP_LOGI(TAG, "HTTP GET successful!");
    }
    esp_http_client_cleanup(client);
}
```

</div>

</div>

## Success Criteria
- ✅ Your quick-start project displays connection info
- ✅ HTTP request proves internet connectivity  
- ✅ You understand the `protocol_examples_common` pattern
- ✅ **Ready to build any protocol application!**

**Time:** 10 minutes • **Foundation:** Your working project from slide 1!