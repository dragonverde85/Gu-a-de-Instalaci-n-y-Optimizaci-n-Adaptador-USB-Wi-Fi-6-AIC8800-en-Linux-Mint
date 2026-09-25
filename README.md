# Installation and Optimization Guide: USB Wi-Fi 6 Adapter (AIC8800) on Linux Mint

## Device Information
- **Model:** USB Wi-Fi 6 AX900 Adapter (Wi-Fi + Bluetooth)
- **Manufacturer / Vendor:** Keroro Technology Ltd.
- **Internal Chipset:** AICSemi AIC8800
- **Disk-Mode ID:** `1111:1111` Pandora International Ltd. 88M80

---

## Step 1: Install System Dependencies
Open a terminal (`Ctrl` + `Alt` + `T`) with an active internet connection (via Ethernet cable or USB tethering from a smartphone) and install the required tools:

```bash
sudo apt update && sudo apt install -y build-essential dkms git linux-headers-$(uname -r) usb-modeswitch
