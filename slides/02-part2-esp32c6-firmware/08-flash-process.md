# Flashing ESP-Hosted Firmware

## Enter Programming Mode:
- Power the esp32p4-function-board trough the **POWER-IN** usb-c.
- Connect the ESP-Prog to your computer.
- Halt P4:
    1. Press and hold the **Boot** button.
    2. Press & Release the **Reset** button (while still holding Boot).
    3. Release the **Boot** button.
- Halt C6 (Same as above, but using the ESP-Prog Buttons.)

## Flash with:
```bash
idf.py -p /dev/ttyUSB0 flash
```
- Replace /dev/ttyUSB0 with the correct port to your ESP-Prog.