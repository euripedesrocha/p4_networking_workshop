# Ethernet Setup: Driver Creation

## 2. Create Driver Components

```c
// Create MAC and PHY instances
esp_eth_mac_t *mac = esp_eth_mac_new_esp32(&mac_config);
esp_eth_phy_t *phy = esp_eth_phy_new_ip101(&phy_config);

// Install Ethernet driver
esp_eth_config_t config = ETH_DEFAULT_CONFIG(mac, phy);
esp_eth_driver_install(&config, &eth_handle);
```

## Key Point
**Three components: MAC (integrated) + PHY (external) + Driver (glue)**