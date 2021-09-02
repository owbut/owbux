# Installation

Before we get started with the installation make sure you have a live CD/USB of a random Linux distribution. Make sure you have an fstab file ready and the disk should be mounted on /mnt. All disks should be formatted accordingly. You will also need to know if you are running EFI or not for the bootloader.

## Install the tarball for the installation.

### Define the variables
```
v=09-02-2021
url=https://github.com/owbut/owbux/releases/download/$v
file=owbux-$v.tar.xz
```

### Download the tarball
The tarball is just the base system, meaning the kernel and the package manager. Everything else, like the bootloader and drivers, will require you to install it manually.  

The packages that are included with Owbux are: base, base-devel (autoconf, automake, binutils, bison, fakeroot, file, findutils, flex, gawk, gcc, gettext, grep, groff, gzip, libtool, m4, make, pacman, patch, pkgconf, sed, sudo, textinfo, which), linux-zen, linux-firmware

### Unpacking the tarball
This will install the base system.
```
> cd /mnt
> tar xvf "/path/to/$file"
```

###  Moving the fstab file
This will allow your system to know what drives to mount on boot.
```
> cp /path/to/fstab /mnt/etc/fstab
```

### Enter the chroot
This will avoid the annoyance of mounting the pseudo filesytems. This will enable the network with in the new installation and will chroot you in as root.
```
> /mnt/bin/owbux-chroot /mnt
```

### Change the locale
Change the locale fitting to your needs.

You will need to change the `/etc/locale.gen` file.

Then you want to run `locale-gen`.

Change the `/etc/locale.conf` file according to the locale you uncommented in `/etc/locale.gen`.

### Change the timezone
To list all avalible timezones do `ls /usr/share/zoneinfo`.

Make a symbolic link from your timezone to `/etc/localtime`.

Sync the hardware clock by running `hwclock --systohc`.

### Add a hostname
To add a hostname edit the `/etc/hostname` file.

Change the `/etc/hosts` file according to the [Arch wiki](https://wiki.archlinux.org/title/Installation_guide#Network_configuration).

### Enable fstrim timer
The fstrim timer will help with SSD life span.

To enable it run `systemctl enable fstrim.timer`

### Change the password and add a user
To change the root password run `passwd`.

To add a user run `useradd` with the flags you want to put aka wheel etc.

To change the password for the new user run `passwd $username`

### Network manager
You will need to install a network manager of your choice. You can install netctl or networkmanager.

### Install drivers
Install all the drivers you need for the system. That includes microcode and GPU drivers.

### Bootloader
Finally you want to install a bootloader to boot into your new system.

### Exit and reboot
Now you will need to exit the chroot and reboot to the new system.
