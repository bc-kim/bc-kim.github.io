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
