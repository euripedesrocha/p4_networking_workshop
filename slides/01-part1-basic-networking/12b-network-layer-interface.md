# Network Layer Interface Design

<div class="grid grid-cols-2 gap-8">

<div>

### Network Manager API
```c
// my_network.h
typedef enum {
    NETWORK_EVENT_GOT_IP,
    NETWORK_EVENT_LOST_IP,
} network_event_t;

typedef void (*network_event_cb_t)(network_event_t event, void *data);

// Core functions
esp_err_t my_network_init(network_event_cb_t callback);
bool my_network_has_ip(void);
esp_err_t my_network_get_ip_string(char *ip_str);
esp_err_t my_network_get_gateway_string(char *gw_str);
esp_err_t my_network_destroy(void);
```

</div>

<div>

### Application Callback Pattern
```c
void app_network_callback(network_event_t event, void *data) {
    switch (event) {
        case NETWORK_EVENT_GOT_IP:
            ESP_LOGI(TAG, "Network ready");
            // TODO: Start your network services
            break;
        case NETWORK_EVENT_LOST_IP:
            ESP_LOGW(TAG, "Network lost");
            // TODO: Pause network operations
            break;
    }
}

// TODO: Add to your app_main()
ESP_ERROR_CHECK(my_network_init(app_network_callback));
```

### Key Benefits
- **Layer 3 focus**: IP address management separate from WiFi
- **Callback-driven**: React to network state changes
- **Status queries**: Check connectivity anytime
- **Workshop task**: Implement alongside WiFi manager

</div>

</div>