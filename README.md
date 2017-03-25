# Vehicle Simulator

<img src="/docs/img/polaris_sim.jpg" align="right" height="168" >

This repository constains a vehicle simulator for use in Gazebo. The simulator is based on [drcsim](https://bitbucket.org/osrf/drcsim) developed by OSRF. Drcsim focused on the simulation of Boston Dynamics Atlas robot for the DARPA Robotics Challenge and the vehicle simulation is only a small part of the package for the vehicle task. This project tries to reuse this part of code. The goal is to create a complete simulation package for research on autonomous vehicles.

# 1. Simulation Setup

Assume your catkin worksapce locates at **$HOME/Workspace/catkin_ws**.

```
$ cd ~/Workspace/catkin_ws
$ wstool init src
$ cd ~/Workspace/catkin_ws/src
$ wstool set vehicle_simulator https://github.com/rxdu/vehicle_simulator.git --git
$ wstool update
```

You need to set a few environment variables so that Gazebo could find vehicle models and plugins properly. Put the following two lines in your ~/.bashrc
```
export GAZEBO_PLUGIN_PATH=$HOME/Workspace/catkin_ws/devel/lib/:$GAZEBO_PLUGIN_PATH
export GAZEBO_MODEL_PATH=$HOME/Workspace/catkin_ws/src/vehicle_simulator/vehicle_description/models:$GAZEBO_MODEL_PATH
```
**Note**: You need to adjust the path according the configurations on your computer.


# 2. Basic testing commands

Turn the steering wheel to the left:
```
$ rostopic pub --once /drc_vehicle/hand_wheel/cmd std_msgs/Float64 '{ data : 3.14 }'
```
Turn the steering wheel to the right:
```
$ rostopic pub --once /drc_vehicle/hand_wheel/cmd std_msgs/Float64 '{ data : -3.14 }'
```
Press the gas pedal:
```
$ rostopic pub --once /drc_vehicle/gas_pedal/cmd std_msgs/Float64 '{ data : 1 }'
```
Disengage hand brake :
```
$ rostopic pub --once /drc_vehicle/hand_brake/cmd std_msgs/Float64 '{ data : 0 }'
```
Turn the engine off:
```
$ rostopic pub --once /drc_vehicle/key/cmd std_msgs/Int8 '{ data : 0 }'
```

# 3. Issues and Solutions

* No namespace found

This issue is due to missing "~/.gazebo/models" folder.
```
$ cd ~
$ wget -r -R "index\.html*" http://models.gazebosim.org/
$ cd models.gazebosim.org
$ mv * ~/.gazebo/models
```

# Reference

* [Problem with Indigo and Gazebo 2.2](http://answers.ros.org/question/199401/problem-with-indigo-and-gazebo-22/)
