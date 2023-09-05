---
layout: page
title: Home
description: Home page for CSCI5551-02 Fall 2023 at the University of Minnesota.
nav_order: 1
permalink: /
---

# Introduction to Intelligent Robotic Systems
## CSCI5551-02 Fall 2023 at The University of Minnesota - Twin Cities
{: .fs-6 .fw-300 }
## M, W 1:00PM-2:15PM CT - [Rapson Hall 45](https://roomsearch.umn.edu/rooms/f1b4771f-5e2e-42a7-aad9-0c5ca96459be)
{: .fs-5 .fw-300 }

<!-- This website describes a course still in development to be offered in the Spring 2023 semester.
{: .text-red-300 .bg-yellow-200 .fs-4 .fw-500} -->

The goal of this course is to introduce students to robotics principles, covering key topics such as 3D transformations, robot kinematics, forward and inverse kinematics, path planning, configuration spaces, sampling-based planning, basic motion control algorithms, and state estimation for mobile robots, which includes mapping, localization, and SLAM. Students will gain hands-on experience in programming robots in the [Java threejs](https://threejs.org/) environment. In later projects, they will have the opportunity to control real-world robots using their virtual counterparts and codebase. There will be a open-ended final project where students can apply their skills acquired throughout the semester to explore new ideas. They will present their projects to a wider audience through poster presentations and demos.

This course builds on and is indebted to materials from - 
- [Prof. Chad Jenkins](https://ocj.name/) (Univ of Michigan) and the staff of [autorob.org](https://autorob.org/#staff)
- [Prof. Nikolaos Papanikolopoulos](https://www-users.cse.umn.edu/~papan001/) (Univ of Minnesota), 
- [Prof. Junaed Sattar](https://junaedsattar.cs.umn.edu/) (Univ of Minnesota)

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
