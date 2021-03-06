# Installing the Cross Tools for ARM 

This page shows you how to install the tools to build, run, and debug Mynewt OS applications that run on supported ARM target boards.  It shows you how to install the following tools on macOS, Linux and Windows:

* ARM cross toolchain to compile and build Mynewt applications for the target boards.
* Debuggers to load and debug applications on the target boards.

<br>

## Installing the ARM Cross Toolchain
ARM maintains a pre-built GNU toolchain with gcc and gdb targeted at Embedded ARM Processors, namely Cortex-R/Cortex-M processor families. Mynewt OS has been tested with version 7.2 of the toolchain and we recommend you install 7.0 or later to get started.  Mynewt OS will eventually work with multiple versions available, including the latest releases. 

### Installing the ARM Toolchain For Mac OS X

Add the **PX4/homebrew-px4** homebrew tap and install version 7.2 of the toolchain. After installing, check that the symbolic link that homebrew created points to the correct version of the debugger.

```no-highlight
$ brew tap PX4/homebrew-px4
$ brew update
$ brew install gcc-arm-none-eabi-74
$ arm-none-eabi-gcc --version
arm-none-eabi-gcc (GNU Tools for Arm Embedded Processors 7-2017-q4-major) 7.2.1 20170904 (release) [ARM/embedded-7-branch revision 255204]
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
$ ls -al /usr/local/bin/arm-none-eabi-gcc
lrwxr-xr-x  1 ccollins  admin  58 Jul  5 18:12 /usr/local/bin/arm-none-eabi-gcc -> ../Cellar/gcc-arm-none-eabi/20171218/bin/arm-none-eabi-gcc
```

**Note:** If no version is specified, brew will install the latest version available. 

<br>
### Installing the ARM Toolchain For Linux

