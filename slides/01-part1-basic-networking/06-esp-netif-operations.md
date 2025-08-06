# ESP-NETIF: Manual Initialization Patterns

<div class="grid grid-cols-2 gap-8">

<div>

### Manual Interface Creation
Beyond `esp_netif_create_default_wifi_sta()`:
```c
// Custom WiFi station configuration
esp_netif_config_t netif_config = ESP_NETIF_DEFAULT_WIFI_STA();
esp_netif_t* netif = esp_netif_new(&netif_config);
// Attach to WiFi driver
esp_netif_attach_wifi_station(netif);
```

### Custom Configuration
```c
// Set hostname before DHCP
esp_netif_set_hostname(netif, "my-esp32-p4");
// Configure custom DHCP behavior
esp_netif_dhcpc_option(netif, 
    ESP_NETIF_OP_SET, ESP_NETIF_DOMAIN_NAME_SERVER, 
    &dns_server, sizeof(dns_server));
```

</div>

<div>

### Status Monitoring Functions
```c
// Get IP as string (for logging)
esp_netif_ip_info_t ip_info;
esp_netif_get_ip_info(netif, &ip_info);
char ip_str[16];
snprintf(ip_str, sizeof(ip_str), IPSTR, IP2STR(&ip_info.ip));
// Check connection health
bool has_ip = (ip_info.ip.addr != 0);
ESP_LOGI(TAG, "IP: %s, Connected: %s", 
         ip_str, has_ip ? "YES" : "NO");
```

</div>

</div>
