# XPS 9560 macOS Sonoma 14.6.1 EFI (OpenCore 1.0.1)

This repository contains the EFI files for running macOS Sonoma 14.6.1 on the Dell XPS 9560 (i7-7700HQ / 4K UHD / GTX 1050 / Intel HD 630) using OpenCore 1.0.1.

## Specifications

- **Model:** Dell XPS 9560
- **CPU:** Intel Core i7-7700HQ
- **GPU:** Intel HD 630 & Nvidia GTX 1050 (disabled in macOS)
- **RAM:** 16GB DDR4
- **Storage:** NVMe SSD
- **Display:** 15.6" 4K UHD (3840x2160)
- **Audio:** Realtek ALC298
- **Wi-Fi:** Intel AX200 (with support using AirportItlwm)
- **Bootloader:** OpenCore 1.0.1
- **macOS Version:** Sonoma 14.6.1

## What's Working

- [x] Intel HD 630 Graphics (with hardware acceleration)
- [x] Audio (internal speakers, microphone, headphone jack)
- [x] Wi-Fi & Bluetooth (with Intel AX200 using AirportItlwm)
- [x] Keyboard & Trackpad (with gestures)
- [x] Battery Management
- [x] Sleep/Wake
- [x] USB Ports (including Type-C)
- [x] HDMI output
- [x] Brightness Control
- [x] Webcam

## Not Working / Issues

- [ ] Nvidia GTX 1050 (not supported in macOS)
- [ ] SD Card Reader (unsupported)
- [ ] Thunderbolt 3 hot-plug (works when connected at boot)
- [ ] Occasionally slow boot times (related to certain ACPI patches)
- [ ] AirDrop, Handoff, and Sidecar (Intel Wi-Fi lacks native macOS support for these features)

## BIOS Settings

To get the best compatibility, ensure your BIOS settings are configured as follows:

- **SATA Operation:** AHCI
- **Secure Boot:** Disabled
- **Enable Legacy Option ROMs:** Disabled
- **Boot Mode:** UEFI
- **Intel SpeedStep:** Enabled
- **VT-d:** Disabled
- **CFG Lock:** Disabled (if available)
- **Thunderbolt Boot Support:** Enabled

## Installation

1. **Prepare macOS USB Installer**: Create a macOS Sonoma 14.6.1 installer using [macOS Recovery](https://support.apple.com/en-us/HT201372) or from a working macOS environment.

2. **Copy EFI Folder**: After creating the USB installer, replace the EFI folder on the USB drive with the one from this repository.

3. **BIOS Setup**: Make sure your BIOS is configured as described in the "BIOS Settings" section.

4. **Install macOS**: Boot from the USB installer and follow the standard macOS installation steps.

5. **Post-Installation**:
    - Copy the EFI folder from the USB to your system's EFI partition after installing macOS.
    - Generate your own SMBIOS using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and replace the `SerialNumber`, `BoardSerialNumber`, and `SmUUID` in `config.plist`.

## Setting Up Intel AX200 Wi-Fi and Bluetooth

1. Download the latest release of [AirportItlwm](https://github.com/OpenIntelWireless/itlwm).
2. Add `AirportItlwm.kext` to your EFI's `OC/Kexts` folder and update your `config.plist` to include the kext.
3. The native macOS Wi-Fi menu will now work with your Intel AX200, no need for HeliPort.

## Known Issues & Troubleshooting

- **Slow Boot Times**: If you experience long boot times, try disabling `AppleCpuPmCfgLock` in `config.plist`.
- **Sleep/Wake Issues**: If the laptop doesn't wake from sleep properly, experiment with different `Darkwake` settings in `config.plist`.
- **Intel Wi-Fi Configuration**: For Intel AX200, follow the instructions from the [OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm) project to set up Wi-Fi and Bluetooth. Note that advanced features like AirDrop and Handoff are not supported.

## Credits

- [Acidanthera](https://github.com/acidanthera) for OpenCore and kexts
- [Dortania](https://dortania.github.io/) for their comprehensive guides
- [OpenIntelWireless](https://github.com/OpenIntelWireless) for Intel Wi-Fi and Bluetooth support
- [XPS 9560 Hackintosh Community](https://www.tonymacx86.com/) for testing and support
