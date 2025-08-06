# IP Events: Event Handler Implementation

<div class="grid grid-cols-2 gap-8">

<div>

### IP Event Handler
```c
static void ip_event_handler(void *arg, 
                            esp_event_base_t event_base,
                            int32_t event_id, 
                            void *event_data) {
    if (event_base == IP_EVENT) {
        switch (event_id) {
            case IP_EVENT_STA_GOT_IP: {
                ip_event_got_ip_t *event = 
                    (ip_event_got_ip_t *)event_data;
                ESP_LOGI(TAG, "Got IP: " IPSTR, 
                         IP2STR(&event->ip_info.ip));
                ESP_LOGI(TAG, "Gateway: " IPSTR, 
                         IP2STR(&event->ip_info.gw));
                s_has_ip = true;
                break;
            }
            case IP_EVENT_STA_LOST_IP:
                ESP_LOGW(TAG, "Lost IP address");
                s_has_ip = false;
                
                break;
        }
    }
}
```

</div>

<div>

### Event Registration
```c
ESP_ERROR_CHECK(esp_event_handler_instance_register(
    IP_EVENT, ESP_EVENT_ANY_ID, 
    &ip_event_handler, NULL, &instance_ip));
```

### Handler Pattern Benefits

- **State tracking**: Maintains `s_has_ip` flag
- **Application callbacks**: Notifies app layer
- **Structured logging**: Clear network information
- **Proper cleanup**: Sets state on IP loss

### Key Implementation Details

- **Event data casting**: `ip_event_got_ip_t`
- **Conservative approach**: Clear state immediately on IP loss

</div>

</div>
