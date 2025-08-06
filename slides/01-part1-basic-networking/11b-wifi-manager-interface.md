# WiFi Manager: Interface Design

<div class="grid grid-cols-2 gap-8">

<div>

### Configuration Structure
```c
// my_wifi.h
typedef struct {
    char ssid[32];          // WiFi network name
    char password[64];      // WiFi password
    uint8_t max_retry;      // Maximum connection attempts
    uint32_t timeout_ms;    // Connection timeout
} my_wifi_config_t;
```

### Core Functions
```c
// Initialize WiFi subsystem
esp_err_t my_wifi_init(const my_wifi_config_t *config);
// Start connection (blocking until success/failure)
esp_err_t my_wifi_start(void);
// Check current connection status
bool my_wifi_is_connected(void);
// Clean shutdown and resource cleanup
esp_err_t my_wifi_destroy(void);
```

</div>

<div>

### Usage Pattern
```c
void app_main(void) {
    // 1. Configure
    my_wifi_config_t config = {
        .ssid = "WorkshopWiFi",
        .password = "workshop123",
        .max_retry = 5,
        .timeout_ms = 10000
    };
    // 2. Initialize
    ESP_ERROR_CHECK(my_wifi_init(&config));
    // 3. Start (blocks until connected)
    ESP_ERROR_CHECK(my_wifi_start());
    // 4. Use connection
    if (my_wifi_is_connected()) {
        // Your application logic here
    }
    // 5. Cleanup when done
    my_wifi_destroy();
}
```

</div>

</div>

