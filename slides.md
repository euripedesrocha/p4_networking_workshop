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

# Introduction

---
src: ./slides/00-introduction/01-title.md
---

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
src: ./slides/01-part1-basic-networking/02-esp-netif-architecture.md
---

---
src: ./slides/01-part1-basic-networking/03-esp-netif-operations.md
---

---
src: ./slides/01-part1-basic-networking/04-ethernet-advantages.md
---

---
src: ./slides/01-part1-basic-networking/05-ethernet-setup.md
---

---
src: ./slides/01-part1-basic-networking/06-ethernet-configuration.md
---

---
src: ./slides/01-part1-basic-networking/07-wifi-remote-basics.md
---

---
src: ./slides/01-part1-basic-networking/08-wifi-configuration.md
---

---
src: ./slides/01-part1-basic-networking/09-network-events.md
---

---
src: ./slides/01-part1-basic-networking/10-part1-hands-on.md
---

# Part 2: ESP32-C6 Custom Firmware

---
src: ./slides/02-part2-esp32c6-firmware/01-part2-intro.md
---

---
src: ./slides/02-part2-esp32c6-firmware/02-connectivity-comparison.md
---

---
src: ./slides/02-part2-esp32c6-firmware/05-esp-hosted-tasks.md
---

---
src: ./slides/02-part2-esp32c6-firmware/06-development-environment.md
---

---
src: ./slides/02-part2-esp32c6-firmware/07-esp-prog-connection.md
---

---
src: ./slides/02-part2-esp32c6-firmware/08-flash-process.md
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