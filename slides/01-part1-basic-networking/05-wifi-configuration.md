# Protocol Examples Common - The Foundation

<div class="grid grid-cols-2 gap-8">

<div>

## Why `protocol_examples_common`?
**Every ESP-IDF protocol example uses it:**
- HTTP client/server examples
- MQTT examples 
- WebSocket examples
- SNTP examples
- **Proven, reliable, battle-tested**

## What `example_connect()` Does
```c
ESP_ERROR_CHECK(example_connect());
```
**This single line handles:**
- WiFi initialization
- Credential configuration  
- Connection establishment
- Event handling
- Retry logic
- IP address assignment

</div>

<div>

## Configuration via Menuconfig
```
Example Connection Configuration  --->
    [*] connect using WiFi interface
    (YourSSID) WiFi SSID
    (YourPassword) WiFi Password
    [ ] connect using Ethernet interface
```

## All The Complex Stuff Hidden
Instead of 100+ lines of WiFi code, you get:
```c
void app_main(void)
{
    // System initialization
    ESP_ERROR_CHECK(nvs_flash_init());
    ESP_ERROR_CHECK(esp_netif_init());
    ESP_ERROR_CHECK(esp_event_loop_create_default());
    
    // Network connection
    ESP_ERROR_CHECK(example_connect());
    
    // Your application starts here
}
```

**Focus on your application, not WiFi plumbing!**

</div>

</div>