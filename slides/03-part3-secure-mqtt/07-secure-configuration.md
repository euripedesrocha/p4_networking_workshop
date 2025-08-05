# Secure MQTT Configuration

## ESP32-P4 mTLS Implementation

<div class="grid grid-cols-2 gap-8">

<div>

### Certificate Storage
```c
// Embed certificates at compile time
extern const char ca_cert_pem_start[] asm("_binary_ca_cert_pem_start");
extern const char client_cert_pem_start[] asm("_binary_client_cert_pem_start");
extern const char client_key_pem_start[] asm("_binary_client_key_pem_start");

// Or load from NVS encrypted storage
esp_err_t load_certificates_from_nvs(void) {
    size_t cert_len;
    esp_err_t err = nvs_get_blob(nvs_handle, 
        "client_cert", client_cert, &cert_len);
    return err;
}
```

</div>

<div>

### MQTT Client Configuration
```c
esp_mqtt_client_config_t mqtt_cfg = {
    .broker = {
        .address.uri = "mqtts://broker.com:8883",
        .verification = {
            .certificate = ca_cert_pem_start,
            .skip_cert_common_name_check = false,
        }
    },
    .credentials = {
        .authentication = {
            .certificate = client_cert_pem_start,
            .key = client_key_pem_start,
        }
    }
};
```

</div>

</div>

## Security Validation
- **Certificate chain** verification against CA
- **Hostname verification** (broker.com matches certificate)
- **Certificate expiration** checking
- **Revocation status** verification (if configured)