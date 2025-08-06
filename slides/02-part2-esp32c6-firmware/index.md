---
title: "Expanding ESP32-P4 Connectivity: Methods and Workshop"
date: "2025-07-16"
tags: ["Workshop", "ESP32-P4", "Connectivity", "ESP32-C6-MINI-1"]
showTableOfContents: true
---

Welcome to the ESP32-P4 connectivity workshop! In this session, you will learn how to expand the connectivity options of the ESP32-P4, a high-performance SoC without built-in wireless, by leveraging different connection modes and the ESP32-P4 Function_EV_Board. This board integrates an ESP32-C6-MINI-1 module, which will be used as a Wi-Fi host.

{{< gallery >}}
 <img src="assets/featured.webp" />
{{< /gallery >}}

## About this Workshop

The ESP32-P4 is a high-performance SoC without built-in wireless connectivity. This workshop focuses on expanding its capabilities using the `esp_wifi_remote` component, which enables Wi-Fi networking by bridging the ESP32-P4 to a wireless co-processor (such as ESP32-C6) over a high-speed interface. We will also explore the theoretical underpinnings of this approach, comparing it to other lower-layer solutions like `eppp_link` and `esp_hosted`, to help you understand the trade-offs and architecture choices for robust wireless integration.

## Prerequisites

### Hardware
- Computer (Windows, Linux, or macOS)
- ESP32-P4 Function_EV_Board (with ESP32-C6-MINI-1 onboard)
- ESP-Prog Board
- USB-C Cable
- Micro USB Cable

