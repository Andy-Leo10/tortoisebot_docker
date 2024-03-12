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