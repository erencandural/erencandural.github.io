---
name: ME407 Automatic Pet Feeder
tools: [Arduino, Eagle, Fusion 360, robotics, PCB Design, Mechanical Design, Prototyping]
image: https://imgur.com/aqpu8cv.jpg
description: Master's Degree Thesis Topic in Politecnico di Milano
# external_url: https://www.google.com
---

# ME407 Automatic Pet Feeder

The final project for the ME407 Mechanical Engineering Design course, Automatic Pet Feeder aims to dispense a given amount of pet kibbles at a certain time.

In this project, I was responsible from:

* Designing the UI
* Drawing the electrical scheme
* Choosing the correct components such as the power module and sizing the stepper motor
* Designing the controller of the system

The system uses:

* Arduino Nano as the system's main controller
* A real-time clock module to keep track of the time even when the power is out
* A stepper motor driver
* A power module
* An LCD screen and a rotary encoder to act as the system's UI

The components and their protoboard PCB can be seen in the figure below.

{% include elements/figure.html image="https://imgur.com/9r96ymM.jpg" caption="Electronics of the system" %}

In addition, a 2-layer PCB was designed in Eagle, the design of which can be seen below.

{% include elements/figure.html image="https://imgur.com/Gu9FCnV.png" caption="PCB Design" %}

A state machine was created to act as the UI and the Arduino code checks for the time at every loop. The screen along different levels of the UI can be seen below.

{% capture carousel_images %}
https://imgur.com/4OY5Aaj.png
https://imgur.com/LkGxwtI.png
https://imgur.com/4JMomuk.png
https://imgur.com/21t4HIB.png
{% endcapture %}
{% include elements/carousel.html %}

The videos of the Automatic Pet Feeder are attached below.

{% include elements/video.html id="VvByOSjFH2o" %}
{% include elements/video.html id="ihgpAKQRzH0" %}
