# WiFi Events: Understanding the Flow

<div class="grid grid-cols-2 gap-8">

<div>

### Event-Driven Programming

**WiFi operates asynchronously - events tell you what happened**

```mermaid
sequenceDiagram
    participant App
    participant WiFi
    participant Driver
    
    App->>WiFi: my_wifi_start()
    WiFi->>Driver: esp_wifi_start()
    Driver-->>WiFi: WIFI_EVENT_STA_START
    WiFi->>Driver: esp_wifi_connect()
    Driver-->>WiFi: WIFI_EVENT_STA_CONNECTED
    Driver-->>WiFi: IP_EVENT_STA_GOT_IP
    WiFi-->>App: Connection Ready!
```

</div>

<div>

### Why Events Matter

- **Asynchronous**: WiFi connection takes time
- **Stateful**: Track connection progress  
- **Reactive**: Respond to network changes

### Connection State Management

```text
[IDLE] → [CONNECTING] → [CONNECTED] → [MONITORING]
   ↑                                        ↓
   ←──────────[DISCONNECTED]←──────────────┘
```

**Event-driven state transitions enable:**
- Non-blocking operations
- Real-time status updates
- Intelligent retry logic
- Security monitoring

</div>

</div>
