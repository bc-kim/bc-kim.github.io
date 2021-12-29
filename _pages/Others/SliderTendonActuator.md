---
permalink: /researches/actuator
title: "Tendon Driven Actuator"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---
<iframe width="950" height="534" src="https://www.youtube.com/embed/fLd5IRjUdt0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


---
- **Byungchul Kim**, Useok Jeong, Brian Byunghyun Kang, Kyu-Jin Cho, "Slider-Tendon Linear Actuator with Under-actuation and Fast-connection for Soft Wearable Robots ", in **IEEE/ASME Transactions on Mechatronics (I.F 5.673, Top 10%)**. [[pdf]][Tmech_pdf] [[site]][Tmech_link] 

- Funded by National Research Foundation of Korea, Ministry of Science, ICT and Future Planning.

- Exhibited in 2020 CES / 2019 RoboSoft.


---
As introduced in the [research overview][overview], I aimed to develop the wearable robot considering the trade-off issue between the robot functionality and the robot usability. In terms of this trade-off issue, the tendon transmission is approprate transmission for the wearable robot because it provides several strong advantages as below:

1. It enables to locate large, complicated, and heavy components (e.g., controller, battery, and actuator) far from the wearing part by using the Bowden cable as shown in Fig. 1.

2. It easily actuates multiple joints using a single tendon. It is because the tendon is compliant with a small cross-section area and therefore the tendon can passes multiple joints.

3. It is useful to use in soft robot application. This transmission -- which is also compliant -- does not spoil the soft robot`s advantages (which originates from the robot softness). Since the robot softness is also a good factor that 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/Overview/TendonTransmission.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

Although the tendon trasnmission has advantages in solving the trade-off issue of usability and functionlaity, there also exists several side-effects as below:

1. The tendon can get tangled or get stucked in a narrow gap somewhere.

2. The tendon elongates when the tension is applied. The tendon elongation makes difficult to estimate the pulled length. 

The wire may get tangled or get caught in a narrow gap somewhere.

Indeed, the use of tendon transmission provides strong advantages in 

However, when using the tendon transmission, it is important to consider the actuation method

For the trade-off issue, it is 

Among various transmissions used for the under-actuated robots, the under-actuated tendon transmission has shown advantages in making the robot compact and light. It is because the tendon is compliant with a small cross-section area, so it can pass through the joints without restrictions. In some researches, Bowden cable has been used to enhance these advantages by locating heavy and bulky components such as the actuators, controllers, and battery far from the robot.


When developing 

Tendon-driven soft wearable robots should be simple, compact, and safe because they are worn on the human body and interact directly with the human. Here, unlike rigid robots, wire pre-tension should be removed at the end-effector due to the inherent characteristics of the soft robot. In this paper, for a stable and compact actuation system without pre-tension, a linear actuator called a Slider-Tendon Linear Actuator is pro-posed. The proposed actuator is designed to make a linear mo-tion using a tendon, as compared to other linear transmissions, such as ball screw or lead screw transmissions. By using the proposed design method that uses a tendon, the actuator size was reduced to 23.6% of the size of an actuator that uses a ball screw; this is because the tendon can endure high tensile force with a small cross-section area. Furthermore, this paper pro-poses a robot design methodology to locate the robot mecha-nism in the actuator, rather than in the end-effector. The pro-posed actuator is designed to contain a fast-connection and stroke-amplified under-actuation mechanism. In the proposed method, not only is the complexity and size of the worn part reduced, but its performance is also improved. Finally, by ap-plying this actuator to a specific wearable robot, this paper verifies that the proposed actuator sufficiently satisfies the requirements of the wearable robot.



[Tmech_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Slider-Tendon_Linear_Actuator_With_Under-Actuation_and_Fast-Connection_for_Soft_Wearable_Robots.pdf
[Tmech_link]: https://ieeexplore.ieee.org/document/9314058 
[overview]: /researches