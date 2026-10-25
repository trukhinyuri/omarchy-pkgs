# asus-proart-touchpad-haptics

Haptic click feedback for the ASUS ProArt P16 H7607BA (NVIDIA N1x) touchpad, a PixArt 093A:4F01 haptic pad on i2c-hid.

The pad reports clicks itself, but its HID descriptor has only a manual haptic trigger (output report 0x45) and no auto trigger, so neither its firmware nor the kernel's `hid-haptic` (which needs both) vibrates on a click. The daemon plays one waveform when a click goes down and one when it comes up, and sets the pad's overall strength (feature report 0x09) as the Windows touchpad slider does.

What it installs:

- `/usr/bin/asus-proart-touchpad-haptics`
- `/usr/lib/systemd/system/asus-proart-touchpad-haptics.service`
- `/usr/lib/udev/rules.d/70-asus-proart-touchpad-haptics.rules`, which starts the service when the pad's hidraw node appears
- `/etc/default/asus-proart-touchpad-haptics`, the settings

Usage:

```bash
sudo asus-proart-touchpad-haptics test          # play waveforms 3-7
sudoedit /etc/default/asus-proart-touchpad-haptics
sudo systemctl restart asus-proart-touchpad-haptics
```

Only the P16's 093A:4F01 is matched. The ProArt P14's 093A:4F02 may take the same reports; add it to the udev rule and `HID_GLOB` once that is checked on a P14.

The daemon is proart-haptic by Leon Marzoll from https://github.com/trukhinyuri/proart-p16-linux (GPL-2.0-only), used on a P16 under Ubuntu. This package starts it from udev instead of polling for the pad, and it exits when the pad stays away.
