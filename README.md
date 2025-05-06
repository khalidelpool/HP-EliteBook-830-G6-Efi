# HP EliteBook 830 G6 – OpenCore EFI for macOS

This repository contains a working OpenCore EFI configuration for installing macOS on the **HP EliteBook 830 G6**. It is tailored for stability, compatibility, and ease of use.

---

## ✅ Supported macOS Versions

- macOS Catalina (10.15)
- macOS Big Sur (11)
- macOS Monterey (12)
- macOS Ventura (13)
- macOS Sonoma (14)

> **Note:** Make sure you’re using an OpenCore version compatible with the macOS version you intend to install.

---

## 💻 Hardware Specifications

| Component        | Details                                |
|------------------|----------------------------------------|
| Model            | HP EliteBook 830 G6                    |
| CPU              | Intel Core i5-8265U / i7-8565U (Whiskey Lake) |
| GPU              | Intel UHD Graphics 620                 |
| RAM              | 8GB / 16GB DDR4                        |
| Storage          | NVMe SSD (e.g., WD SN730)              |
| Wi-Fi/Bluetooth  | Intel Wireless-AC 9560 (using AirportItlwm.kext) |
| Audio            | Realtek ALC236 (via AppleALC.kext)     |

---

## 🔧 What's Working

- Intel UHD Graphics 620 (full acceleration)
- Audio (internal speakers, mic, headphone jack)
- Internal keyboard and trackpad (multi-touch gestures)
- Wi-Fi + Bluetooth (AirportItlwm)
- All USB ports (USBToolBox + UTBMap)
- Battery status monitoring
- Sleep & Wake
- Ethernet (IntelMausi)
- Webcam
- Function keys

---

## 🚫 Known Issues

- Fingerprint sensor (unsupported)
- Thunderbolt 3 (untested)
- SD card reader (may need extra config)

---

## 📁 EFI Folder Structure

EFI/
├── BOOT/
│ └── BOOTx64.efi
└── OC/
├── ACPI/
├── Drivers/
├── Kexts/
├── Tools/
└── config.plist

markdown
Copy
Edit

Main included SSDTs:
- `SSDT-AWAC.aml`
- `SSDT-EC-USBX-LAPTOP.aml`
- `SSDT-PLUG-DRTNIA.aml`
- `SSDT-PNLF.aml`

Main kexts:
- `AirportItlwm.kext`
- `AppleALC.kext`
- `IntelMausi.kext`
- `Lilu.kext`
- `NVMeFix.kext`
- `VirtualSMC.kext` (+ sensors)
- `VoodooI2C`, `VoodooI2CHID`, `VoodooPS2Controller.kext`
- `WhateverGreen.kext`

---

## 🛠️ Installation Steps

1. **Create macOS Installer:**
   - Use a Mac or Hackintosh to download macOS from the App Store.
   - Use `createinstallmedia` to make a bootable USB.

2. **Mount EFI Partition:**
   - Use `diskutil` or [MountEFI](https://github.com/corpnewt/MountEFI).

3. **Copy EFI Folder:**
   - Replace the USB EFI with the `EFI` folder from this repo.

4. **BIOS Settings:**
   - Disable **Secure Boot**
   - Enable **UEFI Boot**
   - Disable **Fast Boot**
   - Set **SATA mode** to **AHCI**
   - Enable **VT-d** *(optional, if using DisableIoMapper)*

5. **Install macOS:**
   - Boot from USB, install macOS.
   - After installation, copy the EFI to the internal drive.

---

## 🧰 Tools & Resources

- 📖 [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- 🛠️ [ProperTree](https://github.com/corpnewt/ProperTree) – for editing `config.plist`
- 🔐 [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) – generate SMBIOS serials
- 🧪 [Hackintool](https://github.com/headkaze/Hackintool) – kexts, patching, diagnostics

---

## 🙏 Credits

- [Acidanthera](https://github.com/acidanthera) – OpenCore, Lilu, WhateverGreen, etc.
- [Dortania](https://dortania.github.io) – Legendary documentation
- [OpenIntelWireless](https://github.com/OpenIntelWireless) – Intel Wi-Fi support
- [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) – Trackpad and I2C support

---

## 📬 Contribute

Found a bug? Improved something? Pull requests and issues are welcome!

---

## 📄 License

MIT License. See the [LICENSE](LICENSE) file.

---
