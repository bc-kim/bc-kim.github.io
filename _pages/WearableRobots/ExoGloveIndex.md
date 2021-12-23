---
permalink: /researches/exogloveindex
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

For this reason, I have designed <i><b>Exo-Index</b></i> that only assists the index finger using three tendon-driven actuators. Since the thumb is fixed by 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/ExoIndex.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption> <b> Fig. 1  Overall view of Exo-Index </b> <br> (a) shows two flexors (yellow line means All Flexor (A.F.) while the white line shows MCP Flexor (M.F.)) in a hand-open position, (b) shows an extensor named as All Extensor (blue line) in a hand-held position. In addition, the method of attaching vicon markers is shown in (c). Three markers attached on the back side of the hand are considered as the base frame.</figcaption>
</figure>


A way to reduce the number of actuators is to use a mechanism, but this does not secure control for each joint.


The number of actuators greatly influences the complexity of the robot.



{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/GraspExoIndex.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption> <b> Fig. 2  Various postures with the assistance of Exo-Index.  </b> <br> With assistance of the proposed robot, three types of grasp postures are established depending on the object size and shape. (a) and (d) show the posture using the Exo-Index. For more detail, (b) shows how card is grasped using narrow pinch while (e) shows how glue is grasped with caging. In addition, (c) and (f) show wide pinch and the grasped objects are paper cup and bottle.
</figcaption>
</figure>

The number of actuator is important 

When controlling the robot

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/ExoIndex/Result.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>
---

Using the Exo-Index developed here, I also studied to find the joint center of rotation and the state estimation.
Details of state estimation is described in [here][state_page_link].


[Sensors_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Kim%2C%20Ryu%2C%20Cho%20-%202020%20-%20Joint%20Angle%20Estimation%20of%20a%20Tendon-driven%20Soft%20Wearable%20Robot%20through%20a%20Tension%20and%20Stroke%20Measurement.pdf
[Sensors_link]: https://www.mdpi.com/718524 

[uatd_page_link]: /researches/tdm
[state_page_link]: /reseraches/stateestimation