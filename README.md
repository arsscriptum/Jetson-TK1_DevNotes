# Jetson TK1 Development Notes

[Starting](http://demotomohiro.github.io/hardware/jetson_tk1/index.html#preparing)


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