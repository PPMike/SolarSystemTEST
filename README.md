#Recognition Video UUV SIM Documentation

<p align="center">
  <img src=https://github.com/vanttec/vanttec_uuv/blob/master/docs/LogoNegro_Azul.png width="400" height="240" align="center"/>
</p>

Author:
- José Miguel Flores Gonzalez

## Requerimientos iniciales ###

 - [**Linux Partition**](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjllKHt4PX9AhVMIUQIHRQNCUkQFnoECC0QAQ&url=https%3A%2F%2Fwww.xataka.com%2Fbasics%2Fcomo-instalar-linux-a-windows-10-ordenador&usg=AOvVaw2GEiRuUGLx-Iwj4YZMo119)
 - [**Docker**](https://docs.docker.com/engine/install/ubuntu/)
    
## Docker recomendations ###

 - Download the extentions Dev Containers and Docker in VS Code
    
## Nvidia-docker2 Instalation ###

 - Follow the steps on this website on the Docker section: [nvidia-docker installation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

##  Nvidia Drivers ##
 - Open on Ubuntu Apps Software & Updates
 - Get in Additional Drivers
 - Select this option
<p align="center">
  <img src=https://github.com/vanttec/vanttec_uuv/blob/master/docs/Drivers.png align="center"/>
</p>
    
### If you don't have Nvidia graphics card run instead of the uuv.build ###

 - Writte the next commands:

```
chmod +x runIntelGpu.bash
sudo make uuv.intelcreate
```
 - Comment the run Pangolin into the Dockerfile
    
## Possible driver error ###

<p align="center">
  <img src=https://github.com/vanttec/vanttec_uuv/blob/master/docs/ErrorIMG.jpeg align="center"/>
</p>

 - Deactivate secure boot in the BIOS

## Download the container of UUV ###
 - Create a Docker account [Docker](https://hub.docker.com/signup)
 - Go to this repository ![UV_dev_docker](https://github.com/vanttec/UV_dev_docker)
 - Follow the steps on "Steps in order to start working"

## Compilation tools ###

```
sudo apt-get install python3-catkin-tools
```
- The command to compilate is
```
catkin build
```

## Install repositories ###
**Dont do catkin_make or catkin build before install all the repositories**
```
cd /ws/src
```
- ZED ROS WRAPPER: This repository is to use the ZED Camera [ZED Repository](https://github.com/stereolabs/zed-ros-wrapper)
```
git clone --recursive https://github.com/stereolabs/zed-ros-wrapper.git
```

- darknet_ros (Paquete que nos permite usar YOLO) [Darknet Ros](https://github.com/leggedrobotics/darknet_ros)
```
git clone --recursive https://github.com/vanttec/darknet_ros.git
```

- Follow the steps to install OpenCV on the section opencv_contrib
[OpenCV](https://docs.opencv.org/4.x/d7/d9f/tutorial_linux_install.html)

## Install ZED SDK on your computer ### 
- Get in this link [ZED SDK](https://www.stereolabs.com/developers/release/)
- Download the version to your computer.
```
chmod +x <Your ZED SDK>
./<Your ZED SDK> -- silent
```

## Install ZED SDK on the Docker ###
- Download this file on the Docker [ZED SDK CUDA 12](https://download.stereolabs.com/zedsdk/4.0/cu121/ubuntu18)
```
chmod +x <Your ZED SDK>
./<Your ZED SDK> -- silent
```
## Librerias faltantes o que requieren versiones específicas ###
```
sudo pip3 install --upgrade pip

sudo apt-get install python3-rospkg

sudo apt install python3-pandas

sudo apt install python-pip

sudo apt-get install python3-sklearn

pip3 install numpy==1.18

pip3 install scipy==1.1.0

pip3 install scikit-learn==0.21.3

pip3 install joblib==1.0.0

pip2 install opencv-contrib-python
pip2 install opencv-python

pip install imutils
```
## Archivos Faltantes ###
Estos archivos se encuentran en el drive [SUB File](https://drive.google.com/drive/folders/1n8lwIeKVj_f0X7uYxjpccCf6gE2nJSBr?usp=sharing)

- Colocar el camera2.yaml en octomap_mapping/octomap_server/cfg/common
- Colocar el RoboSub2021.launch en darknet_ros/launch 
- Poner el robosub_2021_tiny3.cfg en darknet_ros/yolo_network_config/cfg
- Poner robosub2021_96_98.weights en darknet_ros/yolo_network_config/weights

- Compile all
```
catkin build j4
```

## How to use it ###

- To use the camera see the documentation of the zed-ros-wrapper repository [ZED Repository](https://github.com/stereolabs/zed-ros-wrapper)
- Use rostopic to see the topic of the camera and change it on "darknet_ros/config/ros.yaml"
- To launch the YOLO node:
```
roslaunch darknet_ros darknet_ros.launch
```
