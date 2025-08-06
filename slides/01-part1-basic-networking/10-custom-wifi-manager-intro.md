# Time to Build Your Own Connection Manager

<div class="grid grid-cols-2 gap-8">

<div>

### You've Seen the Magic ✨
- `example_connect()` got you connected instantly
- But what's happening inside that black box?
- What if you need custom behavior?

</div>

<div>

### Production-Ready Architecture

```mermaid
graph TB
    App[Application Layer]
    Net[Network Layer - L3<br/>IP Events, DNS Config]
    WiFi[WiFi Layer - L2<br/>Connection, Security, Events]
    Driver[ESP-IDF WiFi Driver]
    
    App --> Net
    App --> WiFi  
    Net --> Driver
    WiFi --> Driver
```


</div>

</div>

