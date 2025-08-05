# Ethernet Setup: Step by Step

## 1. Configure Hardware Components

<div class="grid grid-cols-2 gap-8">

<div>

### MAC Configuration
```c
eth_mac_config_t mac_config = 
    ETH_MAC_DEFAULT_CONFIG();
```
**ESP32-P4 integrated MAC**

</div>

<div>

### PHY Configuration  
```c
eth_phy_config_t phy_config = 
    ETH_PHY_DEFAULT_CONFIG();
phy_config.phy_addr = 1;  // IP101
```
**External IP101GRI PHY**

</div>

</div>