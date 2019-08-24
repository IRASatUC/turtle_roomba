# Software Installation Guide for using a Jetson-Nano.
This guide walks you through the setup of all the software on your jetson-nano.

## Flash Image
You'll need to flash an operating system ([Ubuntu Desktop 18.04](http://releases.ubuntu.com/18.04/)) onto a micro SD card to get started. Although There are plenty of [alternative methods](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write), we use [balenaEtcher](https://www.balena.io/etcher/) to do this.

1. Download the latest [image](https://developer.nvidia.com/jetson-nano-sd-card-image-r322) for Jetson-Nano.
2. Open **balenaEtcher**, `Select image your just downloaded` -> `Select target micro SD card` -> `Flash`
3. Insert the prepared micro SD card to your Jetson-nano's slot, make sure you have mouse and keyboard connected, monitor is hooked up, then power it on. **Note: Use a  `2.4A@5V` power supply with a micro USB plug or a `4A@5V` power supply with 5.5mm OD x 2.5 mm ID barrel jack**
4. The first time your Jetson-Nano powered on will require you to set up your linux account etc.. Follow the prompt to finish the job. Jetson-Nano will reboot automatically after everything was done. 


