# Quick Start: Create Project & Dependencies

### 1. Create Project
```bash
idf.py create-project networking
cd networking
```

### 2. Add Dependencies
Create `main/idf_component.yml`:
```yaml
dependencies:
  protocol_examples_common:
    path: ${IDF_PATH}/examples/common_components/protocol_examples_common
  espressif/esp_wifi_remote: "^0.14.4"
```

**That's it!** These two components give you everything you need for WiFi on ESP32-P4.
