# X.509 Certificate Management

## Certificate Components

<div class="grid grid-cols-2 gap-8">

<div>

### Certificate Authority (CA)
- **Root CA** - Trust anchor
- **Intermediate CA** - Signing authority
- **Certificate chain** validation
- **CRL/OCSP** revocation checking

### Certificate Types
- **Server certificate** - MQTT broker identity
- **Client certificate** - Device identity
- **CA certificate** - Trust verification

</div>

<div>

### Certificate Generation
```bash
# Generate CA private key
openssl genrsa -out ca.key 4096

# Create CA certificate  
openssl req -new -x509 -days 365 \
  -key ca.key -out ca.crt

# Generate client private key
openssl genrsa -out client.key 2048

# Create client certificate request
openssl req -new -key client.key \
  -out client.csr

# Sign client certificate
openssl x509 -req -days 365 \
  -in client.csr -CA ca.crt \
  -CAkey ca.key -out client.crt
```

</div>

</div>

## Certificate Storage in ESP32-P4
- **Embedded in firmware** - Compile-time inclusion
- **NVS encrypted storage** - Runtime secure storage
- **External secure element** - Hardware security module