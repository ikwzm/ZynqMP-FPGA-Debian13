### Build Debian13 RootFS

#### Prepare Linux Kernel Image Debian Package

[./doc/build/linux-kernel-6.12.27-zynqmp-fpga-generic.md](linux-kernel-6.12.27-zynqmp-fpga-generic.md)

#### Prepare the necessary packages

```console
shell$ sudo apt install debootstrap
```

If you are building on a different architecture, use qemu.

```console
shell$ sudo apt install qemu-user-static binfmt-support
```

#### Setup parameters 

```console
shell$ export targetdir=debian13-rootfs
shell$ export distro=trixie
```

#### Build Debian RootFS first-step in $targetdir(=debian13-rootfs)

```console
shell$ mkdir                                            $PWD/$targetdir
shell$ sudo chown root                                  $PWD/$targetdir
shell$ sudo debootstrap --arch=arm64 --foreign $distro  $PWD/$targetdir
shell$ sudo cp /etc/resolv.conf                         $PWD/$targetdir/etc
shell$ sudo cp scripts/build-debian13-rootfs-second.sh  $PWD/$targetdir
shell$ sudo cp debian/linux-image-*.deb                 $PWD/$targetdir
```

If you are using qemu, add qemu-aarch64-static as well.

```console
shell$ sudo cp /usr/bin/qemu-aarch64-static $PWD/$targetdir/usr/bin
```

If you get an error like the following, debootstrap does not yet support bookworm in your environment.

```console
shell$ sudo debootstrap --arch=arm64 --foreign $distro $PWD/$targetdir
E: No such script: /usr/share/debootstrap/scripts/bookworm
```

Please install a debootstrap that does not support bookworm as follows

```console
shell$ sudo dpkg -i debian/debootstrap_1.0.128+nmu2_all.deb
```

#### Build Debian RootFS second-step

##### Change Root to debian13-rootfs

```console
shell$ sudo chroot $PWD/$targetdir
```

There are two ways

1. run build-debian13-rootfs-second.sh (easy)
2. run this chapter step-by-step (annoying)

##### Run debootstrap second stage

```console
debian13-rootfs# distro=trixie
debian13-rootfs# export LANG=C
debian13-rootfs# /debootstrap/debootstrap --second-stage
```

##### Setup APT

```console
debian13-rootfs# cat <<EOT > /etc/apt/sources.list
deb     http://ftp.jp.debian.org/debian  trixie           main contrib non-free non-free-firmware
deb-src http://ftp.jp.debian.org/debian  trixie           main contrib non-free non-free-firmware
deb     http://ftp.jp.debian.org/debian  trixie-updates   main contrib non-free non-free-firmware
deb-src http://ftp.jp.debian.org/debian  trixie-updates   main contrib non-free non-free-firmware
deb     http://security.debian.org       trixie-security  main contrib non-free non-free-firmware
deb-src http://security.debian.org       trixie-security  main contrib non-free non-free-firmware
EOT
```

```console
debian13-rootfs# cat <<EOT > /etc/apt/apt.conf.d/71-no-recommends
APT::Install-Recommends "0";
APT::Install-Suggests   "0";
EOT
```

```console
debian13-rootfs# apt update -y
debian13-rootfs# apt upgrade -y
```

##### Install applications

```console
debian13-rootfs# apt install -y locales dialog
debian13-rootfs# dpkg-reconfigure locales
debian13-rootfs# apt install -y net-tools openssh-server resolvconf sudo less hwinfo tcsh zsh file wget chrony
```

please select "97. en_US.UTF-8 UTF-8" and "2. C.UTF-8"

##### Setup hostname

```console
debian13-rootfs# echo debian-fpga > /etc/hostname
```

##### Setup root password

```console
debian13-rootfs# passwd
```

This time, we set the "admin" at the root' password.

To be able to login as root from Zynq serial port.

```console
debian13-rootfs# cat <<EOT >> /etc/securetty
# Serial Port for Xilinx ZynqMP
ttyPS0
ttyPS1
EOT
```

##### Add a new guest user

```console
debian13-rootfs# adduser fpga
```

This time, we set the "fpga" at the fpga'password.

```console
debian13-rootfs# apt install -y sudo
debian13-rootfs# echo "fpga ALL=(ALL:ALL) ALL" > /etc/sudoers.d/fpga
```

##### Setup sshd config

```console
debian13-rootfs# apt install -y ssh
debian13-rootfs# sed -i -e 's/#PasswordAuthentication/PasswordAuthentication/g' /etc/ssh/sshd_config
```

