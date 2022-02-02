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

- [High-level control using ROS and low-level control using STM][Control]

- [PCB design][PCB design]

- [Human state measuring devices (Vicon, EMG)][State measuring]


---
## 3D CAD design & Fabrication

When we develop the robot, first thing we have to design and fabricate is the robot structure. For this reason, as a mechanical engineer, I have designed lots of mechanisms and robot structures using Solidworks. Since my research topic is about soft wearable robot, I also have an experience in fabricating the glove using the sewing machine.

Representatively, I have designed and manufactured a tendon-driven actuator for the wearable robots. With this actuator, it was possible to operate the soft wearable robot reliabliy; the actuator (shown in Fig.1) is called "Slider-Tendon Linear Actuator" and the details are explained [here][Actuator]. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/SliderTendonLinearActuator/Slider_TendonLinearActuator.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Final design of Slider-Tendon linear actuator. The actuator contains the functions of wire derailment prevention, under-actuation, and tendon connection. One loadcell is used to measure the tension of the wire. The blue wire in the left side is a motor tendon while the gray wire in the right side is an end-effector tendon.</figcaption>
</figure>

## CAN Open communication for real-time motor control (multiple motors)

Controlling the motor requires in-depth understanding on the working principle of the motor. Also, the motor requires high electric power, therefore, additional circuit is required to operate the motor. For this reason, an electric circuit called `motor driver' has been dedicated to controlling the motor. In this way, we can control the motor in a real-time without burdening the main controller. 

When controlling the motor using the motor driver, it is important to follow the communication protocol for the motor driver. [CANOpen][cia_link] protocol is one of the well used communication protocol for the motor control. It is because this protocol provides researchers a variety of features to reliably control the motor in real time. *I have experience controlling 4 motors with 1Khz control loop using CANOpen. I am also confident in constructing robot system using a high-level controller (ROS) and low-level controller(STM) with this CANOpen protocol.* Details of how I constructed the high-level and low-level controller is described in below.

## High-level & Low-level control

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>


## PCB design

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
[cia_link]: https://www.can-cia.org/canopen/

We have to design and fabricate the robot structure; we also have to design the electric circuit for the robot system; further, we have to construct the control system that contains high-level controller (that generates the control input related to the overall target goal of the robot) and the low-level controller (that collects sensing data and provides motor control input under fast control loop with punctuality). 
