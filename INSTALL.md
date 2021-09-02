# Installation

Before we get started with the installation make sure you have a live CD/USB of a random Linux distribution. Make sure you have an fstab file ready and the disk should be mounted on /mnt. All disks should be formatted accordingly.

## Install the tarball for the installation.

### Define the variables
```
v=9-2-2021
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

### Enter the chroot
This will avoid the annoyance of mounting the pseudo filesytems. This will enable the network with in the new installation and will chroot you in as root.
```
> /mnt/bin/owbux-chroot /mnt
```
