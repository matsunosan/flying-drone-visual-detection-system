# **Flying Drone Visual Detection System**  
*A real-time object detection and classification system for UAVs (Unmanned Aerial Vehicles), designed for military and surveillance applications.*

## **Project Overview**  
The **Flying Drone Visual Detection System** is a computer vision-based system that enables UAVs to detect, classify, and differentiate between various objects in real-time. The system is built using deep learning models, integrated with ROS (Robot Operating System), and tested in simulation environment.

## Prerequisites
- Ubuntu
- ROS
- Gazebo
- Ardupilot
- Ardupilot_gazebo plugin
- Docker
- Mavproxy

## Installation
### Ubuntu
Ubuntu 20.04 inside a Virtual Machine (VM) used in this tutorial.

### ROS
The ROS noetic is used in this tutorial. You can use steps below to install it:
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
sudo apt install ros-noetic-desktop-full
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo apt install python3-rosdep
sudo rosdep init
rosdep update
```

### Gazebo
The Gazebo version 11 is used in this tutorial. ROS noetic has gazebo11 but if there is problem with it, you can use steps below to install it:
```
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add –
sudo apt-get update
sudo apt-get install gazebo11 libgazebo11-dev
```
If you are using Ubuntu in a VM and gazebo has graphical problems, put the line below inside your bash (bashrc, zshrc, ...):
```
export SVGA_VGPU10=0
```

### Ardupilot
The latest version (4.3.6 at the time of writing) used in this tutorial. You can use steps below to install it:
```
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git submodule update --init –recursive
alias waf="$PWD/modules/waf/waf-light"
waf configure --board=sitl
waf all
./Tools/environment_install/install-prereqs-ubuntu.sh -y
```

### Ardupilot_gazebo
```
git clone https://github.com/SwiftGust/ardupilot_gazebo
cd ardupilot_gazebo
mkdir build
cd build
cmake ..
make -j2
sudo make install
```
After installation of this plugin, you need to add lines below inside your bash (bashrc, zshrc, ...):
```
source /usr/share/gazebo/setup.sh
export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models:${GAZEBO_MODEL_PATH}
export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models_gazebo:${GAZEBO_MODEL_PATH}
export GAZEBO_RESOURCE_PATH=~/ardupilot_gazebo/worlds:${GAZEBO_RESOURCE_PATH}
export GAZEBO_PLUGIN_PATH=~/ardupilot_gazebo/build:${GAZEBO_PLUGIN_PATH}
```

### Docker
The latest version (23.0.6 at the time of writing) used in this tutorial. You can use steps below to install it:
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Run single UAV
- Open a terminal and run the commands below:
```
cd ~/ardupilot/Tools/autotest
./sim_vehicle.py -v ArduCopter -f gazebo-iris --console -I0
```
- Open a new terminal and run:
```
gazebo --verbose ~/ardupilot/ardupilot_gazebo/worlds/iris_ardupilot.world

```
- After seeing "APM: EKF2 IMU0 is using GPS" message in console, you can use the commands below in the first terminal for takeoff test:
```
mode guided
arm throttle
takeoff 5
```
