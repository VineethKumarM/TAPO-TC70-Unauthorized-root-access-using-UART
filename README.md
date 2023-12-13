# TAPO TC70 & C200 Unauthorized root access using UART.
### Product : TPLINK TAPO TC70 V3.0 , TAPO C200 V3.0 wifi cameras
### Firmware version: 1.3.4

## How to gain the root access
- Solder the UART pins on the camera circuit board to a *UART to USB* cable
- Find the usb port address using the `sudo dmesg` command
- Use the picocom command to start an interactive shell with access to bootlog
- Ex: `sudo picocom /dev/ttyUSBx -b 115200` , (x : {0,1,2..} check dmesg output to
find this)
- When the terminal is ready plugin the camera
- The camera boots twice on the second appearance of the ‘AutoBooting in 1 second’ type `slp` 
- This will grant access to the boot menu
- Change the boot configuration using(add/modify init=/bin/sh to the bootargs env
var): `setenv bootargs console=ttyS1,115200n8 mem=45M@0x0 rmem=19M@0x2d00000
root=/dev/mtdblock6 rootfstype=squashfs spdev=/dev/mtdblock7 noinitrd init=/bin/sh`
- Now reboot using boot command. 
- The camera boots directly to the /bin/sh shell giving root access
- Now you can access the complete file system of the camera and can also dump it using a sd card
