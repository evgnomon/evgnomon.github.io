---
title: "Debian 13 (trixie) on the Samsung Galaxy Book6 Pro 16"
date: 2026-09-23
draft: false
description: "Get Debian trixie working on the Galaxy Book6 Pro 16 with trixie-backports."
tags: ["debian", "trixie", "linux", "samsung", "galaxy-book", "panther-lake", "laptop"]
categories: ["Linux"]
ShowToc: true
---

Trixie ships kernel 6.12. The Book6 Pro (Panther Lake, Arc B390 / Xe3) needs kernel 6.18+, Mesa 25.3+ and current firmware. All of it comes from `trixie-backports`.

<!--more-->

## Before installing

1. Update the BIOS from Windows. Samsung ships firmware only through Windows Update.
2. Have wired network ready (USB-C Ethernet or phone USB tethering). Wi-Fi will not work in the installer.

## 1. Install trixie

Install from the standard netinst or DVD image. Keep `non-free-firmware` enabled. The desktop will run on software rendering until step 4.

## 2. Enable backports

Create `/etc/apt/sources.list.d/backports.sources`:

```text
Types: deb
URIs: http://deb.debian.org/debian
Suites: trixie-backports
Components: main contrib non-free non-free-firmware
Signed-By: /usr/share/keyrings/debian-archive-keyring.gpg
```

```bash
sudo apt update
```

## 3. Kernel and firmware

```bash
sudo apt install -t trixie-backports \
    linux-image-amd64 \
    firmware-linux-nonfree \
    firmware-intel-graphics \
    firmware-iwlwifi \
    firmware-sof-signed
```

Check the kernel version is 6.18 or newer before rebooting:

```bash
apt policy linux-image-amd64
```

Reboot, then verify:

```bash
uname -r
lspci -k | grep -A3 -E "VGA|Display"   # Kernel driver in use: xe
```

Secure Boot keeps working; backports kernels are signed.

## 4. Mesa

```bash
sudo apt install -t trixie-backports \
    mesa-vulkan-drivers libgl1-mesa-dri libegl-mesa0 \
    libglx-mesa0 libgbm1 mesa-va-drivers
sudo apt install mesa-utils vulkan-tools
```

Verify:

```bash
vulkaninfo --summary | grep -E "deviceName|driverName"
```

`llvmpipe` means you are still on software rendering. Check `apt policy mesa-vulkan-drivers`; if backports is below 25.3, wait for the update or move to Debian testing (forky).

## 5. Samsung platform driver

Included in the backports kernel (`samsung-galaxybook`, 6.15+).

```bash
lsmod | grep samsung_galaxybook
cat /sys/firmware/acpi/platform_profile_choices
ls /sys/class/power_supply/        # battery name, e.g. BAT1
```

Other firmware options are under `/sys/class/firmware-attributes/samsung-galaxybook/attributes/`.

## 6. Swap Alt and Super

The Fn key cannot be remapped. Swap Alt and Super so Alt sits next to Fn.

Do it in udev hwdb, not in xkb. GNOME on Wayland applies `altwin:swap_alt_win` to every keyboard, so external keyboards and docks get swapped too. A hwdb remap changes scancodes for the built-in keyboard only.

Create `/etc/udev/hwdb.d/61-keyboard-builtin-altwin.hwdb`:

```text
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnSamsung:pnGalaxyBook6Pro-PAMB:*
 KEYBOARD_KEY_38=leftmeta
 KEYBOARD_KEY_db=leftalt
```

- `atkbd` matches only the internal i8042 keyboard, and only on this Samsung model.
- `0x38` is Left Alt, which now sends Super.
- `0xdb` is Left Super (`e0 5b`), which now sends Alt.
- Right Alt is unchanged.

Apply it without a reboot:

```bash
sudo systemd-hwdb update
sudo udevadm trigger --subsystem-match=input --action=change
```

On another laptop, take the vendor and product from `/sys/class/dmi/id/sys_vendor` and `/sys/class/dmi/id/product_name`, remove the spaces, and put them in the `svn` and `pn` fields. If the keys do not swap, check the scancodes with `sudo evtest` or `sudo showkey -s`.

**Fn + F12** toggles Fn Lock. It resets on reboot.

## 7. Check the rest

| Part | Check |
|---|---|
| Audio | Works. |
| Wi-Fi 7 | Works. |
| Suspend | Run several suspend/resume cycles on battery and on charger. |
| Touchpad | Pointing works; haptic click feedback is uneven. |
| Fingerprint | Not supported by libfprint. Use a password. |
