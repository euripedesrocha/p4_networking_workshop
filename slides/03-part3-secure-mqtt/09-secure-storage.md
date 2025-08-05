# Secure Key Storage

## NVS Encryption for Credentials

<div class="grid grid-cols-2 gap-8">

<div>

### NVS Encryption Setup
```c
// Enable NVS encryption in menuconfig
CONFIG_NVS_ENCRYPTION=y
CONFIG_NVS_SEC_KEY_PROTECTION_SCHEME=1

// Initialize encrypted NVS partition
esp_err_t init_secure_storage(void) {
    nvs_sec_cfg_t cfg = {};
    esp_err_t err = nvs_flash_read_security_cfg(
        NVS_DEFAULT_PART_NAME, &cfg);
    
    if (err == ESP_ERR_NVS_SEC_KEY_NOT_FOUND) {
        // Generate new encryption key
        err = nvs_flash_generate_keys(
            NVS_DEFAULT_PART_NAME, &cfg);
    }
    
    return nvs_flash_secure_init(&cfg);
}
```

</div>

<div>

### Secure Certificate Storage
```c
// Store encrypted certificate
esp_err_t store_client_cert(const char* cert_pem) {
    nvs_handle_t nvs_handle;
    esp_err_t err = nvs_open("certificates", 
                            NVS_READWRITE, &nvs_handle);
    
    if (err == ESP_OK) {
        err = nvs_set_blob(nvs_handle, "client_cert", 
                          cert_pem, strlen(cert_pem));
        nvs_commit(nvs_handle);
        nvs_close(nvs_handle);
    }
    
    return err;
}
```

</div>

</div>

## Hardware Security Features
- **Flash encryption** - Encrypt entire firmware
- **Secure boot** - Verify firmware integrity
- **eFuse** - Hardware-based key storage  
- **Random number generator** - Hardware entropy
- **Memory protection** - Separate secure/non-secure memory