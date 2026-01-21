---
layout: default
title: Thame the Disc - Ultimate Frisbee in Thame — Juniors
---

<!-- Banner -->
<section id="banner">
  <div class="inner">
    <h2>Ultimate Frisbee in Thame for Kids</h2>
    <p>Ultimate is a fast-moving game which can help young people stay fit and healthy. There are lots of opportunities to develop new skills and it’s a great way to socialise and make friends. It’s great exercise, fully inclusive and has responsibility, fun and teamwork at its heart.</p>
  </div>
</section>

<!-- Wrapper -->
<section id="wrapper">
  {% for section in site.data.juniors_sections %}
    {% include spotlight.html
      id=section.id
      style=section.style
      image=section.image
      link=section.link
      alt=section.alt
      title=section.title
      content=section.content
      button_url=section.button_url
      button_text=section.button_text
      features=section.features
    %}
  {% endfor %}
</section> 
