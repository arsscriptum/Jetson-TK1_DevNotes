# Jetson TK1 Development Notes

[Starting](http://demotomohiro.github.io/hardware/jetson_tk1/index.html#preparing)


## Official Support Site 

[This is the official Wiki for embedded Tegra & the Jetson TK1 board](https://elinux.org/Jetson_TK1)

[Official Devlopment Forums](https://forums.developer.nvidia.com/)


#### [How o access board](https://elinux.org/Jetson_TK1#Basic_setup_steps_to_access_the_board_and_access_internet)

## Using Jetson

[Using Jetson TK1 like PC](http://demotomohiro.github.io/hardware/jetson_tk1/setup/pc.html)

or

[Remote connection](http://demotomohiro.github.io/hardware/jetson_tk1/setup/remote.html) / [Remote connection without router](http://demotomohiro.github.io/hardware/jetson_tk1/setup/remote_wo_router.html)

or

[Serial console](http://demotomohiro.github.io/hardware/jetson_tk1/setup/serial.html)


## Boot Jetson TK1 in recovery mode

[Source](http://demotomohiro.github.io/hardware/jetson_tk1/setup/recovery_mode.html)

When you install OS or flash kernel or boot loader to Jetson TK1, it need to be connected to host PC and boot in recovery mode.
Unlike PC with x86 CPU, Jetson TK1 cannot do that by itself.

(2 Jetson TK1 might be able to update each other without PC?)

Requirement:
- Host PC with Linux
- USB cable
- This is included in Jetson TK1 box.

Instruction:
- Turn off Jetson TK1
- Connect the Micro-B plug on the USB cable(included in Jetson TK1 box) to the Recovery (USB Micro-B) Port on the Jetson TK1 and the other end to an available USB port on the host PC
- Power on Jetson in recovery mode
- Press "Force Recovery" Button, press "POWER" Button, release POWER Button and release Force Recovery button.

In recovery mode, you cannot login to Jetson TK1.
If Jetson TK1 in recovery Mode and it is connected to host PC, "lsusb" command lists it with ID 0955:7140 in host PC.

```
    $ lsusb
    Bus 002 Device 007: ID 0955:7140 NVidia Corp.
```


## Code Resources

[Jetson Hacks](https://github.com/jetsonhacks)



## Jetson TK1 Linux for Tegra (L4T) 21.1 – Enable USB 3.0

[Video](https://www.youtube.com/watch?v=P-nt3oLRLWU)
[Page](https://jetsonhacks.com/2014/11/08/jetson-tk1-linux-tegra-l4t-21-1-enable-usb-3-0/)

Linux for Tegra (LT4) uses UBoot as its bootloader, replacing fastboot. In order to enable the full size USB port as 3.0, you can change the boot configuration file on the Jetson.

The boot configuration file is located here:

/boot/extlinux/extlinux.conf

There are several example configuration files in that directory which define how to boot from different devices.

The switch to change is: usb_port_owner_info=2 #USB 3.0

There are two usb_port_owner_info=0 specifications in extlinux.conf, one is extra. Only the last assignment will be used. You may delete one of the specifications, as I've shown in the following example.

A new example config file with USB 3.0 enabled:

```
	TIMEOUT 30
	DEFAULT primary

	MENU TITLE Jetson-TK1 eMMC boot options

	LABEL primary
	MENU LABEL primary kernel
	LINUX /boot/zImage
	FDT /boot/tegra124-jetson_tk1-pm375-000-c00-00.dtb
	APPEND console=ttyS0,115200n8 console=tty1 no_console_suspend=1 lp0_vec=2064@0xf46ff000 video=tegrafb mem=1862M@2048M memtype=255 ddr_die=2048M@2048M section=256M pmuboard=0x0177:0x0000:0x02:0x43:0x00 vpr=151M@3945M tsec=32M@3913M otf_key=c75e5bb91eb3bd947560357b64422f85 usbcore.old_scheme_first=1 core_edp_mv=1150 core_edp_ma=4000 tegraid=40.1.1.0.0 debug_uartport=lsport,3 power_supply=Adapter audio_codec=rt5640 modem_id=0 android.kerneltype=normal fbcon=map:1 commchip_id=0 usb_port_owner_info=2 lane_owner_info=6 emc_max_dvfs=0 touch_id=0@0 tegra_fbmem=32899072@0xad012000 board_info=0x0177:0x0000:0x02:0x43:0x00 root=/dev/mmcblk0p1 rw rootwait tegraboot=sdmmc gpt
```


## Remote Access

https://elinux.org/Jetson/Remote_Access

## Accessing the device from your PC

First you should see if you can ping the device:
```
		ping tegra-ubuntu
```
Assuming this works, log into your device from your PC:
```
		ssh ubuntu@tegra-ubuntu
```
Or if you want to use graphical apps on the device display it on your PC using "X forwarding":
```
		ssh -X ubuntu@tegra-ubuntu nautilus
```
You should now have full remote access to the device. The only remaining feature to test is if the device has internet access. Note: By default the device won't have ICMP ping service enabled, so instead of using "ping www.google.com", you can test internet access by running this on the device:
```
		wget www.google.com
```
You can also get remote desktop access to your device such as by using a VNC or commercial SplashTop / TeamViewer solution, allowing you to run graphical apps easily without needing a HDMI monitor attached to your device. Beware though, that if you are trying to run graphical apps to their limits, some remote desktop solutions such as VNC are unlikely to give you the full performance or GPU acceleration.


## [Updating System](Updating.md)