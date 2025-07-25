# Kuiper Build

## Get Image

### Github Actions Builds

<https://github.com/analogdevicesinc/adi-kuiper-gen/actions>

### Build Locally

<https://github.com/analogdevicesinc/adi-kuiper-gen>

## Write SD Card

1. **Insert your SD card** into your computer.

2. **Identify the device name** of your SD card:

   ```bash
   sudo fdisk -l
   ```

   Look for a device like `/dev/sdX` or `/dev/mmcblkX` (where X is a letter or number) that matches your SD card's size.

3. **Unmount any auto-mounted partitions**:

   ```bash
   sudo umount /dev/sdX*
   ```

   Replace `/dev/sdX` with your actual device path.

4. **Write the image to the SD card**:

   ```bash
   sudo dd if=image_YYYY-MM-DD-ADI-Kuiper-Linux-[arch].img of=/dev/sdX bs=4M status=progress conv=fsync
   ```

   Replace `/dev/sdX` with your actual device path, and update the image filename accordingly.

5. **Ensure all data is written**:

   ```bash
   sudo sync
   ```

6. **Eject the SD card**:

   ```bash
   sudo eject /dev/sdX
   ```

## Prepare Boot Files

### RPi 5

```bash
sudo tar -xf rpi_modules.tar.gz -C /media/$USER/rootfs/lib/modules
sudo cp Image /media/$USER/BOOT/kernel_2712.img
sudo cp *.dtb /media/$USER/BOOT
sudo cp overlays/*.dtb* /media/$USER/BOOT/overlays
```
