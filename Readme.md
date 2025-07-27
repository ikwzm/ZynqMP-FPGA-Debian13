ZynqMP-FPGA-Debian13
====================================================================================

Overview
------------------------------------------------------------------------------------

### Introduction

This Repository provides a Linux Boot Image(U-boot, Kernel, Debian 13 RootFS) for Zynq MPSoC.

### Note

**The Linux Kernel Image and Debian11 RootFS provided in this repository is not official.**

**I modified it to my liking. Please handle with care.**


### Features

* Hardware
  + Ultra96    : Xilinx Zynq UltraScale+ MPSoC development board based on the Linaro 96Boards specification. 
  + Ultra96-V2 : updates and refreshes the Ultra96 product that was released in 2018.
  + KV260      : Kria KV260 Vision AI Startar Kit.
  + KR260      : Kria KR260 Robotics  Startar Kit.
* Boot Loader
  + FSBL(First Stage Boot Loader for ZynqMP)
  + PMU Firmware(Platform Management Unit Firmware)
  + BL31(ARM Trusted Firmware Boot Loader stage 3-1)
  + U-Boot xilinx-v2019.2 (customized)
* [Linux Kernel Version 6.12.27-zynqmp-fpga-generic](https://github.com/ikwzm/ZynqMP-FPGA-Linux-Kernel-6.12/tree/6.12.27-zynqmp-fpga-generic-3)
  + [linux-stable 6.12.27](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git//tag/?h=v6.12.27)
  + Patched equivalent to linux-xlnx v2025.1
  + Enable Device Tree Overlay with Configuration File System
  + Enable FPGA Manager
  + Enable FPGA Bridge
  + Enable FPGA Reagion
  + Enable ATWILC3000 Linux Driver for Ultra96-V2
* Debian13(trixie) Root File System
  + Installed build-essential
  + Installed device-tree-compiler
  + Installed ruby ruby-msgpack ruby-serialport
  + Installed python python3 python3-numpy msgpack-rpc-python
  + Installed u-boot-tools
  + Installed Other package list -> [files/debian13-dpkg-list.txt](files/debian12-dpkg-list.txt)
* FPGA Device Drivers and Services
  + [fclkcfg    (FPGA Clock Configuration Device Driver)](https://github.com/ikwzm/fclkcfg)
  + [u-dma-buf  (User space mappable DMA Buffer)](https://github.com/ikwzm/udmabuf)

Release
------------------------------------------------------------------------------------

**This project is currently under construction.**

