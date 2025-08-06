# ESP-NETIF - Recommended setup patterns

### Use default interface creation
```c
esp_netif_create_default_wifi_sta();
esp_netif_create_default_wifi_ap();
```

### Setting Interface Priority
```c
esp_netif_t* wifi_netif = esp_netif_create_default_wifi_sta();
esp_netif_t* eth_netif = esp_netif_new(ESP_NETIF_DEFAULT_ETH());

// Set priority (lower = higher priority)
esp_netif_set_route_prio(wifi_netif, 10);
esp_netif_set_route_prio(eth_netif, 20);
```
