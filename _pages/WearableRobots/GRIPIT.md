---
permalink: /researches/gripit
title: "GRIPIT"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "docs"

---

<iframe width="950" height="534" src="https://www.youtube.com/embed/3KyD_rQ8nPc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---
- **Byungchul Kim**, Hyunki In, Daeyoung Lee, Kyu-Jin Cho, "Development and assessment of a hand assist device: GRIPIT", in **Journal of NeuroEngineering and Rehabilitation (I.F 3.519, Top 10%)**, 14.1 (2017): 15. [[pdf]][JNER_pdf] [[site]][JNER_link]

- Funded by National Research Foundation of Korea, Ministry of Science, ICT and Future Planning.

- Received Minister`s Prize, 16th Industrial Technology Award of the Month.

- Received $2,000 investment through social funding (KaKao Story Funding).

- This research topic is the thesis topic of my master degree.


---

## Reason why hand wearable robot is difficult to use in real-life

Although the hand wearable robots have been developed by numerous researchers, these robots are not yet in practical use due to several reasons described below: 

1. The human hand plays a variety of roles in our daily life. Therefore, without a perfect understanding of human intention, the use of hand wearable robot will remain incomplete. 

2. The human hand are small. Therefore, the hand wearable robots must also be desinged in a compact size to assist the tasks performend by hand. The miniaturization of the robot increases its cost.

3. The human hand carries out its role with numerous sensing cells and muscles. For this reason, the hand wearable robot requires lots of sensors and actuators. Lots of sensors and actuators increase the robot cost as well as difficulties in robot control.

4. Since the human properties are very different for each individual, the robot should be customized by the user. However, since the robot size should be also small, including the design for customization is difficult issue.

Since I wanted to develop robots that can be used in real life, not in a laboratory, as introduced in my [introduction page][home_link], I developed a hand assist device, named as GRIPIT, that works similar to the tendon-driven wearable robot.
## GRIPIT for the SCI people

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/GRIPIT/Figure 2.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 GRIPIT overview</figcaption>
</figure>


In order to solve the above problems that makes the robot difficult to use in the real-life, I designed a hand assist device GRIPIT as shown in Fig. 1. The design approaches of the GRIPIT are as below (each design approach has a one-to-one correspondence to the four reasons explained in the [*'Reason why hand wearable orbot is difficult to use in real-life'*][reason_link] section):

#### 1. Focusing on a single posture
Even if the researcher develop a hand wearable device that can make various postures, it is difficult to understand human intensiond well. For this reason, I developed the device that assists a single posture; in this way it was possible to maximize the robot simplicity. In GRIPIT design, we focused on a tripod grasp because it is one of well used posture in daily living. I also hoped that GRIPIT could help SCI people hold a pen (which is also conducted by the tripod grasp) so they could continue their studies. Details of experimental result are described in the [paper][JNER_pdf].

#### 2. Manual operation for simple use
In order to make the device compact, I aimed to develop the device that can be operated manually. It is because the actuator is large and requires the controller and battery that is also large and heavy. Also, to make the device functional even with manual operation, I designed the device with under-actuation mechanism. Using this mechanism, it was possible to make the device actuate multiple joints (e.g., nine joints are required to make the tripod grasp) with a single tendon. Details of under-actuated tendon routing is discribed [below][uatd_internal_link]. Also, to make sufficient grasping force even with a small tension, the under-actuated tendon routing with high force transmission ratio was selected; it is also explained below.

#### 3. Under-actuated tendon routing
The GRIPIT was developed to be operated by a single tendon for the easy use; since the device is operated manualy, the number of tendons are important in device usability. Therefore the GRIPIT makes tripod grasp (which requires 9 joints to move) using only a single tendon. It can be thought as the under-actuated tendon routing which is explained [here][uatd_external_link] in detail. 

Since the under-actuated tendon routing also provides adaptability (which is ), the use of under-actuated tendon routing was a


 Therefore an under-actuated tendon routing is used in this device because this tendon routing also increases the adaptability of the device; details of under-actuated tendon routing is explained [here][uatd_extenral_link].) 
 
 However, when the under-actuation mechanism is used, the device performance can be highly affected by the human characteristics. For this reason I designed a specific tendon routing that does not depend on the human characteristics as explained below.

#### 4. Specific tendon routing that does not depend on the human characteristics
When the wearable robot is under-actuated, the robot function can be changed as the wearer changes. For instance, when a single tendon pulls serially connected joints (e.g., when a single tendon pulls three joints in a single finger), torque applied to these joints will be affected by tension of a single tendon; we can not control torque applied at three joints individually. Therefore the motions of three joints will depend on their impedance. 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/GRIPIT/ClosedTendonRouting.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 GRIPIT overview</figcaption>
</figure>

To make the robot that does not depend on the human characteristics, I have designed the device with closed-tendon routing. The closed-tendon routing has a simple principle; the routing can be found in Fig.1. The tendon routing of GRIPIT operates similar to the lasso as it passes the thumb, index and middle fingers simultaneously. One end side of the tendon is fixed at the middle finger (A in Fig.1) and it passes through in the order of B(index finger), C(thumb), D(middle finger), and E(wrist). Since this tendon routing makes the fingertips come together to one point regardless of the joint properties, performance of the GRIPIT does not depend on the human properties. To validate whether 

## Social funding (Kakao Story funding in korea)

Since I wanted GRIPIT to be used in real-life, I promoted the device through social funding. The videos introduced in this social funding are as below:

<iframe width="950" height="534" src="https://www.youtube.com/embed/3KyD_rQ8nPc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---
<iframe width="950" height="534" src="https://www.youtube.com/embed/9meejoST5XM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---
<iframe width="950" height="534" src="https://www.youtube.com/embed/JEQjz-dg03A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---
<iframe width="950" height="534" src="https://www.youtube.com/embed/1_h7CL2VPlw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


[JNER_pdf]:https://github.com/bc-kim/bc-kim.github.io/blob/master/assets/Publications/Kim%20et%20al.%20-%202017%20-%20Development%20and%20assessment%20of%20a%20hand%20assist%20device%20GRIPIT.pdf
[JNER_link]: https://jneuroengrehab.biomedcentral.com/articles/10.1186/s12984-017-0223-4
[home_link]: /#about-me
[reason_link]: gripit#reason-why-hand-wearable-robot-is-difficult-to-use-in-real-life
[result_link]: /researches/gripit#validation-of-the-gripit
[uatd_internal_link]: /researches/gripit#3-under-actuated-tendon-routing
[uatd_extenral_link]: /researches/tdm