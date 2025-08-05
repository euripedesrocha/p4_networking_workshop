# Development Environment Setup

## Step-by-Step Configuration

<div class="grid grid-cols-2 gap-8">

<div>

### 1. Clone ESP-Hosted
```bash
git clone --recursive \
  https://github.com/espressif/esp-hosted.git
cd esp-hosted/esp_hosted_ng/esp
```

### 2. Configure Build
```bash
idf.py set-target esp32c6
idf.py menuconfig
```

</div>

<div>

### 3. Key Configuration Options
- **SDIO Interface** settings
- **WiFi features** to enable
- **Custom protocol** handlers
- **GPIO pin** assignments
- **Performance** optimizations

### 4. Build Firmware
```bash
idf.py build
```

</div>

</div>

## Important Settings
- **SDIO clock frequency** (40MHz recommended)
- **Buffer sizes** for throughput optimization
- **Custom AT commands** for extended functionality