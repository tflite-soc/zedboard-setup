# zedboard-setup
How to setup the host and zedboard so that running tflite is possible.

These steps have been performed using a ubuntu-16.04 host system

## Hardware requirements

* Host pc running a Vivado compatible distribution
* Zedboard
* SD card (8 to 32 GB)
* Ethernet cable and Ethernet to USB adapter (for ssh connection)
* USB to micro-USB cable (for serial connection)

## Host Requirements

* Install Docker
* Install Vivado 2019.x
  * For JTAG connection execute install_drivers script:
    * `sudo <xilinx-install-folder>/Vivado/2019.1/data/xicom/cable_drivers/lin64/install_script/install_drivers/install_drivers`
* Install Vivado HLS

## Zedboard with Xilinux

We want to have OS support on the Zedboard. This step by step guides you on how to install Xillinux on the SD Card, with the necessary Zedboard boot files.

### Download necessary files

Steps adapted from: `http://xillybus.com/xillinux` and `http://xillybus.com/downloads/doc/xillybus_getting_started_zynq.pdf`.

Download the following:
* [Zedboard boot partition](http://xillybus.com/downloads/xillinux-eval-zedboard-2.0c.zip)
* [Xillinux OS](http://xillybus.com/downloads/xillinux-2.0.img.gz)


### Files in the boot partition

* uImage  –  The  Linux  kernel  binary.   This  is  the  only  file  in  the  boot  partition after  writing  the  Xillinux  (Micro)SD  image  to  the  card.   The  kernel  is  board-independent.
* boot.bin – The initial bootloader. This file contains the initial processor initializations and the U-boot utility, and is significantly different from board to board.
* devicetree.dtb – The Device Tree Blob file, which contains hardware informationfor the Linux kernel.
* xillydemo.bit – The PL (FPGA) programming file, generated during the Vivado 2019 step
