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

- Funded by National Research Foundation of Korea, Ministry of Trade, Industry and Energy of Korea.

- Exhibited in 2020 CES / 2019 RoboSoft.


---
As introduced in the [research overview][overview], I aimed to develop the wearable robot considering the trade-off between the robot functionality and the robot usability. In terms of this trade-off issue, the tendon transmission is approprate transmission for the wearable robot because it provides several strong advantages as below:

1. It enables to locate large, complicated, and heavy components (e.g., controller, battery, and actuator) far from the wearing part by using the Bowden cable as shown in Fig. 1.

2. It easily actuates multiple joints using a single tendon. It is because the tendon is compliant with a small cross-section area and therefore the tendon can passes multiple joints. Therefore the robot can be simplified by actuating multiple joints with less actuators.

3. It is useful to use in soft robot application. This transmission --which is also compliant-- does not spoil the soft robot`s advantages (which originates from the robot softness as described in [here][hybrid_link]) in the wearable robot studies. For this reason, it can be argued that the tendon transmission has strengths in the wearable robot studies.

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/SliderTendonLinearActuator/Fig1.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

Although the tendon trasnmission has advantages in solving the trade-off between usability and functionlaity, there also exists several side-effects as below:

1. Friction at the tendon is not negligible. In addition, this friction force accumulates as the tendon passes multiple joints; therefore it is difficult to estimate the friction force. Also, the friction force makes difficult to control the robot.

2. The tendon can get tangled or get stucked in a narrow gap somewhere.

3. The tendon elongates when the tension is applied. The tendon elongation makes difficult to estimate the pulled length and difficult to control the robot.

In general, the side-effect 1 has been solved by using the bearings to reduce the friction. The side-effects 2 and 3 can be easily solved by tensioning the tendon; rigid robots have solved these two problems by applying the pretension at the tendon. However, in the soft robots, it is difficult to maintain the tension all the time. It is because the tension of the tendon deforms the robot body when the robot consists of soft material.

For this reason, I have developed an actuator that can pull the tendon without inducing the above side-effects; the actuator is called 'slider-tendon linear actuator'. Also, in this actuator design, I aimed to locate several mechanisms that improves the functionality and usability of the soft wearable robot; the actuator contains 1) wire derailment prevention mechanism, 2)underactuation mechanism, 3) fast-connection Mechanism, and 4) stroke amplification mechanism. Details of how the actuator was designed and the mechanisms work are explained in the [paper][Tmech_pdf]. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/SliderTendonLinearActuator/Slider_TendonLinearActuator.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 2 Final design of Slider-Tendon linear actuator. The actuator contains the functions of wire derailment prevention, under-actuation, and tendon connection. One loadcell is used to measure the tension of the wire. The blue wire in the left side is a motor tendon while the gray wire in the right side is an end-effector tendon.</figcaption>
</figure>

[Tmech_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Slider-Tendon_Linear_Actuator_With_Under-Actuation_and_Fast-Connection_for_Soft_Wearable_Robots.pdf
[Tmech_link]: https://ieeexplore.ieee.org/document/9314058 
[overview]: /researches
[hybrid_link]: /researches/hbwr