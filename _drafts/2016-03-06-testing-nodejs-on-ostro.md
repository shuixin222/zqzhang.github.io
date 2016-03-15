---
layout: post
type: post
title: Testing Node.js on Ostro
---

Awesome! Ostro OS, a Linux based operating system optimized for the Internet of
Things, is pre-released with Node.js application framework support. This article
introduces how we tested the Node.js, node modules and additional JavaScript
APIs supported by the Ostro OS with Intel Edison Kit for Arduino.

## Introducing Ostro OS

> Ostro™ OS is a Linux based operating system optimized for the Internet of
  Things. This OS is built with security in mind, and integrates rigorous
  security reviews through all stages of development.

It supports the following features related to Node.js:

* Application Framework support for Node.js, Python and C/C++ applications
* RESTful APIs for System Status and Open Connectivity Foundation (OCF)
  resource discovery
* JavaScript APIs based on the OCF specifications
* Security features: Trusted Boot, Applications Memory Isolation and
  Impersonation Prevention, Integrity Verification

See [release notes](https://github.com/ostroproject/ostro-os/releases) and
[https://ostroproject.org/](https://ostroproject.org/) for details.

## Introducing Intel Edison

> an ultra small Intel® Atom™ SoC dual-core 32-bit CPU-based compute module
  aimed at small IoT and wearable computing products.

There are a document for [getting
started](https://software.intel.com/en-us/iot/library/edison-getting-started)
and some
[instructions](https://software.intel.com/en-us/assembling-intel-edison-board-with-arduino-expansion-board)
to help you assemble the Intel Edison board with the Arduino expansion board.
  
There are also a [product brief for boards and
kits](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005664.html)
which describes the features and benefits and high-level specifications, and a
[Edison board
specification](http://download.intel.com/support/edison/sb/edison_pb_331179002.pdf).

## Flashing Ostro image to Intel Edison

Ostro Project website has some documents for [building Ostro OS
images](https://ostroproject.org/documentation/howtos/building-images.html)
and [booting and installing an Ostro OS
image](https://ostroproject.org/documentation/howtos/booting-and-installation.html).
But here we start from downloading the [pre-release
image](https://download.ostroproject.org/releases/ostro-os/milestone/v1.0.0-pre/)
on a development machine (host) with Ubuntu 14.04 and then flash the image
to Intel Edison following these steps:

1. Plug in a micro-USB cable to the J3 connector on the board (corner next to
   the FTDI chip).
2. Flip the DIP switch towards jumper J16.
3. Open the terminal program on host computer to attach to the serial console.
4. Download the `ostro-image-dev-edison` image.
5. Extract the image, enter the `toFlash` sub-directly and execute the
   `flashall.sh` script:
   ```
   $ tar xzvf ostro-image-dev-edison-<build>.toflash.tar.bz2
   $ cd toFlash
   $ sudo ./flashall.sh
   ```
6. Plug in the second micro-USB cable to the J16 connector as instructed by
   the running flashall script.
7. Wait for all the images to flash. You will see the progress on both the
   flasher and on the serial console.
8. Once flashing is done, the image will automatically boot up and auto-login
   as root, no password is required.

To remote access the Ostro OS, however, we need to do something additionally
because by default the Ostro OS prevents logging in remotely using SSH.
We need to generate a private/public key pair to enable SSH access to the
target device.

1. Prepare an ssh key pair on the workstation, either using an existing host
   ssh key pair (in `$HOME/.ssh/`), or by generating a new ssh key pair (refer
   to this [generating an ssh key
   help](https://help.github.com/articles/generating-an-ssh-key/)).
2. Connect to the target device using a serial port terminal program, for
   example:
   ```
   $ sudo screen /dev/ttyUSB0 115200
   ```
3. Save the contents from your workstation’s `$HOME/.ssh/id_rsa.pub` public key
   file to the device's `$HOME/.ssh/authorized_keys` , either by editing the
   `authorized_keys` file with `vi` or copying it using a USB thumbdrive.
4. Make note of the device's IP address (using `ifconfig`) and reboot the device.
5. Login from the host using ssh with the private key (from host) and the IP
   address of your device, for example:
   ```
   # ssh root@192.168.2.2 -i $HOME/.ssh/id_rsa
   ```

## Testing Node.js
