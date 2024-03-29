# tortoisebot_docker

- [tortoisebot\_docker](#tortoisebot_docker)
  - [Simulation Environment (not necessary because is docker's homework)](#simulation-environment-not-necessary-because-is-dockers-homework)
    - [ROS1: thing to do](#ros1-thing-to-do)
    - [ROS2: thing to do](#ros2-thing-to-do)
  - [DOCKER TASKs](#docker-tasks)
    - [TASK #1](#task-1)
    - [TASK #2](#task-2)
    - [TASK #3](#task-3)
    - [TASK #4](#task-4)
- [FOR HELP](#for-help)
  - [compose](#compose)
  - [build](#build)
  - [run](#run)
  - [new shell](#new-shell)
  - [clean](#clean)
  - [Previous step for visualization](#previous-step-for-visualization)
  - [Previous step for Docker](#previous-step-for-docker)
  - [Steps for moving files across systems](#steps-for-moving-files-across-systems)

## Simulation Environment (not necessary because is docker's homework)
### ROS1: thing to do
simulation

    source ~/simulation_ws/devel/setup.bash
    roslaunch tortoisebot_gazebo tortoisebot_playground.launch

bridge and video server

    source ~/simulation_ws/devel/setup.bash
    roslaunch course_web_dev_ros web.launch

mapping

    source ~/simulation_ws/devel/setup.bash
    roslaunch tortoisebot_slam mapping.launch

action server

    source ~/simulation_ws/devel/setup.bash
    rosrun course_web_dev_ros tortoisebot_action_server.py

### ROS2: thing to do
simulation

    source ~/ros2_ws/install/setup.bash
    ros2 launch tortoisebot_bringup bringup.launch.py use_sim_time:=True

mapping

    source ~/ros2_ws/install/setup.bash
    ros2 launch tortoisebot_slam cartographer.launch.py use_sim_time:=True

--------------------------------------------------
## DOCKER TASKs
### TASK #1
    cd ~/simulation_ws/src/tortoisebot_ros1_docker
    docker-compose -f docker-compose-sim1.yml up --build
verify with `docker ps` and web app:
- [x] command the robot with web app

### TASK #2
    cd ~/ros2_ws/src/tortoisebot_ros2_docker
    docker-compose -f docker-compose-sim2.yml up --build
verify with `docker ps` and mapping:
- [x] map the environment

### TASK #3
    cd ~/path/inside/RPi
    docker-compose -f docker-compose-real1.yml up 
verify with `docker ps` and mapping:

In the remote PC use:
- Sourced ROS Noetic and DEVEL
- Set ROS_MASTER_URI to the `http://ip-of-the-raspberry:11311`
- Set ROS_HOSTNAME to the ip of the raspberry
- Set ROS_IP to the ip of the raspberry
- [x] map the environment (node is running but the robot doesn't have odometry)

### TASK #4
    cd ~/path/inside/RPi
    docker-compose -f docker-compose-real2.yml up 
verify with `docker ps` and mapping:

In the remote PC use:
- Sourced ROS Galactic and INSTALL
- Set RMW_IMPLEMENTATION to rmw_cyclonedds_cpp 
- Set ROS_DOMAIN_ID to 30 
- Unset env_var: CYCLONEDDS_URI
```
    ros2 launch tortoisebot_description rviz.launch.py 
    ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
- [x] map the environment

--------------------------------------------------

# FOR HELP

## compose

    docker-compose -f docker-compose-sim1.yml up --build
    docker-compose -f docker-compose-real1.yml up --build | tee build.log

execute a bash of the service

    docker exec -it tortoisebot_ros1_docker_NAME_server_1 /bin/bash
## build

    sudo docker build -f tortoisebot-ros1-IMAGE -t tortoisebot-ros1-IMAGE .

## run

    docker run --rm -it -p 11311:11311 -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix tortoisebot-ros1-gazebo:latest bash

## new shell

    sudo docker exec -it NAME /bin/bash

## clean
    docker kill $(docker ps -aq) &> /dev/null;
    docker container prune -f
    docker rmi $(docker images -q) -f

## Previous step for visualization
**check display available**

    ls -la /tmp/.X11-unix/
    echo $DISPLAY

**remove restrictions to X-server**

    xhost +local:root

## Previous step for Docker 
**installation**
    
    sudo apt-get update
    sudo apt-get install docker.io docker-compose -y
    sudo service docker start

**add user to docker-group**
    
    sudo usermod -aG docker $USER
    newgrp docker

## Steps for moving files across systems 
for copying a file from your local machine to a remote machine
    
    scp /path/to/local/file username@remote:/path/to/remote/directory

for copying a file from a remote machine to your local machine

    scp username@remote:/path/to/remote/file /path/to/local/directory