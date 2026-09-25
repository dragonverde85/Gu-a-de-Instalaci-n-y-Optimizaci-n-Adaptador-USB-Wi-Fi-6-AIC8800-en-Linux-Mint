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

Step 2: Download and Install the Driver

Clone the repository optimized for the AIC8800 chipset variant and run the installation script:
git clone [https://github.com/shenmintao/aic8800d80.git](https://github.com/shenmintao/aic8800d80.git)
cd aic8800d80
sudo ./install.sh

Note: The installation compiles the aic8800_fdrv module using DKMS. This ensures that the driver will be automatically recompiled if Linux Mint updates the kernel in the future.

Step 3: Reboot the System

Once compilation is complete, restart your system to register the changes:
sudo reboot

Optional Additional Steps (Troubleshooting & Stability)

These steps are recommended if the adapter disconnects during heavy file transfers or if Wi-Fi networks do not show up immediately upon startup.

Option A: Disable USB Power Saving (Prevents shutdowns under high load)

Linux Mint may suspend power to the USB port when detecting power consumption spikes or heavy traffic (e.g., during speed tests).

To permanently disable USB autosuspend:
echo "options usbcore autosuspend=-1" | sudo tee /etc/modprobe.d/disable-usb-autosuspend.conf

Option B: Manual Mode Switching (If the adapter gets stuck in Disk / CD-ROM mode)

If the system recognizes the adapter as a virtual drive (1111:1111) upon insertion and does not activate Wi-Fi, run these two commands to force mode switching:

sudo modprobe aic8800_fdrv
sudo usb_modeswitch -c /etc/usb_modeswitch.d/1111:1111

Option C: Thermal Considerations During Speed Tests

Ultra-compact USB adapters lack dedicated heat sinks. Running multiple consecutive speed tests pushes the integrated circuit to 100% continuous load, which may trigger thermal protection on the chip or USB port. For standard daily use (web browsing, downloading, streaming, or gaming), the adapter will maintain stable operation without overheating.
