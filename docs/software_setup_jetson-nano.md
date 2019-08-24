# Software Installation Guide for using a Jetson-Nano.
This guide walks you through the setup of all the software on your jetson-nano.

## Flash Image
You'll need to flash an operating system ([Ubuntu Desktop 18.04](http://releases.ubuntu.com/18.04/)) onto a micro SD card to get started. Although There are plenty of [alternative methods](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write), we use [balenaEtcher](https://www.balena.io/etcher/) to do this.

1. Download the latest [image](https://developer.nvidia.com/jetson-nano-sd-card-image-r322) for Jetson-Nano.
2. Open **balenaEtcher**, `Select image your just downloaded` -> `Select target micro SD card` -> `Flash`
3. Insert the prepared micro SD card to your Jetson-nano's slot, make sure you have mouse and keyboard connected, monitor is hooked up, then power it on. **Note: Use a  `2.4A@5V` power supply with a micro USB plug or a `4A@5V` power supply with 5.5mm OD x 2.5 mm ID barrel jack**
4. The first time your Jetson-Nano powered on will require you to set up your linux account etc.. Follow the prompt to finish the job. Jetson-Nano will reboot automatically after everything was done. 


## [Install AC9260 Driver](https://devtalk.nvidia.com/default/topic/1050449/jetson-nano/intel-9260-wifi-on-jetson-nano-jetbot/post/5364792/#5364792)
```console
# backported drivers
cd ~
git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git

cd backport-iwlwifi
git checkout release/core47
make clean
make defconfig-iwlwifi-public
make -j4
sudo make install

# firmwares
cd ~
git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cd linux-firmware
sudo cp -av ./iwlwifi-9260* /lib/firmware/

sudo reboot
```

## [Use More Memory](https://www.jetsonhacks.com/2019/04/14/jetson-nano-use-more-memory/)
```console
cd ~
git clone https://github.com/JetsonHacksNano/installSwapfile.git
cd installSwapfile
./installSwapfile
```
