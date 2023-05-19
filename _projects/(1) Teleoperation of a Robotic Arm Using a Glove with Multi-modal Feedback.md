---
name: Teleoperation of a Robotic Arm Using a Glove with Multi-modal Feedback
tools: [Unity, C#, ROS, robotics, python, OptiTrack, VR, XR]
image: https://i.imgur.com/Xui0Uhj.jpg
description: Master's Degree Thesis Topic in Politecnico di Milano
# external_url: https://www.google.com
---

# Teleoperation of a Robotic Arm Using a Glove with Multi-modal Feedback
The aim in this project was to create a teleoperation environment in Unity to control a Franka Emika Panda robot using WEART' TouchDIVER. This is my Master's Degree thesis project for Mechanical Engineering in Politecnico di Milano.

{% include elements/figure.html image="https://i.imgur.com/Fv5AHpw.jpg" caption="Remote environment setup" %}

It was proven that haptic feedback, in addition to visual feedback, improves the sense of telepresence and the overall performance of the user in a tele-assembly task.

The work was done in collaboration with IDSIA USI-SUPSI under the guidance of Francesco Braghin, Loris Roveda and Asad Ali Shahid.

## Hardware
### Master Side
The controller interface is a wearable device called [TouchDIVER](https://www.weart.it/touchdiver/) developed by WEART. It's capable of force, temperature and texture feedback. Moreover, it can track the positions of the fingers with respect to the palm. The position tracking of the device is achieved through a magnetic adaptor attached to the palm and in this project, the hand position is tracked using [OptiTrack](https://optitrack.com/). Below are some images of TouchDIVER with the custom OptiTrack Controller
{% capture carousel_images %}
https://i.imgur.com/CJNWdsK.jpg
https://i.imgur.com/EeSfJCr.jpg
https://i.imgur.com/JcGE1Wc.jpg?1
{% endcapture %}
{% include elements/carousel.html %}

### Slave Side
The remote operator in this project, a.k.a. the teleoperator, is the [Franka Emika Panda](https://www.franka.de/) which is a 7-DoF research robot with torque sensors at every joint. The robot is equipped with cameras, one at the end effector frame, the other at giving an overall view of the environment to give visual feedback to the user.

{% include elements/figure.html image="https://i.imgur.com/crkEctd.jpg" caption="Remote environment setup" %}

## Software
The main base of operations for this project was Unity as it provides possibilities with its programmable Game Objects and countless ready-to-use assets such as those of OptiTrack and WEART. Moreover, with the development of [Unity Robotics Hub](https://github.com/Unity-Technologies/Unity-Robotics-Hub) in the past couple of years, Unity was deemed an excellent choice to serve as the base.

There are two operating systems in this project, Linux and Windows. This is due to the fact that the WEART TouchDIVER middleware is a Windows-native application and the franka-ros library that controls the Franka Emika Panda doesn't work on Windows.

The bridge that connects ROS and Unit is a set of ope-source libraries called [ROS#](https://github.com/siemens/ros-sharp). Essentially, it handles the replication of the robot through URDF files, the coordinate system conversion between Unity and ROS and passes the messages between two systems. Since it's open source, several additional assets specific to Franka Emika Panda were created.

The system architecture can be found below.

{% include elements/figure.html image="https://i.imgur.com/VA2q33f.png" caption="Remote environment setup" %}