##### Setup Time Zone

```console
debian13-rootfs# dpkg-reconfigure tzdata
```

or if noninteractive set to Asia/Tokyo

```console
debian13-rootfs# echo "Asia/Tokyo" > /etc/timezone
debian13-rootfs# dpkg-reconfigure -f noninteractive tzdata
```


##### Setup fstab

```console
debian13-rootfs# cat <<EOT > /etc/fstab
none		/config		configfs	defaults	0	0
EOT
````

##### Setup Network

```console
debian13-rootfs# apt install -y ifupdown
debian13-rootfs# cat <<EOT > /etc/network/interfaces.d/eth0
allow-hotplug eth0
iface eth0 inet dhcp
EOT
````

##### Setup /lib/firmware

```console
debian13-rootfs# mkdir /lib/firmware
debian11-rootfs# mkdir /lib/firmware/ti-connectivity
debian11-rootfs# mkdir /lib/firmware/mchp
```

##### Install Development applications

```console
debian13-rootfs# apt install -y build-essential
debian13-rootfs# apt install -y git git-lfs
debian13-rootfs# apt install -y u-boot-tools device-tree-compiler
debian13-rootfs# apt install -y libssl-dev
debian13-rootfs# apt install -y socat
debian13-rootfs# apt install -y ruby rake ruby-msgpack ruby-serialport 
debian13-rootfs# apt install -y python3 python3-dev python3-setuptools python3-wheel python3-pip python3-numpy
debian13-rootfs# apt install -y flex bison pkg-config
debian13-rootfs# apt install -y file dosfstools
```

### Install Wireless tools and firmware

```console
debian13-rootfs# apt install -y wireless-tools
debian13-rootfs# apt install -y wpasupplicant
debian13-rootfs# apt install -y firmware-realtek
debian13-rootfs# apt install -y firmware-ralink
```

Note: If the version of wl18xx-fw-4.bin is 8.9.1.0.0 or later, it will not work, so use 8.9.0.0.90.

```console
debian13-rootfs# git clone git://git.ti.com/wilink8-wlan/wl18xx_fw.git
debian13-rootfs# cd wl18xx_fw && git checkout d2588c16809ecca8e0dc7ea011fc6180c7b08a92 && cd ..
debian13-rootfs# cp wl18xx_fw/wl18xx-fw-4.bin /lib/firmware/ti-connectivity
debian13-rootfs# rm -rf wl18xx_fw/
```

```console
debian13-rootfs# git clone git://git.ti.com/wilink8-bt/ti-bt-firmware
debian13-rootfs# cp ti-bt-firmware/TIInit_11.8.32.bts /lib/firmware/ti-connectivity
debian13-rootfs# rm -rf ti-bt-firmware
```

```console
debian13-rootfs# git clone https://github.com/linux4wilc/firmware  linux4wilc-firmware  
debian13-rootfs# cp linux4wilc-firmware/*.bin /lib/firmware/mchp
debian13-rootfs# rm -rf linux4wilc-firmware  
```

##### Install Other applications

```console
debian13-rootfs# apt install -y samba
debian13-rootfs# apt install -y avahi-daemon
```

##### Install Linux Modules

```console
debian13-rootfs# mkdir /mnt/boot
debian13-rootfs# dpkg -i linux-image-*.deb
```

##### Clean APT Cache

```console
debian13-rootfs# apt clean
```

##### Create Debian Package List

```console
debian13-rootfs# dpkg -l > dpkg-list.txt
```

##### Finish

```console
debian13-rootfs# exit
shell$ sudo rm -f $PWD/$targetdir/build-debian13-rootfs-second.sh
shell$ sudo rm -f $PWD/$targetdir/linux-image-*.deb
shell$ sudo mv    $PWD/$targetdir/dpkg-list.txt files/debian13-dpkg-list.txt
```

If you used qemu, remove qemu-aarch64-static

```console
shell$ sudo rm -f $PWD/$targetdir/usr/bin/qemu-aarch64-static
```

#### Build debian13-rootfs-vanilla.tgz

```console
shell$ cd $PWD/$targetdir
shell$ sudo tar cfz ../debian13-rootfs-vanilla.tgz *
shell$ cd ..
```

#### Build debian13-rootfs-vanilla.tgz.files

```console
shell$ mkdir debian13-rootfs-vanilla.tgz.files
shell$ cd    debian13-rootfs-vanilla.tgz.files
shell$ split -d --bytes=40M ../debian13-rootfs-vanilla.tgz
shell$ cd ..
```
