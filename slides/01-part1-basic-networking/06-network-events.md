# What `example_connect()` Handles For You

<div class="grid grid-cols-2 gap-8">

<div>

## Events You DON'T Need To Handle
```c
// ✅ example_connect() handles these:
WIFI_EVENT_STA_START
WIFI_EVENT_STA_CONNECTED  
WIFI_EVENT_STA_DISCONNECTED
IP_EVENT_STA_GOT_IP
IP_EVENT_STA_LOST_IP

// ✅ Automatic retry logic
// ✅ Connection state management
// ✅ Event synchronization
```

## What Your Code Sees
```c
ESP_ERROR_CHECK(example_connect());
// ↳ Returns only when connected
// ↳ Or fails after retries
// ↳ No events to handle!
```

</div>

<div>

## When You Might Want Custom Events
```c
// For advanced applications:
void custom_event_handler(void* ctx, 
    esp_event_base_t event_base,
    int32_t event_id, void* event_data)
{
    // Custom connection monitoring
    // Application-specific logic
    // Advanced error handling
}
```

## Under The Hood
`example_connect()` contains ~150 lines of:
- Event handler registration
- WiFi initialization sequence  
- Connection retry logic
- IP address waiting
- Error recovery

**You get it all for free!**

</div>

</div>

**Philosophy:** Start simple, customize when needed