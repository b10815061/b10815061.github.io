---
layout: page
title: Virtual Room Reservation Assistant (VRRA)
description: A mimic of online reservation system to multi-users use. Integrated with Google Authentication API and Google Calander API. This is the final project of Software Engineering CSXXXX.
img: assets/img/VRRA/MVC.png
importance: 1
category: school
related_publications: false
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/VRRA/Google_SignIn.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/VRRA/Google_Mail.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/VRRA/Google_Calander.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    We integrated various GCP-based APIs into our service. During login, users are prompted with Google authentication (left) for easy access. When an event is created, updated or deleted, all users involved in the process receive notifications via Gmail API (mid). Additionally, events are automatically updated on the calendar using Google Calendar API (right).
</div>
The project was managed by React + Redux framework for the frontend, GoLang and GORM to interchange information to our MySQL database. During each request, a Jason Web Token was involved to check the user validality.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/VRRA/Project_MainPage.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/VRRA/Update_Page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The main selection page of the VRRA system. Each slot is indicated by color, and users can navigate to them by clicking on available slots (left). Inside each section, users provide the detailed information of the participant and other relevant information (right), which will be presented in the invitation letter sent via Gmail API.
</div>

This project follows a strict concept of software engineering principle, here we provide our software modeling and package documentation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/VRRA/MVC.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/VRRA/package_usage.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


