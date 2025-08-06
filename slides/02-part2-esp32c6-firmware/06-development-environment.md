# ESP-Hosted: Build Steps

## 1. Clone ESP-Hosted
```bash
idf.py create-project-from-example "espressif/esp_hosted:slave"
cd esp_hosted_slave
```

## 2. Configure for ESP32-C6
```bash
idf.py set-target esp32c6
idf.py menuconfig
```
In menuconfig, confirm that the connection type is set to SDIO (default).

## 3. Build Firmware
```bash
idf.py build
```