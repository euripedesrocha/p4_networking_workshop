# WiFi Remote: Setup Steps

<div class="grid grid-cols-2 gap-8">

<div>

## 1. Configure Credentials
```c
wifi_config_t wifi_config = {
    .sta = {
        .ssid = "Your-Network",
        .password = "Your-Password",
        .threshold.authmode = WIFI_AUTH_WPA2_PSK,
    },
};
```

</div>

<div>

## 2. Initialize & Start
```c
wifi_init_config_t cfg = WIFI_INIT_CONFIG_DEFAULT();
esp_wifi_init(&cfg);
esp_wifi_set_mode(WIFI_MODE_STA);
esp_wifi_set_config(WIFI_IF_STA, &wifi_config);
esp_wifi_start();
```

</div>

</div>

**Key Point:** Same WiFi APIs work transparently with ESP32-C6 co-processor