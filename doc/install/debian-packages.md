### Install Debian Packages

#### Boot Target Board and login fpga or root user

fpga'password is "fpga".

```console
debian-fpga login: fpga
Password:
fpga@debian-fpga:~$
```

root'password is "admin".

```console
debian-fpga login: root
Password:
root@debian-fpga:~#
```

#### Install Linux Image Package

Since linux-image-6.12.45-zynqmp-fpga-generic_6.12.45-zynqmp-fpga-1_arm64.deb is already pre-installed in debian11-rootfs.tgz, this The process can be omitted.

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i linux-image-6.12.45-zynqmp-fpga-generic_6.12.45-zynqmp-fpga-1_arm64.deb 
Selecting previously unselected package linux-image-6.12.45-zynqmp-fpga-generic.
(Reading database ... 91322 files and directories currently installed.)
Preparing to unpack linux-image-6.12.45-zynqmp-fpga-generic_6.12.45-zynqmp-fpga-1_arm64.deb ...
Unpacking linux-image-6.12.45-zynqmp-fpga-generic (6.12.45-zynqmp-fpga-1) ...
Setting up linux-image-6.12.45-zynqmp-fpga-generic (6.12.45-zynqmp-fpga-1) ...
```

#### Install Linux Headers Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i linux-headers-6.12.45-zynqmp-fpga-generic_6.12.45-zynqmp-fpga-1_arm64.deb 
Selecting previously unselected package linux-headers-6.12.45-zynqmp-fpga-generic.
(Reading database ... 92408 files and directories currently installed.)
Preparing to unpack linux-headers-6.12.45-zynqmp-fpga-generic_6.12.45-zynqmp-fpga-1_arm64.deb ...
Unpacking linux-headers-6.12.45-zynqmp-fpga-generic (6.12.45-zynqmp-fpga-1) ...
Setting up linux-headers-6.12.45-zynqmp-fpga-generic (6.12.45-zynqmp-fpga-1) ...
make: Entering directory '/usr/src/linux-headers-6.12.45-zynqmp-fpga-generic'
  CC      scripts/mod/empty.o
  MKELF   scripts/mod/elfconfig.h
  HOSTCC  scripts/mod/modpost.o
  CC      scripts/mod/devicetable-offsets.s
  HOSTCC  scripts/mod/file2alias.o
  HOSTCC  scripts/mod/sumversion.o
  HOSTCC  scripts/mod/symsearch.o
  HOSTLD  scripts/mod/modpost
make: Leaving directory '/usr/src/linux-headers-6.12.45-zynqmp-fpga-generic'
```

#### Install fclkcfg Device Driver and Services Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i fclkcfg-6.12.45-zynqmp-fpga-generic_1.9.0-1_arm64.deb 
Selecting previously unselected package fclkcfg-6.12.45-zynqmp-fpga-generic.
(Reading database ... 117120 files and directories currently installed.)
Preparing to unpack fclkcfg-6.12.45-zynqmp-fpga-generic_1.9.0-1_arm64.deb ...
Unpacking fclkcfg-6.12.45-zynqmp-fpga-generic (1.9.0-1) ...
Setting up fclkcfg-6.12.45-zynqmp-fpga-generic (1.9.0-1) ...
```

#### Install u-dma-buf Device Driver and Services Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i u-dma-buf-6.12.45-zynqmp-fpga-generic_5.3.0-0_arm64.deb 
Selecting previously unselected package u-dma-buf-6.12.45-zynqmp-fpga-generic.
(Reading database ... 117126 files and directories currently installed.)
Preparing to unpack u-dma-buf-6.12.45-zynqmp-fpga-generic_5.3.0-0_arm64.deb ...
Unpacking u-dma-buf-6.12.45-zynqmp-fpga-generic (5.3.0-0) ...
Setting up u-dma-buf-6.12.45-zynqmp-fpga-generic (5.3.0-0) ...
```