On a Debian-based Linux distribution, gcc 7 for ARM can be installed with
apt-get as documented below. The steps are explained in depth at
[https://launchpad.net/~team-gcc-arm-embedded/+archive/ubuntu/ppa](https://launchpad.net/~team-gcc-arm-embedded/+archive/ubuntu/ppa).

```no-highlight
$ sudo apt-get remove binutils-arm-none-eabi gcc-arm-none-eabi 
$ sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa
$ sudo apt-get update 
$ sudo apt-get install gcc-arm-embedded
```
<br>
### Installing the ARM Toolchain for Windows
Step 1: Download and run the [installer](https://developer.arm.com/-/media/Files/downloads/gnu-rm/7-2018q2/gcc-arm-none-eabi-7-2018-q2-update-win32-sha2.exe?revision=bc72768f-9927-454e-9141-918927fb74ff?product=GNU%20Arm%20Embedded%20Toolchain,32-bit,,Windows,7-2018-q2-update) to install arm-none-eabi-gcc and arm-none-eabi-gdb. Select the default destination folder: **C:\Program Files (x86)\GNU Tools Arm Embedded\7 2018-q2-update**.

**Notes:** 

* Check the `Add path to environment variable` option before you click the `Finish` button for the installation. 
* You may select a different folder but the installation instructions use the default values.

Step 2: Check that you are using the installed versions arm-none-eabi-gcc and arm-none-eabi-gdb.  Open a MinGW terminal and run the `which` commands. 

**Note:** You must start a new MinGW terminal to inherit the new **Path** values.

```no-highlight
$ which arm-none-eabi-gcc
/c/Program Files (x86)/GNU Tools Arm Embedded/7 2018-q2-update/bin/arm-none-eabi-gcc
$ which arm-none-eabi-gdb
/c/Program Files (x86)/GNU Tools Arm Embedded/7 2018-q2-update/bin/arm-none-eabi-gdb
```
## Installing the Debuggers 
Mynewt uses, depending on the board, either the OpenOCD or SEGGER J-Link debuggers. 
<br>
### Installing the OpenOCD Debugger
OpenOCD (Open On-Chip Debugger) is open-source software that allows your
computer to interface with the JTAG debug connector on a variety of boards.  A
JTAG connection lets you debug and test embedded target devices. For more on
OpenOCD go to [http://openocd.org](http://openocd.org).

OpenOCD version 0.10.0 with nrf52 support is required.  A binary for this version is available to download for Mac OS, Linux, and Windows.

<br>
#### Installing OpenOCD on Mac OS
Step 1: Download the [binary tarball for Mac OS](https://github.com/runtimeco/openocd-binaries/raw/master/openocd-bin-0.10.0-MacOS.tgz).

Step 2: Change to the root directory: 
```no-highlight 
$cd / 
```
<br>
Step 3: Untar the tarball and install into ** /usr/local/bin**.  You will need to replace ** ~/Downloads ** with the directory that the tarball is downloaded to.  
```no-highlight
sudo tar -xf ~/Downloads/openocd-bin-0.10.0-MacOS.tgz
```
<br>
Step 4: Check the OpenOCD version you are using.  

```no-highlight
$which openocd
/usr/local/bin/openocd
$openocd -v
Open On-Chip Debugger 0.10.0
Licensed under GNU GPL v2
For bug reports, read
http://openocd.org/doc/doxygen/bugs.html
```

You should see version: **0.10.0**. 

If you see one of these errors:

* Library not loaded: /usr/local/lib/libusb-0.1.4.dylib -  Run `brew install libusb-compat`.
* Library not loaded: /usr/local/opt/libftdi/lib/libftdi1.2.dylib - Run `brew install libftdi`.
* Library not loaded: /usr/local/lib/libhidapi.0.dylib - Run `brew install hidapi`.

<br>
#### Installing OpenOCD on Linux 
Step 1: Download the [binary tarball for Linux](https://github.com/runtimeco/openocd-binaries/raw/master/openocd-bin-0.10.0-Linux.tgz)

Step 2: Change to the root directory: 
``` 
$cd / 
```
<br>
Step 3: Untar the tarball and install into ** /usr/local/bin**.  You will need to replace ** ~/Downloads ** with the directory that the tarball is downloaded to.  

** Note:** You must specify the -p option for the tar command.

```no-highlight
$sudo tar -xpf ~/Downloads/openocd-bin-0.10.0-Linux.tgz
```
<br>
Step 4: Check the OpenOCD version you are using: 

```no-highlight
$which openocd
/usr/local/bin/openocd
$openocd -v
Open On-Chip Debugger 0.10.0
Licensed under GNU GPL v2
For bug reports, read
http://openocd.org/doc/doxygen/bugs.html
```
You should see version: **0.10.0**. 

If you see any of these error messages:

* openocd: error while loading shared libraries: libhidapi-hidraw.so.0: cannot open shared object file: No such file or directory

* openocd: error while loading shared libraries: libusb-1.0.so.0: cannot open shared object file: No such file or directory 

run the following command to install the libraries: 
```no-highlight
$sudo apt-get install libhidapi-dev:i386
```
<br>
#### Installing OpenOCD on Windows 
Step 1: Download the [binary zip file for Windows](https://github.com/runtimeco/openocd-binaries/raw/master/openocd-0.10.0.zip).

Step 2: Extract into the **C:\openocd-0.10.0** folder. 

Step 3: Add the path: ** C:\openocd-0.10.0\bin** to your Windows User **Path** environment variable.  Note: You must add **bin** to the path.

Step 4: Check the OpenOCD version you are using.  Open a new MinGW terminal and run the following commands: 

**Note:** You must start a new MinGW terminal to inherit the new **Path** values.

```no-highlight
$which openocd
/c/openocd-0.10.0/bin/openocd
$openocd -v
Open On-Chip Debugger 0.10.0
Licensed under GNU GPL v2
For bug reports, read
        http://openocd.org/doc/doxygen/bugs.html
```
You should see version: **0.10.0**. 

<br>
###Installing SEGGER J-Link 
You can download and install Segger J-LINK Software and documentation pack from [SEGGER](https://www.segger.com/jlink-software.html). 

**Note:** On Windows, perform the following additonal steps:

* Make note of the destination folder of your installation.
* Add the installation destination folder path to your Windows user **Path** environment variable.  You do not need to add **bin** to the path.
* Open a new MinGW terminal to inherit the new **Path** values.
