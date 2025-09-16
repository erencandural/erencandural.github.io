---
layout: default
title: ME407 Automatic Pet Feeder
---

[Home](/) | [Blog](/blog) | [Portfolio](/portfolio) | [Resume](/resume)

# ME407 Automatic Pet Feeder

The final project for the ME407 Mechanical Engineering Design course, Automatic Pet Feeder aims to dispense a given amount of pet kibbles at a certain time.

In this project, I was responsible from:

- Designing the UI
- Drawing the electrical scheme
- Choosing the correct components such as the power module and sizing the stepper motor
- Designing the controller of the system

The system uses:

- Arduino Nano as the system's main controller
- A real-time clock module to keep track of the time even when the power is out
- A stepper motor driver
- A power module
- An LCD screen and a rotary encoder to act as the system's UI

The components and their protoboard PCB can be seen in the figure below.

![Electronics of the system](https://imgur.com/9r96ymM.jpg)

In addition, a 2-layer PCB was designed in Eagle, the design of which can be seen below.

![PCB Design](https://imgur.com/Gu9FCnV.png)

A state machine was created to act as the UI and the Arduino code checks for the time at every loop. The screen along different levels of the UI can be seen below.

<div class="carousel" id="myCarousel">
  <img src="https://imgur.com/4OY5Aaj.png" alt="Opening Screen" class="active"/>
  <img src="https://imgur.com/LkGxwtI.png" alt="Meal Plan"/>
  <img src="https://imgur.com/4JMomuk.png" alt="Options"/>
  <img src="https://imgur.com/21t4HIB.png" alt="Example Meal"/>
</div>

<div class="carousel-buttons">
  <button onclick="showSlide(0)">1</button>
  <button onclick="showSlide(1)">2</button>
  <button onclick="showSlide(2)">3</button>
  <button onclick="showSlide(3)">4</button>
</div>

<script>
function showSlide(index) {
  const slides = document.querySelectorAll('#myCarousel img');
  slides.forEach((slide, i) => {
    slide.classList.toggle('active', i === index);
  });
}
</script>

(LCD Screen mock-ups were created with [LCD Screen Screenshot Generator](https://avtanski.net/projects/lcd/))

The videos of the Automatic Pet Feeder are attached below.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/VvByOSjFH2o" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> User interaction.

<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/ihgpAKQRzH0" 
  frameborder="0" 
  allowfullscreen>
</iframe>
> The first prototype dispensing kibbles.
