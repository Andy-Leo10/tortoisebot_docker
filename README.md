# tortoisebot_docker

- [tortoisebot\_docker](#tortoisebot_docker)
  - [Simulation Environment](#simulation-environment)
    - [ROS1](#ros1)
    - [ROS2](#ros2)
  - [TASKs](#tasks)
    - [TASK #1](#task-1)
    - [TASK #2](#task-2)
    - [TASK #3](#task-3)
    - [TASK #4](#task-4)
- [FOR HELP](#for-help)
  - [compose](#compose)
  - [build](#build)
  - [run](#run)
  - [new shell](#new-shell)
  - [Previous step for visualization](#previous-step-for-visualization)
  - [Previous step for Docker](#previous-step-for-docker)

## Simulation Environment
### ROS1
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

### ROS2
simulation

    source ~/ros2_ws/install/setup.bash
    ros2 launch tortoisebot_bringup bringup.launch.py use_sim_time:=True

mapping

    source ~/ros2_ws/install/setup.bash
    ros2 launch tortoisebot_slam cartographer.launch.py use_sim_time:=True

--------------------------------------------------
## TASKs
### TASK #1
    cd ~/simulation_ws/src/tortoisebot_ros1_docker
    docker-compose up
verify with `docker ps` and web app:
- [ ] command the robot with web app

### TASK #2
    cd ~/ros2_ws/src/tortoisebot_ros2_docker
    docker-compose up
verify with `docker ps` and mapping:
- [ ] map the environment

### TASK #3
    docker-compose up
    docker ps
verify with `docker ps` and mapping:
- [ ] map the environment

### TASK #4
    docker-compose up
    docker ps
verify with `docker ps` and mapping:
- [ ] map the environment

--------------------------------------------------

# FOR HELP

## compose

    docker-compose -f docker-compose-sim1.yml up --build

## build

    sudo docker build -f tortoisebot-ros1-IMAGE -t tortoisebot-ros1-IMAGE .

## run

    docker run --rm -it -p 11311:11311 -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix tortoisebot-ros1-gazebo:latest bash

## new shell

    sudo docker exec -it NAME /bin/bash

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
