# ESP-NETIF Architecture

<div class="text-center mb-8">

```
┌─────────────────┐
│   Application   │
├─────────────────┤
│   ESP-NETIF     │ ← Transport Independent
├─────────────────┤
│   lwIP Stack    │
├─────────────────┤
│ Driver (ETH/WiFi) │
└─────────────────┘
```

</div>

## Key Benefits
- **Transport independent** - Same API for Ethernet/WiFi
- **Multi-interface** support with automatic routing
- **Event-driven** architecture for state management