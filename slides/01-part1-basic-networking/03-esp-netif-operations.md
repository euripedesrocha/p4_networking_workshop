# ESP-NETIF: Key Operations

<div class="grid grid-cols-2 gap-8">

<div>

## Interface Creation
```c
// Create network interface
esp_netif_t* netif = esp_netif_new(&config);
```

## DHCP Management
```c
// Start/stop DHCP client
esp_netif_dhcpc_start(netif);
esp_netif_dhcpc_stop(netif);
```

</div>

<div>

## IP Configuration
```c
// Set static IP
esp_netif_set_ip_info(netif, &ip_info);
```

## Status Monitoring
```c
// Get current IP info
esp_netif_get_ip_info(netif, &ip_info);
```

</div>

</div>

## Core Concept
**Same APIs work for Ethernet, WiFi, or any network interface**