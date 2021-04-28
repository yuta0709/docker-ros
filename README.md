# docker-ros
This is a ROS image that can be used with GUI by remote desktop.

## Build
```console
git clone https://github.com/yuta0709/docker-ros.git
cd docker-ros/noetic
docker build -t [UserName]/[ImageName]:[Tag] .
```
## Usage
```console
cd noetic
docker-compose up
```
Open [localhost:6080](http://localhost:6080) in Browser

## Creating `Dockerfile`
```docker
FROM yuta0709/docker-ros:noetic

RUN apt-get update && \
    apt-get install -y ros-noetic-[package_name]
COPY ./config_files/id_rsa.pub /root/.ssh/authorized_keys
```

```console
docker build -t [UserName]/[ImageName]:[Tag] .
```
## Creating `docker-compose.yml`
```yaml
version: '3'
services: 
    ros:
        image: [UserName]/[ImageName]:[Tag]
        ports: 
            - "6080:80"
            - "2222:22"
        volumes:
            - "./catkin_ws:/root/catkin_ws"
```
### Start container
```console
docker-compose up
```
