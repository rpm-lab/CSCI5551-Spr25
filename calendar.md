---
layout: page
title: Calendar
description: Calendar with course content for CSCI5551-02 Fall 2023 at the University of Minnesota.
nav_order: 3
---
# Current Running Schedule
{% for module in site.modules %}
{{ module }}
{% endfor %}

<h1> Snapshot of Planned Schedule </h1>
<div>
<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSkQMklHg9700JewJbMwF7d5ZNibp5xxygNXpBAZf7CrqoS7RUwBQDwx6HaZtIuJFsWYmn8DNKjOJoz/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false"></iframe>
</div>

<!-- # Snapshot of Planned Schedule
![Calendar](/CSCI5551-Fall23-S2/assets/images/calendar_draft.png){: .cal-img } -->

<!-- {% include google_sheet.html %} -->

<!-- <table>
    <thead>
      {% for row in site.data.google_sheet limit:1 %}
        <tr>
          {% for col in row %}<th>{{col}}</th>{% endfor %}
        </tr>
      {% endfor %}
    </thead>
    <tbody>
      {% for row in site.data.google_sheet offset:1 %}
        <tr>
          {% for col in row %}<td>{{col}}</td>{% endfor %}
        </tr>
      {% endfor %}  
    </tbody>
  </table> -->