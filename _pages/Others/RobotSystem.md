---
permalink: /researches/robotsystem
title: "Robot System Design"
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

When developing 



There exists several approaches to deal with this trade-off issues in the wearable robots.

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
