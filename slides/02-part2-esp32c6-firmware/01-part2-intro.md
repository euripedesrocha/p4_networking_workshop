# Part 2: Wireless Connectivity for ESP32-P4

Espressif provides four main solutions for adding Wi-Fi and Bluetooth:

- **ESP-AT**: Simple, AT command-based interface for basic connectivity. Easy to use, but limited in performance and flexibility.
- **ESP-Extconn**: Integrates external wireless connectivity using familiar ESP-IDF APIs. Flexible, but requires more development effort. low SoC supported
- **Wi-Fi Remote over ESP-Hosted**: Provides a standard network interface to the host. Supports advanced features, higher performance, and is open-source for customization.
- **Wi-Fi Remote over EPPP**: General-purpose PPP connectivity for WiFi gateway applications. Uses standard PPP protocol with support for multiple transports and logical channels. 
