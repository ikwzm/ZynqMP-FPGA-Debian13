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

Since linux-image-6.12.27-zynqmp-fpga-generic_6.12.27-zynqmp-fpga-2_arm64.deb is already pre-installed in debian11-rootfs.tgz, this The process can be omitted.

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i linux-image-6.12.27-zynqmp-fpga-generic_6.12.27-zynqmp-fpga-3_arm64.deb 
(Reading database ... 40346 files and directories currently installed.)
Preparing to unpack linux-image-6.12.27-zynqmp-fpga-generic_6.12.27-zynqmp-fpga-3_arm64.deb ...
Unpacking linux-image-6.12.27-zynqmp-fpga-generic (6.12.27-zynqmp-fpga-3) over (6.12.27-zynqmp-fpga-3) ...
Setting up linux-image-6.12.27-zynqmp-fpga-generic (6.12.27-zynqmp-fpga-3) ...
```

#### Install Linux Headers Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i linux-headers-6.12.27-zynqmp-fpga-generic_6.12.27-zynqmp-fpga-3_arm64.deb 
Selecting previously unselected package linux-headers-6.12.27-zynqmp-fpga-generic.
(Reading database ... 40346 files and directories currently installed.)
Preparing to unpack linux-headers-6.12.27-zynqmp-fpga-generic_6.12.27-zynqmp-fpga-3_arm64.deb ...
Unpacking linux-headers-6.12.27-zynqmp-fpga-generic (6.12.27-zynqmp-fpga-3) ...
Setting up linux-headers-6.12.27-zynqmp-fpga-generic (6.12.27-zynqmp-fpga-3) ...
make: Entering directory '/usr/src/linux-headers-6.12.27-zynqmp-fpga-generic'
  HOSTCC  scripts/basic/fixdep
  HOSTCC  scripts/dtc/dtc.o
  HOSTCC  scripts/dtc/flattree.o
  HOSTCC  scripts/dtc/fstree.o
  HOSTCC  scripts/dtc/data.o
  HOSTCC  scripts/dtc/livetree.o
  HOSTCC  scripts/dtc/treesource.o
  HOSTCC  scripts/dtc/srcpos.o
  HOSTCC  scripts/dtc/checks.o
  HOSTCC  scripts/dtc/util.o
  HOSTCC  scripts/dtc/dtc-lexer.lex.o
  HOSTCC  scripts/dtc/dtc-parser.tab.o
  HOSTLD  scripts/dtc/dtc
  HOSTCC  scripts/dtc/libfdt/fdt.o
  HOSTCC  scripts/dtc/libfdt/fdt_ro.o
  HOSTCC  scripts/dtc/libfdt/fdt_wip.o
  HOSTCC  scripts/dtc/libfdt/fdt_sw.o
  HOSTCC  scripts/dtc/libfdt/fdt_rw.o
  HOSTCC  scripts/dtc/libfdt/fdt_strerror.o
  HOSTCC  scripts/dtc/libfdt/fdt_empty_tree.o
  HOSTCC  scripts/dtc/libfdt/fdt_addresses.o
  HOSTCC  scripts/dtc/libfdt/fdt_overlay.o
  HOSTCC  scripts/dtc/fdtoverlay.o
  HOSTLD  scripts/dtc/fdtoverlay
  HOSTCC  scripts/selinux/genheaders/genheaders
  HOSTCC  scripts/selinux/mdp/mdp
  HOSTCC  scripts/kallsyms
  HOSTCC  scripts/sorttable
  HOSTCC  scripts/asn1_compiler
  CC      scripts/mod/empty.o
  HOSTCC  scripts/mod/mk_elfconfig
  MKELF   scripts/mod/elfconfig.h
  HOSTCC  scripts/mod/modpost.o
  CC      scripts/mod/devicetable-offsets.s
  HOSTCC  scripts/mod/file2alias.o
  HOSTCC  scripts/mod/sumversion.o
  HOSTCC  scripts/mod/symsearch.o
  HOSTLD  scripts/mod/modpost
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
make[1]: warning:  Clock skew detected.  Your build may be incomplete.
make: warning:  Clock skew detected.  Your build may be incomplete.
make: Leaving directory '/usr/src/linux-headers-6.12.27-zynqmp-fpga-generic'
```

#### Install fclkcfg Device Driver and Services Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i fclkcfg-6.12.27-zynqmp-fpga-generic_1.9.0-1_arm64.deb 
Selecting previously unselected package fclkcfg-6.12.27-zynqmp-fpga-generic.
(Reading database ... 65051 files and directories currently installed.)
Preparing to unpack fclkcfg-6.12.27-zynqmp-fpga-generic_1.9.0-1_arm64.deb ...
Unpacking fclkcfg-6.12.27-zynqmp-fpga-generic (1.9.0-1) ...
Setting up fclkcfg-6.12.27-zynqmp-fpga-generic (1.9.0-1) ...
```

#### Install u-dma-buf Device Driver and Services Package

```console
root@debian-fpga:~# cd /home/fpga/debian
root@debian-fpga:/home/fpga/debian# dpkg -i u-dma-buf-6.12.27-zynqmp-fpga-generic_5.3.0-0_arm64.deb 
Selecting previously unselected package u-dma-buf-6.12.27-zynqmp-fpga-generic.
(Reading database ... 65057 files and directories currently installed.)
Preparing to unpack u-dma-buf-6.12.27-zynqmp-fpga-generic_5.3.0-0_arm64.deb ...
Unpacking u-dma-buf-6.12.27-zynqmp-fpga-generic (5.3.0-0) ...
Setting up u-dma-buf-6.12.27-zynqmp-fpga-generic (5.3.0-0) ...
```

