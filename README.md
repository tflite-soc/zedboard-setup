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
  * For JTAG connection execute `install_drivers` script:
    * `sudo <xilinx-install-folder>/Vivado/2019.1/data/xicom/cable_drivers/lin64/install_script/install_drivers/install_drivers`
* Install Vivado HLS

## Zedboard with Xilinux

We want to have OS support on the Zedboard. This step by step guides you on how to install Xillinux on the SD Card, with the necessary Zedboard boot files.

Steps adapted from: `http://xillybus.com/xillinux` and `http://xillybus.com/downloads/doc/xillybus_getting_started_zynq.pdf`.

### Download necessary files

Download the following:

* Boot partition files
  * (Option 1)[Zedboard boot partition](http://xillybus.com/downloads/xillinux-eval-zedboard-2.0c.zip)
  * (Option 2) Files in boot-partition
* [Xillinux OS](http://xillybus.com/downloads/xillinux-2.0.img.gz)

### Follow the steps in the tutorial

Follow the steps from the [Xillibus tutorial](http://xillybus.com/downloads/doc/xillybus_getting_started_zynq.pdf).

* Collect the files needed to boot
  * (OPTION 1) Unzip the boot files `xillinux-eval-board-XXX.zip`
    * Generate the bitstream with Vivado and the `verilog` project (3.3.4 and 3.3.5)
  * (OPTION 2) Download the files from the boot partition folder in this project 
* Copy the image to the SD card (3.4.3)
  * Verify in which partition is the SD Card with `lsblk` (`/dev/sdX`)
  * flash the SD card (be careful to not erase anything on the host PC)
   * `gunzip -c xillinux-2.0.img.gz`
   * `sudo dd if=xillinux-2.0.img of=/dev/sdX bs=64K conv=noerror,sync`
   * `sync # Necessary to flush all the writes to the sd card` 
* Copying the bootfiles and bitstreams to the SD Card image (3.5)
  * Must copy `boot.bin` and `devicetree.dtb` into SD Card first partition `/dev/sdX1`
  * Must copy `xilidemo.bit` generated with Vivado into SD Card first partition `/dev/sdX1`
* Insert SD card into zedboard and make sure that the jumpers are set to boot from the SD card (4.1.1)
* Log to your zedboard using the serial port
  * `minicom -D /dev/ttyACM0 -b 115200 -8 -o`
* Find out the zedboard ip address for ssh connection
  * `ifconfig`
  * on the host `ssh root@10.42.0.196`
* Increase the space of the sd card (4.4.1)


### Files in the boot partition

* uImage  –  The  Linux  kernel  binary.   This  is  the  only  file  in  the  boot  partition after  writing  the  Xillinux  (Micro)SD  image  to  the  card.   The  kernel  is  board-independent.
* boot.bin – The initial bootloader. This file contains the initial processor initializations and the U-boot utility, and is significantly different from board to board.
* devicetree.dtb – The Device Tree Blob file, which contains hardware informationfor the Linux kernel.
* xillydemo.bit – The PL (FPGA) programming file, generated during the Vivado 2019 step
