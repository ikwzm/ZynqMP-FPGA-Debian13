### Build Linux Kernel 6.12.27-zynqmp-fpga-generic

#### Download ZynqMP-FPGA-Linux-Kernel-6.12

```console
shell$ wget https://github.com/ikwzm/ZynqMP-FPGA-Linux-Kernel-6.12/archive/refs/tags/6.12.27-zynqmp-fpga-generic-3.tar.gz
shell$ tar xfz 6.12.27-zynqmp-fpga-generic-3.tar.gz
```

#### Setup parameters

```console
shell$ export LINUX_KERNEL_REPOSITORY=ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3
shell$ export LINUX_KERNEL_VERSION=6.12.27
shell$ export LINUX_KERNEL_RELEASE=$LINUX_KERNEL_VERSION-zynqmp-fpga-generic
```


#### Copy Linux Kernel Image to this repository

```console
shell$ install -d ./files
shell$ cp $LINUX_KERNEL_REPOSITORY/vmlinuz-$LINUX_KERNEL_RELEASE-*      ./files
shell$ cp $LINUX_KERNEL_REPOSITORY/files/config-$LINUX_KERNEL_RELEASE-* ./files
```

#### Copy Linux Image and Header Debian Packages to this repository

```console
shell$ install -d ./debian
shell$ cp $LINUX_KERNEL_REPOSITORY/linux-image-$LINUX_KERNEL_RELEASE_*.deb   ./debian
shell$ cp $LINUX_KERNEL_REPOSITORY/linux-headers-$LINUX_KERNEL_RELEASE_*.deb ./debian
```

#### Copy devicetree for KV260

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-$LINUX_KERNEL_RELEASE.sh -d ./target/Kv260/boot -U -v kv260
# SCRIPT NAME     =  ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/scripts/install-linux-6.12.27-zynqmp-fpga-generic.sh
# SCRIPT VERSION  =  0.3
# KERNEL_RELEASE  =  6.12.27-zynqmp-fpga-generic
# BUILD_VERSION   =  3
# TARGET          =  kv260_revB
# TARGET_DIRECTRY =  ./target/Kv260/boot
install -d ./target/Kv260/boot
gzip -d -c /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/vmlinuz-6.12.27-zynqmp-fpga-generic-3 > ./target/Kv260/boot/image-6.12.27-zynqmp-fpga-generic
# do_install_dtb(kv260_revB)
cp /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/devicetrees/6.12.27-zynqmp-fpga-generic-3/zynqmp-kv260-revB.dtb ./target/Kv260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kv260-revB.dtb
dtc -I dtb -O dts --symbols -o ./target/Kv260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kv260-revB.dts ./target/Kv260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kv260-revB.dtb
# do_generate_uenv(kv260_revB)
# cat ... > ./target/Kv260/boot/uEnv-linux-6.12.27-zynqmp-fpga-generic.txt
```

#### Copy devicetree for KR260

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-$LINUX_KERNEL_RELEASE.sh -d ./target/Kr260/boot -U -v kr260
# SCRIPT NAME     =  ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/scripts/install-linux-6.12.27-zynqmp-fpga-generic.sh
# SCRIPT VERSION  =  0.3
# KERNEL_RELEASE  =  6.12.27-zynqmp-fpga-generic
# BUILD_VERSION   =  3
# TARGET          =  kr260_revB
# TARGET_DIRECTRY =  ./target/Kr260/boot
install -d ./target/Kr260/boot
gzip -d -c /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/vmlinuz-6.12.27-zynqmp-fpga-generic-3 > ./target/Kr260/boot/image-6.12.27-zynqmp-fpga-generic
# do_install_dtb(kr260_revB)
cp /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/devicetrees/6.12.27-zynqmp-fpga-generic-3/zynqmp-kr260-revB.dtb ./target/Kr260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kr260-revB.dtb
dtc -I dtb -O dts --symbols -o ./target/Kr260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kr260-revB.dts ./target/Kr260/boot/devicetree-6.12.27-zynqmp-fpga-generic-kr260-revB.dtb
# do_generate_uenv(kr260_revB)
# cat ... > ./target/Kr260/boot/uEnv-linux-6.12.27-zynqmp-fpga-generic.txt
```

#### Copy devicetree for Ultra96

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-$LINUX_KERNEL_RELEASE.sh -d ./target/Ultra96/boot -U -v ultra96
# SCRIPT NAME     =  ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/scripts/install-linux-6.12.27-zynqmp-fpga-generic.sh
# SCRIPT VERSION  =  0.3
# KERNEL_RELEASE  =  6.12.27-zynqmp-fpga-generic
# BUILD_VERSION   =  3
# TARGET          =  ultra96
# TARGET_DIRECTRY =  ./target/Ultra96/boot
install -d ./target/Ultra96/boot
gzip -d -c /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/vmlinuz-6.12.27-zynqmp-fpga-generic-3 > ./target/Ultra96/boot/image-6.12.27-zynqmp-fpga-generic
# do_install_dtb(ultra96)
cp /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/devicetrees/6.12.27-zynqmp-fpga-generic-3/avnet-ultra96-rev1.dtb ./target/Ultra96/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96.dtb
dtc -I dtb -O dts --symbols -o ./target/Ultra96/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96.dts ./target/Ultra96/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96.dtb
# do_generate_uenv(ultra96)
# cat ... > ./target/Ultra96/boot/uEnv-linux-6.12.27-zynqmp-fpga-generic.txt
```

#### Copy devicetree for Ultra96-V2

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-$LINUX_KERNEL_RELEASE.sh -d ./target/Ultra96-V2/boot -U -v ultra96v2
# SCRIPT NAME     =  ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/scripts/install-linux-6.12.27-zynqmp-fpga-generic.sh
# SCRIPT VERSION  =  0.3
# KERNEL_RELEASE  =  6.12.27-zynqmp-fpga-generic
# BUILD_VERSION   =  3
# TARGET          =  ultra96v2
# TARGET_DIRECTRY =  ./target/Ultra96-V2/boot
install -d ./target/Ultra96-V2/boot
gzip -d -c /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/vmlinuz-6.12.27-zynqmp-fpga-generic-3 > ./target/Ultra96-V2/boot/image-6.12.27-zynqmp-fpga-generic
# do_install_dtb(ultra96v2)
cp /home/fpga/work/ZynqMP-FPGA-Debian13/ZynqMP-FPGA-Linux-Kernel-6.12-6.12.27-zynqmp-fpga-generic-3/devicetrees/6.12.27-zynqmp-fpga-generic-3/avnet-ultra96v2-rev1.dtb ./target/Ultra96-V2/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96v2.dtb
dtc -I dtb -O dts --symbols -o ./target/Ultra96-V2/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96v2.dts ./target/Ultra96-V2/boot/devicetree-6.12.27-zynqmp-fpga-generic-ultra96v2.dtb
# do_generate_uenv(ultra96v2)
# cat ... > ./target/Ultra96-V2/boot/uEnv-linux-6.12.27-zynqmp-fpga-generic.txt
```

