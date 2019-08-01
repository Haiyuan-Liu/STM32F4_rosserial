# DJI Robomaster STM32F4 + NvidiaTX2 communication with ROS via rosserial_python
## Harware
- Nvidia TX2 installed a Ubuntu 16.04 system and ROS kinetic
- DJI Robomaster development Board Type A, with a STM32F427IIH6 chip
- CH340 divice (convert USB to TTL) 
## Setup for Nvidia TX2
The TX2 lacks a CH340 driver and its original kernal does not support USB. With command `ls -l /dev | grep ttyUSB*` ttyUSB could not be find.
The first step is to updata the TX2 kernal, which can refer to the blog <https://blog.csdn.net/qq_41628231/article/details/81210188>  
1. Down load all the .sh files:  
`git clone https://github.com/jetsonhacks/buildJetsonTX2Kernel.git`  
 `git checkout vL4T28.1`  
 `cd buildJetsonTX2Kernel`  
2. Download the source code of tx2 source kernal: 
`./getKernelSources.sh`  
3. Congif the file to enable the CH340 driver  
4. Compile the code:
`./makeKernel.sh`  
5. Change the boot image: 
`./copyImage.sh`  
6. Restart the system:
`reboot`  
7. The usb device can be found with `ls -l /dev | grep ttyUSB`
## rosserial for STM32
### Motivation
Given the complexity of the protocol between the PC and the STM32 via serial port, it is much more convinent to wrap all the massages into a ROS message. By subscribing the topics, the information can be transfored easily.
### What's more
The CUBEMX project is confied as <https://github.com/BugLiao/rosserial>.  
**Attention:** The clock tree is configed is a little bit tricky. I use the following configeration:    
![text](https://github.com/madeira-sustcer/STM32F4_rosserial/blob/master/images/1.JPG?raw=true)
### Don't worry about this error. The conmunication is ok.  
![text](https://github.com/madeira-sustcer/STM32F4_rosserial/blob/master/images/4.png?raw=true)
### The testing result:
![text](https://github.com/madeira-sustcer/STM32F4_rosserial/blob/master/images/2.png?raw=true)
![text](https://github.com/madeira-sustcer/STM32F4_rosserial/blob/master/images/3.png?raw=true)


