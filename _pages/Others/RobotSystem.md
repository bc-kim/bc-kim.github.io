---
permalink: /researches/robotsystem
title: "Robot System Design"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---

Designing the robot system requires various skills. I am confident in constructing the robot systems using following skills.

- [3D CAD design & Fabrication (3D printer, laser printer, CNC, molding, etc.)][3D CAD design]

- [CAN Open communication for real-time motor control (multiple motors)][CANOpen]

- [PCB design][PCB design]

- [High-level control using ROS and low-level control using STM][Control]

- [Human state measuring devices (Vicon, EMG)][State measuring]


---
## 3D CAD design & Fabrication

When we develop the robot, first thing we have to design and fabricate is the robot structure. For this reason, as a mechanical engineer, I have designed lots of mechanisms and robot structures using Solidworks. Since my research topic is about soft wearable robot, I also have an experience in fabricating the glove using the sewing machine.

Mainly, I have designed and fabricated a tendon-driven actuator for the soft robots called Slider-Tendon Linear Actuator. With this actuator, it was possible to operate the soft wearable robot reliably; details are explained [here]. 

Also, this actuator is published in 

Slider_TendonLinearActuator

The main objective of this actuator is to solve the tangling issue occured in the soft robots. 

In the soft robot, unlike rigid robots, the tendon can be tangled. 


(details are explained in [actuator session][Actuator]). 



I developed the actuator that pulls the tendon stable in tendon-driven soft robots. 


The soft robot requires a specified actuator because the tension of tendon should be removed when the robot is not operating; when the tendon tension is zero, the tendon starts to tangle causing numerous problems (details are explained in [actuator session][Actuator]). 

Unlike rigid robots, the situation where tension of all tendons exist is not suitable to 
the tendon-driven soft robots requi 
As explained in [actuator session][Actuator], I aimed to
develop the 
in tendon-driven soft robots, since the tendon derailment

First category of my 3D CAD design is actuator I aimed to develop the 
I have designed a tendon-driven linear actuator (Slider-Tendon Linear Actuator).


When designing the robot system with multiple motors (multi-axis), CAN Open communication provides enables researchers to easily control the motors in real-time. One disadvantage of the CAN Open communication is that it requires the researchers 

One difficult thing in developing the robot system is that 

## CAN Open communication for real-time motor control (multiple motors)

Controlling the motor requires in-depth understanding of the working principle of the motor. Since the motor requires high electric power, most of researchers use motor driver to operate the motor. However, when we use multiple motors, 

We have to design complicated circuit that uses high power and 

 One way to solve this issue is to use 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

## PCB design

## High-level & Low-level control

## Human state measuring devices

[Tmech_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Slider-Tendon_Linear_Actuator_With_Under-Actuation_and_Fast-Connection_for_Soft_Wearable_Robots.pdf
[Tmech_link]: https://ieeexplore.ieee.org/document/9314058 
[3D CAD design]: /researches/robotsystem#3d-cad-design--fabrication
[up]: /researches/robotsystem
[Actuator]: /researches/actuator
[CANOpen]: /researches/robotsystem#can-open-communication-for-real-time-motor-control-multiple-motors
[PCB design]: /researches/robotsystem#pcb-design
[Control]: /researches/robotsystem#high-level--low-level-control
[State measuring]: /researches/robotsystem#human-state-measuring-devices


We have to design and fabricate the robot structure; we also have to design the electric circuit for the robot system; further, we have to construct the control system that contains high-level controller (that generates the control input related to the overall target goal of the robot) and the low-level controller (that collects sensing data and provides motor control input under fast control loop with punctuality). 
