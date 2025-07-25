# RPi 5 Desktop Not Working

## Issue Description

Kuiper arm64 written on SD card works fine on RPi4. On RPi5 the desktop doesn't work.

## Cause

Missing /dev/dri.

## Resources

<https://github.com/home-assistant/operating-system/issues/3321>

<https://forums.raspberrypi.com/viewtopic.php?t=358853>

<https://askubuntu.com/questions/1502950/raspi5-23-10-cannot-switch-to-lightdm-from-gdm3>

## Solution

Add /etc/X11/xorg.conf.d/99-vc4.conf with the following content:

```text
Section "OutputClass"
    Identifier "vc4"
    MatchDriver "vc4"
    Driver "modesetting"
    Option "PrimaryGPU" "true"
EndSection
```

Problem = since RPi5 has two GPUs, x11 doesn't choose correctly the one that should handle the display.

## Even Better Solution

On top of adding the conf file specified in the [section above](#solution):

In config.txt have dtoverlay=vc4-kms-v3d-pi5.

Here overlay_map.dtb is missing from overlays, so vc4-kms-v3d is not automatically mapped to vc4-kms-v3d-pi5.

## Ideal Solution

When copying the boot files in the SD card BOOT partition, make sure to also copy the files that have .dtb extension, not only .dtbo.

Easy fix: instead of copying *.dtbo, copy \*.dtb\*.

In config.txt have dtoverlay=vc4-kms-v3d, since now the mapping is done automatically.