### Software
- [ESP-IDF v5.5.0 or later](https://github.com/espressif/esp-idf/releases)
- [`esp_wifi_remote` component](https://components.espressif.com/components/espressif/esp_wifi_remote/versions/0.14.4?language=en) (for Wi-Fi remote bridging)
- [`eppp_link`](https://components.espressif.com/components/espressif/eppp_link) (for understanding the PPP-based transport layer)
- [`esp_hosted`](https://components.espressif.com/components/espressif/esp_hosted) (for reference and comparison)

## Board Overview
The [ESP32-P4](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32p4/esp32-p4-function-ev-board/index.html) Function_EV_Board is a versatile development platform featuring:
- ESP32-P4 SoC (main application processor)
- ESP32-C6-MINI-1 module (provides Wi-Fi 6 and Bluetooth 5)
- Rich I/O and expansion options


{{< gallery >}}
  <!-- Placeholder: Board block diagram or photo -->
{{< /gallery >}}

## Hands-on: Create a new project

To create the project from the command line interface (CLI), you can use the following command. Make sure you have your ESP-IDF installed.
  
**Create a new project from example**

  ```bash
  idf.py create-project-from-example "espressif/esp_mqtt_cxx:tcp
  cd tcp/
  ```
> **TODO:** Review the broker issue, and P4 workaround

**Configure the project:**
   ```bash
   idf.py set-target esp32c6
   idf.py menuconfig
   ```

   In menuconfig -> Example Configuration, change the Broker to:
   ```bash
    mqtt://test.mosquitto.org
   ```

**Add support to P4**

  Currently the esp-idf-cxx GPIO does not support P4. Open: 
  ```bash
  managed_components/espressif__esp-idf-cxx/gpio_cxx.gpp
  ```

  At line 34 add the following code:

  ```c
    #elif CONFIG_IDF_TARGET_ESP32P4
    constexpr std::array<uint32_t, 0> INVALID_GPIOS = {};
  ```
**Build the firmware:**
  
  ```bash
    idf.py build
  ```

## Hands-on: Setup Netif and Wi-Fi

{{< alert icon="circle-info">}}
For this section, we will set up the station mode Wi-Fi driver and connect to a Wi-Fi 4 / Wi-Fi 6 network.
{{< /alert >}}

To get started with Wi-Fi, we need to set up the Wi-Fi driver in order to connect to a Wi-Fi network, using the access credentials (SSID and password).

**Open main/mqtt_tcp_example.cpp**

**Remove example_connect()**

**Add all the necessary includes.**
  ```c
  TODO
  ```

**Initialize Wi-Fi**

To initialize the Wi-Fi driver, perform the following steps:

- Initialize the TCP/IP stack:
  ```c
  esp_netif_init();
  esp_event_loop_create_default();
  esp_netif_create_default_wifi_sta();
  ```

- Initialize and allocate the resources for the Wi-Fi driver:
  ```c
  wifi_init_config_t cfg = WIFI_INIT_CONFIG_DEFAULT();
  esp_wifi_init(&cfg);
  ```

- Register the event handler for `WIFI_EVENT` and `IP_EVENT`:
  ```c
  esp_event_handler_instance_t instance_any_id;
  esp_event_handler_instance_t instance_got_ip;
  esp_event_handler_instance_register(WIFI_EVENT,
          ESP_EVENT_ANY_ID,
          &event_handler,
          NULL,
          &instance_any_id);
  esp_event_handler_instance_register(IP_EVENT,
          IP_EVENT_STA_GOT_IP,
          &event_handler,
          NULL,
          &instance_got_ip);
  ```

- Set the Wi-Fi mode as Station using `WIFI_MODE_STA`:
  ```c
  esp_wifi_set_mode(WIFI_MODE_STA);
  ```

- Set the Wi-Fi configuration:
  Using the struct `wifi_config_t`, set up Wi-Fi as `sta`:
  ```c
  wifi_config_t wifi_config = {
      .sta = {
          // Set the network name
          .ssid = WIFI_SSID,
          // Set the network pass key
          .password = WIFI_PASS,
          // Set WPA as the authentication mode
          .threshold.authmode = WIFI_AUTH_WPA_PSK,
          // Set Simultaneous Authentication (SAE) and Password Element (PWE) derivation method
          .sae_pwe_h2e = WPA3_SAE_PWE_BOTH,
          // Set the password identifier for H2E (Hash-to-Element)
          .sae_h2e_identifier = "",
      },
  };
  ```

  Then, set up the network **ssid** and **password** as:
  ```c
  #define WIFI_SSID "network-ssid"
  #define WIFI_PASS "network-pass"
  ```

- Now you can call the `esp_wifi_set_config` function.
  ```c
  esp_wifi_set_config(WIFI_IF_STA, &wifi_config);
  ```

- Start Wi-Fi on selected mode with the configuration defined:
  ```c
  esp_wifi_start();
  ```
---

#### Secure your Network

> **TODO:** Add Security steps

---

## Connectivity Methods with Wi-Fi Remote

The `esp_wifi_remote` component is the baseline for enabling Wi-Fi connectivity on the ESP32-P4. It allows the P4 to use Wi-Fi as if it were native, by offloading all Wi-Fi operations to a co-processor (such as ESP32-C6) over a high-speed interface. The main benefits are:
- Seamless integration with ESP-IDF networking APIs
- High throughput and low latency
- Minimal changes to application code
- Flexibility to choose the underlying transport layer

Wi-Fi Remote can use different lower-layer transport mechanisms to communicate with the co-processor. The two main options are:

### EPPP Link
The `eppp_link` component provides a general-purpose PPP (Point-to-Point Protocol) link between two microcontrollers, typically over UART, SPI, SDIO, or Ethernet. It negotiates IP addresses and networking using standard PPP, and can be used for tunneling IP traffic or custom data streams between the host (e.g., ESP32-P4) and the co-processor (e.g., ESP32-C6).

**Pros:**
- Flexible transport options (UART, SPI, SDIO, Ethernet) for the host-to-co-processor link
- Standard PPP protocol for IP networking between devices
- Supports logical channels for multiplexing multiple data streams over the same link
- Optional PPP authentication (PAP/CHAP) for securing the link

**Cons:**
- PPP adds protocol overhead to the host-to-co-processor link
- Security is limited to PPP authentication; no built-in encryption for the link
- May require more configuration for optimal performance
- Not as tightly integrated with standard network interfaces as esp_hosted

### ESP-Hosted
The `esp_hosted` solution turns the ESP32 (or similar) into a network co-processor, exposing either an Ethernet-like (802.3) or Wi-Fi-like (802.11) interface to the host. The host (e.g., ESP32-P4) communicates with the co-processor (e.g., ESP32-C6) over SPI, SDIO, or UART, and sees a standard network interface.

**Pros:**
- Presents a standard network interface (Ethernet/Wi-Fi) to the host for the host-to-co-processor link
- Supports advanced networking features (VLAN, multiple interfaces) over the link
- Can use SPI, SDIO, or UART for the physical connection
- Open source and customizable

**Cons:**
- More complex integration than simple PPP
- Security of the link depends on the transport and driver; typically no built-in encryption or authentication for the host-to-co-processor link
- May require driver support and more resources on both host and co-processor

### Comparison Table: EPPP Link vs ESP-Hosted (Host-to-Co-Processor Link)

| Feature/Aspect      | EPPP Link (Host-Co-Processor)     | ESP-Hosted (Host-Co-Processor)  |
|--------------------|-----------------------------------|---------------------------------|
| Interface Options  | UART, SPI, SDIO, Ethernet         | SPI, SDIO, UART                 |
| Protocol/Stack     | PPP (Point-to-Point Protocol)     | 802.3 (Ethernet), 802.11 (Wi-Fi)|
| Security           | PPP authentication (PAP/CHAP); no built-in encryption | Typically none; relies on physical security or custom driver extensions |
| Multiplexing       | Logical channels (configurable)   | Multiple interfaces, VLAN       |
| Host Integration   | PPP interface, custom netif       | Standard netif (Ethernet/Wi-Fi) |
| Use Cases          | General IP tunneling, custom RPC  | Standard networking, advanced   |
| Performance        | Depends on transport, protocol    | Typically higher, optimized     |
| Customization      | High (protocol-level)             | High (network stack, features)  |


---

## Hands-on: Integrating Wi-Fi Remote into the Application

In this hands-on, you will learn how to integrate ESP-Hosted firmware for the ESP32-C6 co-processor, and connect it to your ESP32-P4 application.


### 1. Preparing ESP-Hosted Firmware to ESP32-C6
TODO: Update launchpad page
> **Note:** If you prefer a quick method using pre-built binary and the ESP Launchpad web tool, see [Flashing ESP-Hosted with Launchpad](launchpad).

The board connection for this workshop is **SDIO** (which is the default value in the configuration).

Follow these steps to build and flash ESP-Hosted firmware to your ESP32-C6 using ESP-Prog:

**Create the ESP-Hosted project from the example:**
   ```bash
   idf.py create-project-from-example "espressif/esp_hosted:slave"
   cd esp_hosted_slave
   ```
**Configure the project:**
   ```bash
   idf.py set-target esp32c6
   idf.py menuconfig
   ```
   - In menuconfig, confirm that the connection type is set to SDIO (default for this workshop).
**Build the firmware:**
   ```bash
   idf.py build
   ```
**Connect the ESP32-C6 to your computer using ESP-Prog.**
   - Connect the ESP-Prog to the ESP32-C6 UART and headers as shown below:
   ![Connect the cables](/assets/esp32-p4-function-ev-board-esp-prog.jpg)
   - Set the ESP32-C6 into download mode (hold Boot, press Reset, release Boot).
**Flash the firmware:**
   ```bash
   idf.py -p <ESP32-C6 serial port> flash
   ```
   - Replace `<ESP32-C6 serial port>` with the correct port (e.g., `/dev/ttyUSB0` or `COMx`).
**Reset the ESP32-C6 and verify the firmware is running.**

> For more details and troubleshooting, see the [official ESP32-P4 Function EV Board guide](https://github.com/espressif/esp-hosted-mcu/blob/main/docs/esp32_p4_function_ev_board.md#52-using-esp-prog).

---

### 2. Setting Up Wi-Fi Remote to the Application

Now it's time to connect the ESP32-P4 to a Wi-Fi network using Wi-Fi Remote. The ESP32-P4, together with the ESP32-C6 as a co-processor, will connect to your Wi-Fi network and enable advanced connectivity features.

**Add Wi-Fi Remote Required Components**

  Add dependencies for Wi-Fi remote and hosted support:
  ```bash
    idf.py add-dependency "espressif/esp_wifi_remote"
    idf.py add-dependency "espressif/esp_hosted"
  ```
  > **Note:** If adding these components to a different program, be sure to remove incompatible components (e.g. esp-extconn)

**Build and Flash**
  - Build the project:
    ```bash
      idf.py build
    ```
  - Flash and monitor:
    ```bash
    idf.py -p <host serial port> flash monitor
    ```
  - Replace `<host serial port>` with the correct port (e.g., `/dev/ttyUSB0` or `COMx`).

---

You have now set up ESP-Hosted on your WebSocket client application for the ESP32-P4, including Wi-Fi initialization. With the firmware built and flashed, your device is ready to leverage advanced wireless connectivity provided by the ESP32-C6.

> **Tip:** After flashing, check the serial monitor for successful Wi-Fi connection and network interface initialization.  

## References
- [`esp_wifi_remote` component documentation](https://components.espressif.com/components/espressif/esp_wifi_remote/versions/0.14.4?language=en)
- [`eppp_link` component documentation](https://components.espressif.com/components/espressif/eppp_link)
- [`esp_hosted` component documentation](https://components.espressif.com/components/espressif/esp_hosted)
- [Wireless Connectivity Solutions for ESP32-P4](https://developer.espressif.com/blog/wireless-connectivity-solutions-for-esp32-p4/)
---
