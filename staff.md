---
layout: page
title: 🧑‍🏫 Staff
description: A listing of all the course staff members.
nav_order: 4
---

# **Staff**

Jump to: [Instructors](#instructors), [Teaching Assistants](#teaching-assistants), [Tutors](#tutors)

**Email [data8@berkeley.edu](mailto:data8@berkeley.edu) for all logistical and student support questions!**



## Instructors
<div class="role flex">
{% assign instructors = site.staffers | where: 'role', 'Instructor' %}
{% for staffer in instructors %}
{{ staffer }}
{% endfor %}
</div>


<!-- ## Head Teaching Assistants -->

<!-- {% assign head_teaching_assistants = site.staffers | where: 'role', 'Head Teaching Assistant' %}
{% assign num_head_teaching_assistants = head_teaching_assistants | size %}
{% if num_head_teaching_assistants != 0 %}

<div class="role flex">
{% for staffer in head_teaching_assistants %}
{{ staffer }}
{% endfor %}
{% endif %}
</div> -->


## Teaching Assistants

{% assign teaching_assistants = site.staffers | where: 'role', 'Teaching Assistant' %}
{% assign num_teaching_assistants = teaching_assistants | size %}
{% if num_teaching_assistants != 0 %}


<div class="role flex">
{% for staffer in teaching_assistants %}
{{ staffer }}
{% endfor %}
{% endif %}
</div>

## Tutors

{% assign tutors = site.staffers | where: 'role', 'Tutor' %}
{% assign num_tutors = tutors | size %}
{% if num_tutors != 0 %}

<div class="role flex">
{% for staffer in tutors %}
{{ staffer }}
{% endfor %}
{% endif %}
</div>
