# Flashing Process Overview

## Programming Methods

<div class="grid grid-cols-2 gap-8">

<div>

### Method 1: UART Programming
- **USB-C cable** to ESP32-P4 board
- **Boot button** sequence required
- **Slower** but widely available
- **Standard** esp-idf flashing

```bash
idf.py -p /dev/ttyACM0 flash
```

</div>

<div>

### Method 2: JTAG Programming  
- **ESP-Prog** debugger required
- **Faster** and more reliable
- **Debug capability** included
- **Professional** development approach

```bash
openocd -f board/esp32c6.cfg
idf.py openocd-flash
```

</div>

</div>

## ESP32-P4 Function EV Board Connections
- **ESP32-C6** accessible via board connectors
- **Boot/Reset** buttons for programming mode
- **Status LEDs** for feedback
- **SDIO lines** automatically connected