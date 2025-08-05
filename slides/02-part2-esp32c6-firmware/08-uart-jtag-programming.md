# UART/JTAG Programming Details

## UART Programming Steps

<div class="grid grid-cols-2 gap-8">

<div>

### 1. Enter Download Mode
```bash
# Hold Boot button, press Reset
# Release Reset, then Boot
# ESP32-C6 enters programming mode
```

### 2. Flash Firmware
```bash
idf.py -p /dev/ttyACM0 flash monitor

# Monitor output:
# - Boot messages
# - SDIO initialization  
# - WiFi stack startup
# - Ready for commands
```

</div>

<div>

### JTAG Programming Steps

### 1. Connect ESP-Prog
- **TMS, TCK, TDI, TDO** to ESP32-C6
- **GND** connection
- **3.3V** power (if needed)

### 2. OpenOCD Session
```bash
openocd -f interface/ftdi/esp32_devkitj_v1.cfg \
        -f target/esp32c6.cfg
```

### 3. GDB Debugging
```bash
xtensa-esp32c6-elf-gdb build/esp_hosted_ng.elf
```

</div>

</div>

**Advantage:** JTAG provides real-time debugging capabilities