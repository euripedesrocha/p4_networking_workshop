# Minimal Working Code

### 3. Replace `main/wifi_quickstart.c`

```c
#include "esp_system.h"
#include "esp_log.h"
#include "nvs_flash.h"
#include "esp_netif.h"
#include "esp_event.h"
#include "protocol_examples_common.h"
static const char *TAG = "wifi_quickstart";
void app_main(void)
{
    ESP_LOGI(TAG, "[APP] Startup..");
    // Initialize required systems
    ESP_ERROR_CHECK(nvs_flash_init());
    ESP_ERROR_CHECK(esp_netif_init());
    ESP_ERROR_CHECK(esp_event_loop_create_default());
    // Connect to WiFi
    ESP_ERROR_CHECK(example_connect());
    ESP_LOGI(TAG, "Connected! Ready for networking");
}
```


