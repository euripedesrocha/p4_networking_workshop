---
# You can also start simply with 'default'
theme: default
# favicon, can be a local file path or URL
favicon: '/favicons/favicon-32x32.png'
# force color schema for the slides, can be 'auto', 'light', or 'dark'
colorSchema: light
# aspect ratio for the slides
aspectRatio: 16/9
# real width of the canvas, unit in px
canvasWidth: 980
# some information about your slides (markdown enabled)
title: ESP32-P4 Networking Workshop
info: |
  ## ESP32-P4 Networking Workshop
  3-Part Hands-On Workshop: Basic Networking to Secure MQTT
  
  Covers ESP-NETIF, Ethernet, WiFi Remote, Custom Firmware, and Secure MQTT
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# Config required for slidev-component-poll addon
pollSettings:
  anonymous: true
---

# ESP32-P4 Networking Workshop

<span style="font-size: 1.5rem;">Hands-On Workshop: Basic Networking to Secure MQTT</span>

<div style="position: absolute; bottom: 2rem; left: 0; width: 100%; text-align: center;">
  ESP32-P4 Function EV Board + ESP32-C6<br>
  <span style="font-size: 0.8rem; display: inline-block;">3-Part Workshop • Basic Networking • Custom Firmware • Secure MQTT</span>
</div>

---
src: ./slides/00-introduction/02-new-agenda.md
---

---
src: ./slides/00-introduction/03-esp32-p4-overview.md
---

# Part 1: Basic Networking Fundamentals

---
src: ./slides/01-part1-basic-networking/01-part1-intro.md
---

---
src: ./slides/01-part1-basic-networking/02-quick-start-hands-on.md
---

---
src: ./slides/01-part1-basic-networking/03-minimal-working-code.md
---

---
src: ./slides/01-part1-basic-networking/04-menuconfig-wifi-setup.md
---

---
src: ./slides/01-part1-basic-networking/05-esp-netif-architecture.md
---

---
src: ./slides/01-part1-basic-networking/06-esp-netif-operations.md
---

---
src: ./slides/01-part1-basic-networking/07-esp-netif-configuration.md
---

---
src: ./slides/01-part1-basic-networking/08-wifi-remote-basics.md
---

---
src: ./slides/01-part1-basic-networking/09-wifi-configuration.md
---

<!-- --- -->
<!-- src: ./slides/01-part1-basic-networking/06-network-events.md -->
<!-- --- -->

---
src: ./slides/01-part1-basic-networking/10-custom-wifi-manager-intro.md
---

---
src: ./slides/01-part1-basic-networking/11a-wifi-manager-concepts.md
---

---
src: ./slides/01-part1-basic-networking/11b-wifi-manager-interface.md
---

---
src: ./slides/01-part1-basic-networking/11c-wifi-event-concepts.md
---

---
src: ./slides/01-part1-basic-networking/11d-wifi-event-types.md
---

---
src: ./slides/01-part1-basic-networking/11e-wifi-event-implementation.md
---

---
src: ./slides/01-part1-basic-networking/11f-wifi-reason-codes.md
---

---
src: ./slides/01-part1-basic-networking/12a-network-layer-concepts.md
---

---
src: ./slides/01-part1-basic-networking/12b-network-layer-interface.md
---

---
src: ./slides/01-part1-basic-networking/12c-ip-event-concepts.md
---

---
src: ./slides/01-part1-basic-networking/12d-ip-event-handler.md
---

---
src: ./slides/01-part1-basic-networking/12e-network-status-api.md
---

---
src: ./slides/01-part1-basic-networking/13a-retry-patterns.md
---

---
src: ./slides/01-part1-basic-networking/13b-retry-strategies.md
---

---
src: ./slides/01-part1-basic-networking/13c-retry-logic.md
---

---
src: ./slides/01-part1-basic-networking/13d-retry-success-handling.md
---

---
src: ./slides/01-part1-basic-networking/13e-reason-codes-mapping.md
---

---
src: ./slides/01-part1-basic-networking/13f-reason-codes-categories.md
---

---
src: ./slides/01-part1-basic-networking/13g-event-registration.md
---

---
src: ./slides/01-part1-basic-networking/13h-event-cleanup.md
---

---
src: ./slides/01-part1-basic-networking/18a-integration-concepts.md
---

---
src: ./slides/01-part1-basic-networking/18b-initialization-sequence.md
---

<!-- --- -->
<!-- src: ./slides/01-part1-basic-networking/18c-monitoring-concepts.md -->
<!-- --- -->
<!---->
<!-- --- -->
<!-- src: ./slides/01-part1-basic-networking/18d-monitoring-implementation.md -->
<!-- --- -->
<!---->
<!-- --- -->
<!-- src: ./slides/01-part1-basic-networking/18e-resource-management.md -->
<!-- --- -->
<!---->
<!-- --- -->
<!-- src: ./slides/01-part1-basic-networking/19a-part1-hands-on.md -->
<!-- --- -->

# Part 2: ESP32-C6 Custom Firmware

---
src: ./slides/02-part2-esp32c6-firmware/01-part2-intro.md
---

---
src: ./slides/02-part2-esp32c6-firmware/02-esp-hosted-architecture.md
---

---
src: ./slides/02-part2-esp32c6-firmware/03-custom-firmware-benefits.md
---

---
src: ./slides/02-part2-esp32c6-firmware/04-firmware-requirements.md
---

---
src: ./slides/02-part2-esp32c6-firmware/05-development-environment.md
---

---
src: ./slides/02-part2-esp32c6-firmware/06-building-firmware.md
---

---
src: ./slides/02-part2-esp32c6-firmware/07-flashing-process.md
---

---
src: ./slides/02-part2-esp32c6-firmware/08-uart-jtag-programming.md
---

---
src: ./slides/02-part2-esp32c6-firmware/09-sdio-verification.md
---

---
src: ./slides/02-part2-esp32c6-firmware/10-advanced-features.md
---

---
src: ./slides/02-part2-esp32c6-firmware/11-part2-hands-on.md
---

# Part 3: Secured MQTT with Mutual Authentication

---
src: ./slides/03-part3-secure-mqtt/01-part3-intro.md
---

---
src: ./slides/03-part3-secure-mqtt/02-mqtt-fundamentals.md
---

---
src: ./slides/03-part3-secure-mqtt/03-security-concepts.md
---

---
src: ./slides/03-part3-secure-mqtt/04-tls-overview.md
---

---
src: ./slides/03-part3-secure-mqtt/05-certificate-management.md
---

---
src: ./slides/03-part3-secure-mqtt/06-mutual-authentication.md
---

---
src: ./slides/03-part3-secure-mqtt/07-secure-configuration.md
---

---
src: ./slides/03-part3-secure-mqtt/08-certificate-validation.md
---

---
src: ./slides/03-part3-secure-mqtt/09-secure-storage.md
---

---
src: ./slides/03-part3-secure-mqtt/10-implementation.md
---

---
src: ./slides/03-part3-secure-mqtt/11-part3-hands-on.md
---

# Conclusion

---
src: ./slides/04-conclusion/01-workshop-summary.md
---

---
src: ./slides/04-conclusion/02-next-steps.md
---

---
src: ./slides/04-conclusion/03-questions-discussion.md
---
