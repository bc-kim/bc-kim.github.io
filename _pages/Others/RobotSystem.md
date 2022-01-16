---
permalink: /researches/robotsystem
title: "Robot System Design"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---

Designing the robot system requires These are 

- [3D CAD design & Fabrication (3D printer, laser printer, CNC, molding, etc.)][3D CAD design]

- CAN Open communication for real-time motor control (multiple motors)

- PCB design

- High-level control using ROS and low-level control using STM

- Human state measuring devices (Vicon, EMG)

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

---
## 3D CAD design

As a mechanical engineer, I have designed lots of mechanisms and robot structures using Solidworks. Mainly, I developed the actuator that pulls the tendon stable in tendon-driven soft robots. The soft robot requires a specified actuator because the tension of tendon should be removed when the robot is not operating; when the tendon tension is zero, the tendon starts to tangle causing numerous problems (details are explained in [actuator session][Actuator]). 

Unlike rigid robots, the situation where tension of all tendons exist is not suitable to 
the tendon-driven soft robots requi 
As explained in [actuator session][Actuator], I aimed to
develop the 
in tendon-driven soft robots, since the tendon derailment

First category of my 3D CAD design is actuator I aimed to develop the 
I have designed a tendon-driven linear actuator (Slider-Tendon Linear Actuator).


When designing the robot system with multiple motors (multi-axis), CAN Open communication provides enables researchers to easily control the motors in real-time. One disadvantage of the CAN Open communication is that it requires the researchers 

One difficult thing in developing the robot system is that 

As the first approach to solve this trade off issue, our lab has used a <i>tendon transmission</i>. It is because this transmission makes the robot end-effector compact, simple, and safe by locating heavy/bulky components -- such as the actuator, controller, and battery -- far from the end-effector using simple Bowden cable as shown in Fig. 1.

- Hand wearable robots and assist devices
  - Exo-Glove Shell
  - Exo-Glove Index
  - GRIPIT
- Tendon Driven Actuators and Tendon Driven Mechanism
  - Tendon Driven Actuator
  - Tendon Driven Mechanism


{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

[Tmech_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Slider-Tendon_Linear_Actuator_With_Under-Actuation_and_Fast-Connection_for_Soft_Wearable_Robots.pdf
[Tmech_link]: https://ieeexplore.ieee.org/document/9314058 
[3D CAD design]: /researches/robotsystem#3d-cad-design
[up]: /researches/robotsystem
[Actuator]: /researches/actuator

