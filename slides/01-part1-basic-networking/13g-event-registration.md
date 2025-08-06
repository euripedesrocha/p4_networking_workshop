# Event Handler Registration

<div class="grid grid-cols-2 gap-8">

<div>

```c
static esp_event_handler_instance_t instance_wifi_any;
static esp_event_handler_instance_t instance_ip_any;

esp_err_t register_event_handlers(void) {
    // Register WiFi event handler
    ESP_ERROR_CHECK(esp_event_handler_instance_register(
        WIFI_EVENT,              // Event base
        ESP_EVENT_ANY_ID,        // All WiFi events
        &wifi_event_handler,     // Handler function
        NULL,                    // Handler argument
        &instance_wifi_any       // Instance handle
    ));
    // Register IP event handler  
    ESP_ERROR_CHECK(esp_event_handler_instance_register(
        IP_EVENT,               // Event base
        ESP_EVENT_ANY_ID,       // All IP events
        &ip_event_handler,      // Handler function
        NULL,                   // Handler argument
        &instance_ip_any        // Instance handle
    ));
    ESP_LOGI(TAG, "Event handlers registered");
    return ESP_OK;
}
```

</div>

<div>

### Registration Best Practices

- **Store instance handles**
- **Register early**
- **Check return values**

### Integration Example
```c
esp_err_t my_wifi_init(const my_wifi_config_t *config) {
    // Initialize event loop first
    ESP_ERROR_CHECK(esp_event_loop_create_default());
    // Register handlers before WiFi init
    ESP_ERROR_CHECK(register_event_handlers());
    // Initialize WiFi stack
    ESP_ERROR_CHECK(esp_netif_init());
    ESP_ERROR_CHECK(esp_wifi_init(&cfg));
    return ESP_OK;
}
```

### Handler Arguments

It is possible to pass context to handlers if needed for more complex implementations.

</div>

</div>
