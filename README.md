# Linux Zen with WCN785x Support

This repository provides a patched version of the Arch Linux Zen kernel that fixes Bluetooth audio connection failures on systems with Qualcomm FastConnect 7800 Wi-Fi 7 cards (WCN785x chipset).

It is based on the official [Arch Linux Zen kernel](https://gitlab.archlinux.org/archlinux/packaging/packages/linux-zen) with the addition of [GreyXor's WCN785x patch](https://patchwork.kernel.org/project/bluetooth/patch/20241121180742.156230-1-greyxor@protonmail.com/), which adds support for the Qualcomm WCN785x Bluetooth chip.

The patch adds the USB ID `0489:e10a` to the Linux kernel's `btusb` driver, allowing proper recognition of Qualcomm FastConnect 7800 Bluetooth devices.

## Installation (Arch)

```bash
# Clone the repository
git clone https://github.com/thongtech/linux-zen-wcn785x.git
cd linux-zen-wcn785x

# Build and install the package
makepkg -si
```

The compilation process takes a while, depending on your hardware (approximately 20 minutes on my Ryzen AI 9 365 system).

This package will be installed as **`linux-zen-wcn785x`**, so it won't replace your current kernel. You can safely remove it later once the patch is merged upstream.

## Post-Installation

After installation, **you need to update your bootloader to include the new kernel**:

- **GRUB**: Follow the [Arch Wiki GRUB instructions](https://wiki.archlinux.org/title/GRUB#Generated_grub.cfg)
- **systemd-boot**: Follow the [Arch Wiki systemd-boot instructions](https://wiki.archlinux.org/title/Systemd-boot#Adding_loaders)
- **rEFInd**: Follow the [Arch Wiki rEFInd instructions](https://wiki.archlinux.org/title/REFInd#Configuration)

## Credits

- [GreyXor](https://patchwork.kernel.org/project/bluetooth/patch/20241121180742.156230-1-greyxor@protonmail.com/) for identifying the issue and creating the patch
- [Arch Linux Team](https://gitlab.archlinux.org/archlinux/packaging/packages/linux-zen) for the linux-zen package

This repository will be maintained until the patch is included in the upstream kernel.
