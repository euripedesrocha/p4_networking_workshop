# MQTT: Publish/Subscribe Messaging

<div class="grid grid-cols-2 gap-8">

<div>

## Message Flow
```
Device A ────→ MQTT Broker ────→ Device B
         publish         forward
                   ↑
            Device B subscribes
```

**Pattern:** Publisher → Broker → Subscribers

</div>

<div>

## Key Features
- **Topics** - Message routing (`sensors/temp`)
- **QoS Levels** - Delivery guarantees (0,1,2)
- **Retain** - Persistent messages
- **Last Will** - Offline detection

</div>

</div>
EOF < /dev/null