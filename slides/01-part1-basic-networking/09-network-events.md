# Network Events: State Management

<div class="grid grid-cols-2 gap-8">

<div>

## Key Event Types
- `IP_EVENT_STA_GOT_IP` - WiFi connected
- `IP_EVENT_ETH_GOT_IP` - Ethernet ready  
- `IP_EVENT_STA_LOST_IP` - Connection lost
- `IP_EVENT_GOT_IP6` - IPv6 available

</div>

<div>

## Event Handler Pattern
```c
void ip_event_handler(void* arg, 
    esp_event_base_t event_base,
    int32_t event_id, void* event_data)
{
    if (event_id == IP_EVENT_STA_GOT_IP) {
        // Handle IP obtained
    }
}
```

</div>

</div>

**Core concept:** Event-driven network state management