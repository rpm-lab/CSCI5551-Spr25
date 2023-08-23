---
layout: page
title: Home
description: CSCI5551 at the University of Minnesota.
nav_order: 1
permalink: /
---

# Introduction to Intelligent Robotic Systems
## CSCI5551-02 Fall 2023 at The University of Minnesota - Twin Cities
{: .fs-6 .fw-300 }
## M, W 1:00PM-2:15PM CT - Rapson Hall 45
{: .fs-5 .fw-300 }

<!-- This website describes a course still in development to be offered in the Spring 2023 semester.
{: .text-red-300 .bg-yellow-200 .fs-4 .fw-500} -->

The objective of this course is to introduce students to the principles of robotics. The main topics of interest covered in the class include: transformations in 3D, kinematics, inverse kinematics, velocity kinematics, and introduction to robot programming with the Robot
Operating System (ROS). If time permits, we will address other issues such as dynamics and those related to mobile robots, primarily sensing, estimation, and autonomous navigation later in the semester. Robot programming will be introduced in the context of the final project.

This course builds on and is indebted to materials from Prof. Nikolaos Papanikolopoulos (Univ of Minnesota), Prof. Junaed Sattar (Univ of Minnesota), and Professor Elizabeth A. Croft (Dean, College of Engineering, Monash University, Australia).

<div class="staff-row" >
<div markdown="1" class="staff-column">

## Instructors

{% assign instructors = site.staffers | where: 'role', 'Instructor' %}
{% for staffer in instructors %}
{{ staffer }}
{% endfor %}

</div>

</div>

{% assign teaching_assistants = site.staffers | where: 'role', 'Teaching Assistant' %}
{% assign num_teaching_assistants = teaching_assistants | size %}
{% if num_teaching_assistants != 0 %}
## Teaching Assistants

<div class="staffer-table">
{% for staffer in teaching_assistants %}
{{ staffer }}
{% endfor %}
</div>
{% endif %}
