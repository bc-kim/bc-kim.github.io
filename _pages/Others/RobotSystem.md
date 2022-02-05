---
permalink: /researches/robotsystem
title: "Robot System Design"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---

Designing the robot system requires various skills. We have to design and fabricate the robot structure; we also have to design the electric circuit for the robot system; further, we have to construct the control system that contains high-level controller (that generates the control input related to the overall target goal of the robot) and the low-level controller (that collects sensing data and provides motor control input under fast control loop with punctuality). Since I have constructed couple of robot systems, I am confident in constructing the robot systems using following skills.

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

When designing the robot system, it is required to 

When controlling the robot, we have to construct numerous 


{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>


## PCB design
To control the robot system using the above element techniques (CANOpen, low-level controller, and high level controller), designing the electric circuit is also important. It is because the reliability of the robotic system highly depends on the electric circuit design. Therefore, using the universal board to connect all the IC chips is an inappropriate manufacturing method when we consider the roboustness of the robot system.

Alternatively, we can use a printed circuit board (PCB) for more reliable electric. For this reason, I have designed numerous PCBs using [KiCAD][KiCAD_link]. The Electric system in Fig.1 shows the PCB that I designed to control the motor using CANOpen protocol, low-level controller, and high-level controller. Using this PCB unit, it was possible to controll total four actuators measuring the tension of the tendon; it was used to control the [Exo-Glove Shell][Exo-Glove_shell] that assists the thumb opposition/reposition and flexion/extension of the index/middle finger.

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/GRIPIT/Figure 13.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption><b>Fig. 2 (a)</b> Total system construction to measure force and position of the pen simultaneously, <b>(b)</b> experimental setup to measure the writing force and the position of markers, and <b>(c)</b> marker attachment points to measure the position of pen from a hand frame view.</figcaption>
</figure>


## Human state measuring devices
Since I have developed numerous hand wearable devices and robots, I have used lots of experimental devices that measures human states. Mostly, I have used motion capture system from [Vicon][vicon_link] to validate the performance of the wearable robot. 
In addition, I have an experience measuring the EMG signal using [Delsys][Delsys] EMG sensors to control the hand wearable robot. 

For instance, as the experimental setup (Fig.2) shows, by measuring the force applied at the object (using the 6-axis loadcell called [mini40][mini40]) and the position/orientation of object (using Vicon motion capture cameras), I measured the grasp stability when the wearable robot assists the disabled people; details are explained [here][JNER_pdf]. Here, since syncing the force data with position data is important, additional trigger signal was used as shown in the Fig.2 (a).

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/GRIPIT/Figure 13.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption><b>Fig. 3 (a)</b> Total system construction to measure force and position of the pen simultaneously, <b>(b)</b> experimental setup to measure the writing force and the position of markers, and <b>(c)</b> marker attachment points to measure the position of pen from a hand frame view.</figcaption>
</figure>

I have also conducted experiments (Fig.2) that figure out how the motor torque/position of the developed wearable robot ([ExoIndex][ExoIndex]) affects the joint angle of the user. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Fig4_1.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption><b>Fig. 3</b> Schematic view of the experimental protocol to validate Exo-Index system; (a) shows an external device for synchronizing load cell data measured in the MCU and posture data measured by the Vicon; (b) shows overall control and actuation system for the robot; (c) provides a brief look at how the three tendons of the actuator are connected to the glove.
Figure
</figcaption>
</figure>

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
[vicon_link]: https://www.vicon.com
[KiCAD_link]: https://kicad.org
[Exo-Glove_shell]: /researches/exogloveshell
[ExoIndex]: /researches/exogloveindex
[Delsys]: https://delsys.com
[mini40]: https://www.ati-ia.com/products/ft/ft_models.aspx?id=mini40
[JNER_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Kim%20et%20al.%20-%202017%20-%20Development%20and%20assessment%20of%20a%20hand%20assist%20device%20GRIPIT.pdf
