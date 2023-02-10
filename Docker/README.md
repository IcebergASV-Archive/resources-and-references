<img src="https://user-images.githubusercontent.com/92492605/201941889-f4a18508-506d-4b2e-bd12-ac9e4553c2b9.png" width="200" height="200" />

# Linux for Tegra (L4T) Docker Container
## Notes
- The following information is for running the L4T docker container on a device that does **not** use **arm64** architecture.
- It is required to use a device that has a **NVIDIA GPU**.
- The information below is bound to a **linux** device. 

## Setup
### Docker and Docker Desktop Install
- [Docker Installation](https://docs.docker.com/engine/install/ubuntu/)
### Install NVIDIA Drivers
View information about your GPU:  
```hwinfo --gfxcard --short```  

Check for compatible drivers:  
```apt search nvidia-driver```  

![image](https://user-images.githubusercontent.com/92492605/211946786-c327014f-bcb5-4bd7-b17d-d42cd33bb9a3.png)

Install desired driver:  
``` sudo apt install nvidia-driver-<driver version>```  

Example:  
```sudo apt install nvidia-driver-525```  

Reboot:  
```sudo reboot```


### Install NVIDIA Container Toolkit
Head to the [NVIDIA Container Toolkit Site](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/overview.html) and follow the installation guide.

### Setup QEMU Emulator
Install the qemu packages:  
```sudo apt-get install qemu binfmt-support qemu-user-static```  

Execute the registering scripts:  
```docker run --rm --privileged multiarch/qemu-user-static --reset -p yes # This step will execute the registering scripts```

## Building the Docker Image and Running the Container
Enter the Docker directory:  
```cd asv-system/Docker```  

Build the image:  
```sudo docker build -t asv-l4t```  

Run the container:  
```xhost +```  
```sudo docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix -v /usr/bin/qemu-arm-static:/usr/bin/qemu-arm-static asv-l4t```  

