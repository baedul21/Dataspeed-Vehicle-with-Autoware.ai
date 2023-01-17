# Dataspeed-Vehicle-with-Autoware.ai
# 1. How to install Autoware.ai ROS1
This instruction shows how to install Autoware.ai (ROS1) in your Ubuntu machine.

## 1.1. Prerequisite
### Install Ubuntu
Download desktop image - https://releases.ubuntu.com/18.04/ and make USB boot - https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#1-overview

Install Ubuntu 18.04 - https://ubuntu.com/tutorials/install-ubuntu-desktop-1804#1-overview 

Install ROS1 melodic - http://wiki.ros.org/melodic/Installation/Ubuntu

## 1.2. Install Docker
There are two options you can install docker but highly recommend use Option 2 - Docker's installation page.

Option 1 - autoware.ai docker installation - https://github.com/Autoware-AI/autoware.ai/wiki/docker-installation

Option 2 - Docker's installation page - https://docs.docker.com/engine/install/ubuntu/

### Setting up System dependencies for Ubuntu 18.04 / Melodic

$ sudo apt update

$ sudo apt install -y python-catkin-pkg python-rosdep ros-$ROS_DISTRO-catkin

$ sudo apt install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool

$ pip3 install -U setuptools

### Nvidia CUDA Toolkit Installation
Reference website: https://docs.nvidia.com/cuda/archive/10.0/cuda-installation-guide-linux/index.html#ubuntu-installation

Before you install CUDA toolkit, you have to check the version of the kernel in your system:

$ uname -r

and the kernel headers and development packages for the currently running kernel can be installed with:

$ sudo apt-get install linux-headers-$(uname -r)

##### Install the most recent CUDA toolkit
Before install the most recent CUDA toolkit, you can select options based on your system - https://developer.nvidia.com/cuda-downloads.
![image](https://user-images.githubusercontent.com/24539075/212996825-6ef16a32-ec9b-4401-bd13-3f60aac39ea8.png)

For example, select 'Linux' as an operating system, 'x86_64' as an architecture, 'Unbuntu' as a distribution, '18.04' as a version, and 'deb (local)' as an installation type. And you will get installer as below:

$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin

$ sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600

$ wget https://developer.download.nvidia.com/compute/cuda/11.6.1/local_installers/cuda-repo-ubuntu1804-11-6-local_11.6.1-510.47.03-1_amd64.deb

$ sudo dpkg -i cuda-repo-ubuntu1804-11-6-local_11.6.1-510.47.03-1_amd64.deb

$ sudo apt-key add /var/cuda-repo-ubuntu1804-11-6-local/7fa2af80.pub

$ sudo apt-get update

$ sudo apt-get -y install cuda

After the installation, reboot your system.

### Nvidia Docker Installation
Reference website: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker

#### Setting up Docker
Docker-CE on Ubuntu can be setup using Docker’s official convenience script:

$ curl https://get.docker.com | sh \

&& sudo systemctl --now enable docker

#### Setting up NVIDIA Container Toolkit
Setup the 'stable' repository and the GPG key:

$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \

&& curl -s -Lhttps://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \

&& curl -s -Lhttps://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

Install the 'nvidia-docker2' package (and dependencies) after updating the package listing:

$ sudo apt-get update

$ sudo apt-get install -y nvidia-docker2

Restart the Docker daemon to complete the installation after setting the default runtime:

$ sudo systemctl restart docker

Working setup can be tested by running a base CUDA container:

$ nvidia-smi

For example,
![image](https://user-images.githubusercontent.com/24539075/212996492-e844701b-d561-4d7b-90b1-01f750be06c5.png)


## 1.3. Run an Autoware Docker Container
Reference website: https://github.com/Autoware-AI/autoware.ai/wiki/Generic-x86-Docker

In this case, we are using 'Case 1: Using Autoware Docker Containers with Pre-Built Source Code Included.'

The pre-built Autoware containers include all of the necessary prerequisites for a given release of Autoware.ai and also contain the Autoware.ai source code for that release, pre-compiled. To run one of these containers:

Clone the docker repository and move into the generic docker folder:

$ git clone https://github.com/Autoware-AI/docker.git

$ cd docker/generic

Use the run.sh script to start and enter the Docker container:
$ ./run.sh

### Errors
After you run a 'run.sh' file, you might face two types of errors. First is 'UID' , user ID error. You can fix this error by editing the 'run.sh' file. Open and edit 'USER_ID' to '1000'.
![image](https://user-images.githubusercontent.com/24539075/212997034-4ad36ae1-5cd4-4146-ae78-98f8089c1949.png)

The second type of error is docker error as below:
![image](https://user-images.githubusercontent.com/24539075/212997071-9aea529a-2e2f-4de3-abef-111b53a42c38.png)

You can fix this error by typing as below:

$ sudo service docker stop

$ sudo rm -rf /var/lib/docker

$ sudo service docker start

or type,

$sudo chmod 666 /var/run/docker.sock

## 1.4. Start Autoware.ai
Open a 'run.sh' file again.

$ cd docker/generic

$ ./run.sh

Once you open 'Autoware.ai' , start the Autoware.ai

$ cd Autoware

$ source install/setup.bash

$ roslaunch runtime_manager runtime_manager.launch

Starting Autoware.ai video - https://youtu.be/Kx010F8bI_Y

## 1.5. Now, you are Autoware.ai user!
Next, we will work on how to run the demo.
