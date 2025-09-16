---
layout: default
title: Teleoperation of a Robotic Arm Using a Glove with Multi-modal Feedback
---

[Home](/) | [Blog](/blog) | [Projects](/projects) | [Resume](/resume)

# Teleoperation of a Robotic Arm Using a Glove with Multi-modal Feedback

The aim in this project was to create a teleoperation environment in Unity to control a Franka Emika Panda robot using WEART's TouchDIVER. This is my Master's Degree thesis project for Mechanical Engineering in Politecnico di Milano.

![General concept](https://i.imgur.com/Fv5AHpw.jpg)

It was proven that haptic feedback, in addition to visual feedback, improves the sense of telepresence and the overall performance of the user in a tele-assembly task.

The work was done in collaboration with IDSIA USI-SUPSI under the guidance of Francesco Braghin, Loris Roveda and Asad Ali Shahid.

There were two steps to this project; establishing the virtual space and then applying it to the actual robot.
The simulation environment was used to verify that the robot controllers are communicating with the Unity and environment and are responsive to the WEART TouchDIVER. Below, a simple pick and place task in the Unity environment can be seen.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/oPmNJ25dEYc" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> The simulated environment

Once the real robot was involved, the Unity environment acted as a control interface for the user, displaying two camera feeds and the simulated robot state.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/hsfufMpFk60" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> The UI visible to the user during opertaion.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/GUH9oQvIqe0" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> What a successful attempt looks like, along with the graph of the force applied to the end effector.

## Hardware

### Master Side

The controller interface is a wearable device called [TouchDIVER](https://www.weart.it) developed by WEART. It's capable of force, temperature and texture feedback. Moreover, it can track the positions of the fingers with respect to the palm. The position tracking of the device is achieved through a magnetic adaptor attached to the palm and in this project, the hand position is tracked using [OptiTrack](https://optitrack.com/). Below are some images of TouchDIVER with the custom OptiTrack Controller

![TouchDIVER 1](https://i.imgur.com/CJNWdsK.jpg)
![TouchDIVER 2](https://i.imgur.com/EeSfJCr.jpg)
![TouchDIVER 3](https://i.imgur.com/JcGE1Wc.jpg)

### Slave Side

The remote operator in this project, a.k.a. the teleoperator, is the [Franka Emika Panda](https://www.franka.de/) which is a 7-DoF research robot with torque sensors at every joint. The robot is equipped with cameras, one at the end effector frame, the other at giving an overall view of the environment to give visual feedback to the user.

![Robot setup](https://i.imgur.com/crkEctd.jpg "Robot setup")

## Software

The main base of operations for this project was Unity as it provides possibilities with its programmable Game Objects and countless ready-to-use assets such as those of OptiTrack and WEART. Moreover, with the development of [Unity Robotics Hub](https://github.com/Unity-Technologies/Unity-Robotics-Hub) in the past couple of years, Unity was deemed an excellent choice to serve as the base.

There are two operating systems in this project, Linux and Windows. This is due to the fact that the WEART TouchDIVER middleware is a Windows-native application and the franka-ros library that controls the Franka Emika Panda doesn't work on Windows.

The bridge that connects ROS and Unit is a set of open-source libraries called [ROS#](https://github.com/siemens/ros-sharp). Essentially, it handles the replication of the robot through URDF files, the coordinate system conversion between Unity and ROS and passes the messages between two systems. Since it's open source, several additional assets specific to Franka Emika Panda were created.

The system architecture can be found below.

![Conceptual system architecture](https://i.imgur.com/VA2q33f.png)

## Methodology

There are essentially three controllers developed in the system:

- Robot Controller (ROS controller)
- Gripper Controller (python)
- Custom Feedback (C#)

The robot controller in the system is the Cartesian Impedance controller that comes with the franka-ros library. It comes with a safety feature that brakes the robot whenever the magnitude of an external wrench acting on the end effector frame exceeds a certain value, 20N in this case.

The franka-ros library also comes with ROS actions that control the gripper. However, these actions are meant to be used sequentially. In order to transition between these commands and create a heightened sense of telepresence, a state machine was written for the gripper controller. The schematic of this state machine can be found below.

![Grip state machine](https://i.imgur.com/qnBrhsM.png)

Finally, a custom feedback scenario was developed using the WEART Unity assets. In this scenario force feedback corresponds to the external wrench acting on the end effector, the maximum amount of force feedback corresponds to the Cartesian reflex, i.e. the safety brake of 20N, so that the users can gage how they are interacting with the environment.

![safety](https://i.imgur.com/aAZUaEd.png)

The haptic feedback is used to signal to the user whether the grasp was successful or not. The grasp action in the gripper controller feedbacks the result via a ROS topic. If the grasp is a success, the user gets a "Single Click" sensation and a "Double Click" sensation if it's a failure. The haptic feedback scenario was achieved only in the simulated environment, however.

![haptic feedback success](https://i.imgur.com/yOP0TlJ.png "Haptic Feedback scenario 1")
![haptic feedback failure](https://i.imgur.com/Wc6z8k7.png "Haptic Feedback scenario 2")
