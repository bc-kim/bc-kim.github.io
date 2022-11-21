---
permalink: /research/exogloveindex
title: "Exo-Index"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---
- **Byungchul Kim**, Jiwon Ryu, Kyu-Jin Cho, "Joint Angle Estimation of a Tendon-Driven Soft Wearable Robot through a Tension and Stroke Measurement," in **Sensors (I.F 3.275, Top 25%)**, 20.10 (2020): 2852. [[pdf]][Sensors_pdf] [[site]][Sensors_link]


---

The number of actuators highly affects the robot complexity. Although the under-actuation mechanism (detail explanation is described [here][uatd_page_link]) can reduce the actuator number, we can not guarantee the robot controllability when this mechanism is used. 

As an alternative method to reduce the number of actuators, I have designed a robot that assists only one finger with limited number of actuators. I have designed <i><b>Exo-Index</b></i> that only assists the index finger using three tendons as shown in Fig. 1; in this robot, two flexors (1. tendon that flexes all joints of the index finger; and 2. tendon that only flexes MCP joint) and one extensor that extends all joints of the index finger. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/ExoIndex.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption> <b> Fig. 1  Overall view of Exo-Index </b> <br> (a) shows two flexors (yellow line means All Flexor (A.F.) while the white line shows MCP Flexor (M.F.)) in a hand-open position, (b) shows an extensor named as All Extensor (blue line) in a hand-held position. In addition, the method of attaching vicon markers is shown in (c). Three markers attached on the back side of the hand are considered as the base frame.</figcaption>
</figure>

In this robot, since the thumb is fixed by the passive structure, it was possible to grasp various objects even the robot assists a single finger as shown in Fig. 2. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/GraspExoIndex.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption> <b> Fig. 2  Various postures with the assistance of Exo-Index.  </b> <br> With assistance of the proposed robot, three types of grasp postures are established depending on the object size and shape. (a) and (d) show the posture using the Exo-Index. For more detail, (b) shows how card is grasped using narrow pinch while (e) shows how glue is grasped with caging. In addition, (c) and (f) show wide pinch and the grasped objects are paper cup and bottle.
</figcaption>
</figure>

Although the robot was desgined with three tendons(actuators) to make various postures of the index finger, we need a robot system modeling to control the motion. However, the robot system modelling was remained difficult issue due to the numerous uncertainties in the robot system - e.g., it is difficult to figure out the joint stiffness because it changes as the human posture changes; it is also hard to know the exact tendon configuration which affects the tendon jacobian; and it is also difficult to know the center of rotation of the human joint. For instance, if we estimate the angle of the finger joints using tendon kinematics, the estiamted result can be differ a lot with its real value as shown in Fig. 3.

For this reason, I also studied to find the center of rotation and the angle of the human joints using the Gaussian Process Regression (GPR). Details are described in [here][state_page_link].

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Result.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 3 Results of estimation that shows relationship between joint angle and wire tension. (a) shows comparison of the ground truth angle with the estimated angle from data-driven method and the estimated angle from model-driven method; (b) and (c) each show response plot of the data-driven method and model-driven method respectively.</figcaption>
</figure>
---

[Sensors_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Kim%2C%20Ryu%2C%20Cho%20-%202020%20-%20Joint%20Angle%20Estimation%20of%20a%20Tendon-driven%20Soft%20Wearable%20Robot%20through%20a%20Tension%20and%20Stroke%20Measurement.pdf
[Sensors_link]: https://www.mdpi.com/718524 

[uatd_page_link]: /researches/tdm
[state_page_link]: /reseraches/stateestimation