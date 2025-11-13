# Devices

- `ls /dev` lists all devices. The first character represents the type of device:
  - b: block
  - c: character
  - s: socket
  - p: pipe

#### dd-command
The [dd](https://blog.kubesimplify.com/the-complete-guide-to-the-dd-command-in-linux) command can do a looooot of things, including copying files, wiping disks, creating backups. Here's a basic command to copy data from `/dev/zero` (an endless stream of zero bytes) to `new_file`:

```sh
$ dd if=/dev/zero of=new_file bs=1024 count=1
```

* **if=file** — Input file (defaults to standard input).
* **of=file** — Output file (defaults to standard output).
* **bs=size** — Block size for both reading and writing. You can use suffixes:

  * `b` = 512 bytes
  * `k` = 1024 bytes
    Example: `bs=1k` is the same as `bs=1024`.
* **ibs=size, obs=size** — Input and output block sizes when they differ. If they’re the same, just use `bs`.
* **count=num** — Number of blocks to copy. This prevents endless copying when the input is very large or infinite (like `/dev/zero`).
* **skip=num** — Skip the first *num* blocks of the input before copying.

### Device names
- Device names are kind of a hassle in linux. I think they get assigned device names based on the order in which they're encountered during boot, so there is no guarantee that `/dev/sda` and `/dev/sdb` are going to point to the same device.
- A solid way to get the device name is to query the `udev` daemon (`udevd`) using `udevadm`.
- If you dont have access to `udevadm` for some reason, you could try to find the device in `/sys`, check the logs using `journalctl -k` or `cat /proc/devices`. None of these are as easy as using `udev` of course.

### Device types
There are a lot of types, so I'll note down the most useful ones:
#### Hard disks: /dev/sd*
- The kernel makes separate files like `/dev/sda` and `/dev/sdb` based on the partitions.
- The sd stands for SCSI disk, and SCSI stands for Small Computer System Interface. This is an old hardware and protocol for communication between devices. SCSI hardware is not used anymore, but the protocol was pretty good that it stuck around. 
- USBs and SATA devices are represented using `sd`.
- To get a list of `sd` devices, use `lsscsi` command. Pretty sure it is supposed to mean: `ls scsi`

#### Non-Volatile Memory Devices: /dev/nvme*
- Is used to talk to some SSDs.

#### Device Mapper: /dev/dm-\*, /dev/mapper/*
LVM uses a device mapper to create block devices?

### Creating Device Files
```
mknod /dev/sda1 b 8 1
```
b - block device
8 and 1 are the major and minor numbers respectively.
The major number and minor number tell the kernel how to access the device. A common major number is assigned to all devices that are being controlled by the same device driver. The minor number helps to distinguish between the exact device type/controller using the same device driver.

Don't use `mknod` though, it's a lil unstable.

### udev
The `udev` daemon, i.e., `udevd` is responsible for sending notifications to the user space when a new device is detected. For example, plugging in a USB device.

[There's a lot more to understand about `udev` but the `Linux in a Nutshell` book pretty much told me to skip ahead until I'm more familiar with linux, so yep.]