# Certificate Validation & Pinning

## Advanced Validation Techniques

<div class="grid grid-cols-2 gap-8">

<div>

### Certificate Pinning
```c
// Pin specific certificate or public key
const char* pinned_cert_sha256 = 
    "A1:B2:C3:D4:E5:F6:07:08:09:0A:1B:2C:3D:4E:5F:60";

esp_err_t validate_server_cert(mbedtls_x509_crt* cert) {
    // Calculate certificate fingerprint
    unsigned char fingerprint[32];
    mbedtls_sha256_ret(cert->raw.p, cert->raw.len, 
                       fingerprint, 0);
    
    // Compare with pinned value
    return memcmp(fingerprint, expected_sha256, 32);
}
```

</div>

<div>

### Custom Validation Callback
```c
int custom_cert_verify(void *data, mbedtls_x509_crt *crt, 
                       int depth, uint32_t *flags) {
    // Custom validation logic
    if (depth == 0) {  // Server certificate
        // Check subject CN
        if (strstr(crt->subject.val, "mqtt.company.com") == NULL) {
            *flags |= MBEDTLS_X509_BADCERT_CN_MISMATCH;
            return -1;
        }
    }
    
    // Additional security checks
    return check_certificate_security_policy(crt);
}
```

</div>

</div>

## Security Policies
- **Certificate expiration** monitoring
- **Weak cryptography** detection (RSA < 2048, etc.)
- **Subject Alternative Names** (SAN) validation
- **Key usage** verification (digital signature, key encipherment)
- **Extended Key Usage** validation (server/client authentication)