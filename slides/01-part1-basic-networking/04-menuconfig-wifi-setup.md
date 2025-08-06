# Configure WiFi Settings

<div class="grid grid-cols-2 gap-8">

<div>

### 3. Set Target & Configure
```bash
idf.py set-target esp32p4
idf.py menuconfig
```

Navigate to:
**Example Connection Configuration →**

Set these values:
- ✅ **connect using WiFi interface**
- **WiFi SSID**: `[Workshop WiFi Name]`
- **WiFi Password**: `[Workshop WiFi Password]`  
- ❌ connect using Ethernet interface

</div>

<div>

### 4. Build & Flash
```bash
idf.py build
idf.py flash monitor
```

### Expected Output:
```
I (xxx) wifi_quickstart: [APP] Startup..
I (xxx) example_connect: Start example_connect.
I (xxx) example_connect: Connecting to [WiFi Name]...
I (xxx) example_connect: Connected to AP SSID:[WiFi Name]
I (xxx) example_connect: Got IPv4 address: 192.168.1.100
I (xxx) wifi_quickstart: Connected! Ready for networking
```

**Success!** WiFi connected in under 5 minutes! 🎉

</div>

</div>

**Workshop WiFi:** SSID and password will be shared during the session