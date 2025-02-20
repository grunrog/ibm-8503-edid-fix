# IBM 8503 EDID Fix
(TODO)
## Installation
1. Copy the EDID file to the `/lib/firmware` directory :
```
sudo cp ibm_8503_edid.bin /lib/firmware/ibm_8503_edid.bin
```
2. Open the GRUB configuration file in `/etc/default/grub` and add "`drm.edid_firmware=DP-2:ibm_8503_edid.bin`" to the `GRUB_CMDLINE_LINUX_DEFAULT` line.

Example :
```
...
GRUB_CMDLINE_LINUX_DEFAULT="... drm.edid_firmware=DP-2:ibm_8503_edid.bin"
...
```
3. Regenerate the GRUB configuration file :
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
4. Open the mkinitcpio configuration file in `/etc/mkinitcpio.conf` and add to the `FILES` section the path to the EDID (`/lib/firmware/ibm_8503_edid.bin`).

Example :
```
...
# FILES
# This setting is similar to BINARIES above, however, files are added
# as-is and are not parsed in any way.  This is useful for config files.
FILES=(/lib/firmware/ibm_8503_edid.bin)
...
```
5. Regenerate the initramfs image :
```
sudo mkinitcpio -P
```
6. Reboot the system.
