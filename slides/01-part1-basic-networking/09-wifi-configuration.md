# Protocol Examples Common - Quickstart

<div class="grid grid-cols-2 gap-8">

<div>

### Why `protocol_examples_common`?
**Provides a quickstart point to fast start**

### What `example_connect()` Does
```c
ESP_ERROR_CHECK(example_connect());
```

**This single line handles:**

- WiFi initialization, Credential configuration, Connection establishment, Event handling, Retry logic, IP address assignment

</div>

<div>

### Configuration via Menuconfig
```
Example Connection Configuration  --->
    [*] connect using WiFi interface
    (YourSSID) WiFi SSID
    (YourPassword) WiFi Password
    [ ] connect using Ethernet interface
```

### All The Complex Stuff Hidden
Instead of 100+ lines of WiFi code, you get:
```c
ESP_ERROR_CHECK(example_connect());
    
```

### But What If You Need More?
- Custom retry strategies
- Security configuration
- Event handling for diagnostics  
- Production error recovery

</div>

</div>
