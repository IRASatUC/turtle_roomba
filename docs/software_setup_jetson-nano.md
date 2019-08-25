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

## [Librealsense](https://www.jetsonhacks.com/2019/05/16/jetson-nano-realsense-depth-camera/)
**Note: **Thie will take about a hour, so be patient.
```console
cd ~
git clone https://github.com/jetsonhacksnano/installLibrealsense.git
cd installLibrealsense
./installLibrealsense.sh
./patchUbuntu.sh
```
> Enter your password according to the prompt in the middle of the process.

## [Install ROS Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu)
```console
# setup source.list
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# installation
sudo apt update
sudo apt install ros-melodic-ros-base
sudo rosdep init
rosdep update

# post installation
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc

# install essential software
sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential python-catkin-tools
```

## Create a ROS Workspace
```console
cd ~
mkdir -p ros_ws/src
cd ros_ws
catkin init

# setup workspcae environment
echo "source $HOME/ros_ws/devel/setup.bash" >> ~/.bashrc
```

## [Install RealSenseRos](https://github.com/JetsonHacksNano/installRealSenseROS)
```console 
cd ~
git clone https://github.com/JetsonHacksNano/installRealSenseROS.git
cd installRealSenseROS
./installRealSenseROS.sh ros_ws
```

## Build ROS Packages for iRobot Create 2
```console
cd ~/ros_ws/src

# download packages
git clone https://github.com/AutonomyLab/create_autonomy.git
cd create_autonomy
git clone https://github.com/AutonomyLab/libcreate.git

# build libcreate (a C++ library for interfacing with iRobot's Create 1 and 2 as well as most models of Roomba)
cd ~/ros_ws
catkin build libcreate

# build create_autonomy
rosdep update  
rosdep install --from-paths src -i
catkin build create_autonomy

# USB permission
sudo usermod -a -G dialout $USER
rsudo eboot
```

## [Install rtabmap_ros](http://wiki.ros.org/rtabmap_ros)
```console
sudo apt update
sudo apt install ros-melodic-rtabmap-ros
```
