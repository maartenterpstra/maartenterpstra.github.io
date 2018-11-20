---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* BSc in Computing Science, University of Groningen, July 2014
  * Thesis supervisor: prof. dr. A. Lazovik
  * Thesis title: Applying web-scale architectures to legacy systems. 
* MSc in Computing Science, University of Groningen, January 2017
  * Thesis supervisor: prof. dr. A.C. Telea
  * Thesis title: Dense Skeletons for Image Compression and Manipulation.
* Ph.D in Deep Learning for real-time MRI-guided radiotherapy, 2022 (expected)

Work experience
======
* January 2017 - July 2018: Software Developer
  * Royal Netherlands Meteorological Institute (KNMI)
  * Duties included: 
   * Frontend and Backend development (React and Spring/Java, respectively)
   * Devops responsiblities (development, testing, and deployment)
   * Co-creating institute-wide standards on the whole software development pipeline
  
{% if site.publications %}
Publications
======
  <ul>{% for post in site.publications %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
{% endif %}
{% if site.talks %}
Talks
======
  <ul>{% for post in site.talks %}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>
{% endif %}
Teaching
======
  <ul>{% for post in site.teaching %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  