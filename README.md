# HP EliteBook 830 G6 – OpenCore EFI for macOS

This repository contains a working OpenCore EFI configuration for installing macOS on the **HP EliteBook 830 G6**. It is tailored for simplicity, stability, and a high success rate — even if it means sacrificing some GPU functionality for now.

---

## ✅ Supported macOS Versions

- macOS Catalina (10.15)
- macOS Big Sur (11)
- macOS Monterey (12)
- macOS Ventura (13)
- macOS Sonoma (14)

> **Note:** Ensure you use the right OpenCore version for your target macOS version.

---

## 💻 Hardware Specifications

| Component        | Details                                |
|------------------|----------------------------------------|
| Model            | HP EliteBook 830 G6                    |
| CPU              | Intel Core i5-8265U / i7-8565U (Whiskey Lake) |
| GPU              | Intel UHD Graphics 620 *(see note below)* |
| RAM              | 8GB / 16GB DDR4                        |
| Storage          | NVMe SSD (e.g., WD SN730)              |
| Wi-Fi/Bluetooth  | Intel Wireless-AC 9560 (using AirportItlwm.kext) |
| Audio            | Realtek ALC236 (via AppleALC.kext)     |

---

## 🔧 What's Working

- macOS boots and runs stably
- Internal keyboard and trackpad (with multi-touch gestures)
- Audio (speakers, mic, headphone jack)
- Wi-Fi & Bluetooth (with `AirportItlwm.kext`)
- All USB ports (USBToolBox + UTBMap)
- Ethernet (IntelMausi)
- Battery status monitoring
- Sleep & Wake
- Webcam
- Function keys (volume, brightness, etc.)

> ❗ **No graphics acceleration**: iGPU acceleration is disabled by default for maximum EFI compatibility (see below).

---

## ⚠️ iGPU Note – Why Hardware Acceleration is Disabled

During testing, setting a **device-id** for the Intel UHD 620 broke every EFI I tried. Removing it allowed macOS to boot successfully, but **at the cost of hardware acceleration** (you’ll notice animations may be slower, and some apps may lag).

This setup **prioritizes compatibility** — it works across multiple macOS versions. Advanced users can attempt to restore full iGPU acceleration by configuring the device properties correctly and are encouraged to contribute fixes or patches back to this repo to help others.

---

## 🚫 Known Issues

- ❌ No hardware acceleration (UHD 620 disabled)
- ❌ Fingerprint sensor (unsupported)
- ⚠️ Thunderbolt 3 (untested)
- ⚠️ SD card reader (may need extra config)

---

## 📁 EFI Folder Structure

```text
EFI/
├── BOOT/
│   └── BOOTx64.efi
└── OC/
    ├── ACPI/
    │   ├── SSDT-AWAC.aml
    │   ├── SSDT-EC-USBX-LAPTOP.aml
    │   ├── SSDT-PLUG-DRTNIA.aml
    │   └── SSDT-PNLF.aml
    ├── Drivers/
    ├── Kexts/
    │   ├── AirportItlwm.kext
    │   ├── AppleALC.kext
    │   ├── IntelMausi.kext
    │   ├── Lilu.kext
    │   ├── NVMeFix.kext
    │   ├── VirtualSMC.kext
    │   ├── VoodooI2C.kext
    │   ├── VoodooI2CHID.kext
    │   ├── VoodooPS2Controller.kext
    │   └── WhateverGreen.kext
    ├── Tools/
    └── config.plist
```

---

## 🛠️ Installation Steps

1. **Create macOS Installer:**
   - On a Mac or Hackintosh, download macOS from the App Store.
   - Use `createinstallmedia` to make a bootable USB.

2. **Mount EFI Partition:**
   - Use `diskutil` or [MountEFI](https://github.com/corpnewt/MountEFI).

3. **Copy EFI Folder:**
   - Replace the USB’s EFI with the one from this repository.

4. **BIOS Settings (Important):**
   - Disable **Secure Boot**
   - Enable **UEFI Boot**
   - Disable **Fast Boot**
   - Set **SATA Mode** to **AHCI**
   - (Optional) Enable **VT-d** if `DisableIoMapper` is active

5. **Install macOS:**
   - Boot from the USB, follow macOS installer steps.
   - After install, copy EFI from USB to internal drive using MountEFI.

---

## 🧰 Tools & Resources

- 📖 [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- 🛠️ [ProperTree](https://github.com/corpnewt/ProperTree) – for editing `config.plist`
- 🔐 [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) – generate valid serials
- 🧪 [Hackintool](https://github.com/headkaze/Hackintool) – diagnostics & USB mapping

---

## 🙏 Credits

- [Acidanthera](https://github.com/acidanthera) – OpenCore, Lilu, WhateverGreen, AppleALC, etc.
- [Dortania](https://dortania.github.io) – Comprehensive documentation
- [OpenIntelWireless](https://github.com/OpenIntelWireless) – Intel Wi-Fi kexts
- [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) – Trackpad and I2C support

---

## 🤝 Contribute

This repo works well out of the box, but there’s room for improvement — especially enabling proper graphics acceleration.

If you improve compatibility, enable UHD 620 acceleration, or fix other issues, please submit a pull request so others benefit too!

---

## 📄 License

MIT License – see the [LICENSE](LICENSE) file.
