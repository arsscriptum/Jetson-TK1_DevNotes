## Updating system using internet

Requirement:
- Host PC with Linux
- Internet
- USB cable

This is included in Jetson TK1 box.

Instruction:
- Install OS in Jetson TK1
- Install NVIDIA kernel and drivers
- Login to your Jetson TK1
- Execute following command in Jetson TK1

```
	sudo apt-add-repository universe
	#Keep Jetson specific driver files.
	sudo apt-mark hold xserver-xorg-core

	#Update system
	sudo apt-get update
	sudo apt-get upgrade
```

Check whether Jetson specific driver files are not over written


```
    sha1sum -c /etc/nv_tegra_release
```

### (Optional) Install "The Grinch" Custom Kernel by Santyago
If you want to use the Grinch kernel, use this script.
(His kernel supports more devices than nvidia kernel)


### Tips:

If you will use the shell command-line a lot.
```
    sudo apt-get install bash-completion command-not-found
```
You can update Ubuntu with following command next time.
```
		sudo apt-get update
		sudo apt-get upgrade
```
These command don't update drivers for Jetson TK1.
New drivers for Jetson TK1 will be released here.

