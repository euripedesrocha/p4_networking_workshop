# Production Monitoring Implementation

<div class="grid grid-cols-2 gap-8">

<div>

### Connection Monitoring Loop
```c
void app_main_loop(void) {
    ESP_LOGI(TAG, "Starting monitoring loop");
    
    while (1) {
        bool wifi_ok = my_wifi_is_connected();
        bool network_ok = my_network_has_ip();
        
        if (wifi_ok && network_ok) {
            handle_connected_state();
        } else if (wifi_ok) {
            ESP_LOGW(TAG, "WiFi OK, waiting for IP");
        } else {
            ESP_LOGW(TAG, "WiFi disconnected");
        }
        
        vTaskDelay(pdMS_TO_TICKS(30000)); // Check every 30s
    }
}

// TODO: Add to your app_main() after connection setup
```

</div>

<div>

### State Handler & Service Management
```c
static bool s_services_running = false;

static void handle_connected_state(void) {
    char ip[16];
    my_network_get_ip_string(ip);
    ESP_LOGI(TAG, "Connected - IP: %s", ip);
    
    if (!s_services_running) {
        start_network_services();
        s_services_running = true;
    }
    // TODO: Add your application logic here
}

static void start_network_services(void) {
    ESP_LOGI(TAG, "Starting network services");
    // TODO: Start HTTP server, MQTT client, etc.
}

static void stop_network_services(void) {
    ESP_LOGW(TAG, "Stopping network services");
    s_services_running = false;
    // TODO: Cleanup network resources
}
```

### Workshop Integration
- **Monitor both layers**: WiFi + IP status
- **Service lifecycle**: Start/stop as needed
- **Add your services** in start_network_services()

</div>

</div>