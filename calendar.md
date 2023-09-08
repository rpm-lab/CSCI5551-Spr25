---
layout: page
title: Calendar
description: Calendar with course content for CSCI5551-02 Fall 2023 at the University of Minnesota.
nav_order: 3
---

# Tentative Schedule
![Calendar](/CSCI5551-Fall23-S2/assets/images/calendar_draft.png){: .cal-img }

{% include google_sheet.html %}

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