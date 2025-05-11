
# Isaac ROS Common

Dockerfiles and scripts for development using the Isaac ROS suite.

## How To Use
Copied from  [Isaac ROS Documentation](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_common/index.html)
**Prerequisites:** 
- [Docker](https://docs.docker.com/engine/install/) 
- [Docker nvidia toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) 

**Installation steps & how to use:**
1. Clone this repository 
2. Create a ros2 workspace, then run the following command  
	```
	$PATH_TO_ISAAC_ROS_COMMON/scripts/run_dev.sh -d $PATH_TO_ROS_WORKSPACE -a "{additional_arguments}" 
	```
	example: 
	```
	~/docker/isaac_ros_common/scripts/run_dev.sh -d ~/docker/workspaces/IsaacSim-ros_workspaces/humble_ws -a "-v /dev/shm:/dev/shm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  -v $HOME/.Xauthority:/root/.Xauthority"
	```

## Modification Overview
This repo is modified from the original repo, for an issue workaround on not using "--runtime nvidia" args 
``` 
docker run -it --rm \
    --privileged \
    --network host \
    --ipc=host \
    ${DOCKER_ARGS[@]} \
    -v $ISAAC_ROS_DEV_DIR:/workspaces/isaac_ros-dev \
    -v /etc/localtime:/etc/localtime:ro \
    --name "$CONTAINER_NAME" \
    --runtime nvidia \
    --entrypoint /usr/local/bin/scripts/workspace-entrypoint.sh \
    --workdir /workspaces/isaac_ros-dev \
    $BASE_NAME \
    /bin/bash
``` 
into 
``` 
docker run -it --rm \
    --privileged \
    --network host \
    --ipc=host \
    ${DOCKER_ARGS[@]} \
    -v $ISAAC_ROS_DEV_DIR:/workspaces/isaac_ros-dev \
    -v /etc/localtime:/etc/localtime:ro \
    --name "$CONTAINER_NAME" \
    --gpus all \
    --entrypoint /usr/local/bin/scripts/workspace-entrypoint.sh \
    --workdir /workspaces/isaac_ros-dev \
    $BASE_NAME \
    /bin/bash
``` 
## Overview

The Isaac ROS Common
repository contains a number of scripts and Dockerfiles to help
streamline development and testing with the Isaac ROS suite.

<div align="center"><a class="reference internal image-reference" href="https://media.githubusercontent.com/media/NVIDIA-ISAAC-ROS/.github/main/resources/isaac_ros_docs/repositories_and_packages/isaac_ros_common/isaac_ros_common_tools.png/"><img alt="Isaac ROS DevOps tools" src="https://media.githubusercontent.com/media/NVIDIA-ISAAC-ROS/.github/main/resources/isaac_ros_docs/repositories_and_packages/isaac_ros_common/isaac_ros_common_tools.png/" width="auto"/></a></div>

Docker containers allow you to quickly set up a sensitive set of frameworks
and dependencies to ensure a smooth experience with Isaac ROS packages.
The Dockerfiles for x86_64 are based on the version 23.10 image from [Deep Learning
Frameworks Containers](https://docs.nvidia.com/deeplearning/frameworks/support-matrix/index.html).
On Jetson platforms, JetPack manages all of these dependencies for you.

Use of Docker images enables CI|CD systems to scale with DevOps work and
run automated testing in cloud native platforms on Kubernetes.

For solutions to known issues, see the [Troubleshooting](https://nvidia-isaac-ros.github.io/troubleshooting/index.html) section.

---

## Documentation

Please visit the [Isaac ROS Documentation](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_common/index.html) to learn how to use this repository.

---

## Latest

Update 2024-12-10: Refactored Dockerfiles
