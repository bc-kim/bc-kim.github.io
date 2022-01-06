---
permalink: /reseraches/stateestimation
title: "Human State Estimation"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---
- **Byungchul Kim**, Jiwon Ryu, Kyu-Jin Cho, "Joint Angle Estimation of a Tendon-Driven Soft Wearable Robot through a Tension and Stroke Measurement," in **Sensors (I.F 3.275, Top 25%)**, 20.10 (2020): 2852. [[pdf]][Sensors_pdf] [[site]][Sensors_link]


---

**Necessity and difficulties of human state estimation**
---

When controlling a soft wearable robot, it is necessary to estimate not only the robot state, but also the human state. However, estimating the human/robot state is quite difficult in the soft hand wearable robot due to several reasons as below:

1. It is difficult to attach sufficient number of sensors at the hand due to the size issue. As I explained in the [Research Overview][overview] page, we wanted to develop the wearble robot that considers both usability and functionality. Therefore we didn`t wanted to use sensors at the wearing part.

2. Some of human state variables are not constant. For instance, the stiffness of human joint is a function of wrist position. Therefore it is hard to figure out using the model-based method.

3. When the robot is under-actuated robot (since we designed the robot using the under-actuation mechanism to consider both usability and functionality), the joint angle of the finger is not determined even the motor stroke is determined; there exist null space in the joint angle space. 

4. The elongation of the soft material makes difficult to estimate the kinematic relationship between the transmission and the human joint. For instance, if the robot is actuated using tendon transmission, the distance between the tendon and the joint is important in calculating the moment arm of the tendon. However, when the glove part elongate, it is difficult to estimate the moment arm of the tendon.

In this research, to consider the above uncertainties, I used a data-driven method that identifies both kinematic and stiffness parameters using tension and wire stroke of the actuators. Through [kinematic identification][kmID], a method is proposed to find the exact joint position as a function of the joint angle. Through [stiffness identification][knID], the relationship between the actuation force and the joint angle is obtained using Gaussian Process Regression (GPR).

This identification methods have been validated using a specific robot named [Exo-Index][ExoIndex]. The result shown in Fig.1 shows that the estimation result using GPR shows better accuracy compared to the result drived from the model-based method. Details of human state estimation is described in the following sections.

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Result.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1. Results of estimation that shows relationship between joint angle and wire tension. (a) shows comparison of the ground truth angle with the estimated angle from data-driven method and the estimated angle from model-driven method; (b) and (c) each show response plot of the data-driven method and model-driven method respectively.</figcaption>
</figure>


**Human State Estimation**
--
In this research, I aimed to find joint angle and 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Fig2_3_All5.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1. Experimental results about the position of the finger joints found using a vicon motion capture system. (a) The marker position used to measure the joint position. With this marker setup, the position of the MCP, PIP, and DIP joint are measured, as shown in (b), (c), and (d). Since the joints move as the joint angle changes, the positions of the joints are expressed in terms of the angle of the joints.</figcaption>
</figure>


{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Fig_knid.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1. Experimental results of the stiffness parameter estimation that shows a relationship between the joint angle and the wire tension. (a,c,e) are plots of the ground truth angles measured by Vicon cameras and estimated angles using the wire tension and wire stroke. (b,d,f) are comparisons between the estimation and the ground truth. The RMS error indicates the disparity from the y = x relationship.</figcaption>
</figure>

This is because the angle of the finger joint is not determined even if the position of the motor is determined.

robot can be 


it is required to estimate the human 

it is important to estimate the state of the human (joint )


The complexity of the robot system is highly affected by the number of actuators. For this reason, several researchers have tried to use less number of actuators than the robot actual degree of freedoms (DoF); these robots and mechanism were named as <i> under-actuated robots </i> and <i>under-actuation mechanism</i>, respectively.

Among various transmissions used in the under-actuated robots, the tendon transmission 

Among various transmissions used for the under-actuated robots \cite{Birglen2006}, the under-actuated tendon transmission has shown advantages in making the robot compact and light. It is because the tendon is compliant with a small cross-section area, so it can pass through the joints without restrictions. In some researches, Bowden cable has been used to enhance these advantages by locating heavy and bulky components such as the actuators, controllers, and battery far from the robot 

The number of actuator is 

Under-actuated tendon-driven (UATD) robots have advantages in terms of 1) lightweight; 2) compact size; and 3) ability to make adaptive motions against the external environment. However, in UATD robots, friction at the tendons accumulates as they pass through many joints, causing hysteresis and detrimental to tension distribution, reliability and efficiency. For this issue, this paper presents a method to find possible under-actuated tendon routings for the robot that has $n$ fingers; it derives $2^{n+1}-1$ routings for the robot that has $n$ parallel links. This paper also shows validation of the routings with four performance factors (i.e., adaptability, torsional balance, reliability, and efficiency) that are determined by friction. By applying the proposed framework to a specific robot application, a soft hand wearable robot that assists the SCI people, we proved that the proposed framework works effectively improving the performance of the tendon-driven robots as follow: 1) it improves under-actuation performance (the difference in fingertip force reduced from 3.1N  to  1.3N); 2) it reduces hysteresis (the hysteresis in joint angle domain reduced from  81.8\%  to  46.9\%) at the flexor; 3) it enables to use passive tendon; and 4) it enables to attach tension sensor at the end-effector in a compact size. These improvements verify the efficacy of the proposed framework for improving the robot performance. 

[Sensors_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Kim%2C%20Ryu%2C%20Cho%20-%202020%20-%20Joint%20Angle%20Estimation%20of%20a%20Tendon-driven%20Soft%20Wearable%20Robot%20through%20a%20Tension%20and%20Stroke%20Measurement.pdf
[Sensors_link]: https://www.mdpi.com/718524 
[overview]: /researches
[knID]: /reseraches/stateestimation#estimation-of-the-joint-angle-using-the-motor-data
[kmID]: /reseraches/stateestimation#estimation-of-the-joint-position
[ExoIndex]: /researches/exogloveindex