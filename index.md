---
layout: default
title: Thame the Discs - Ultimate Frisbee in Thame
---

<!-- Banner -->
<section id="banner">
  <div class="inner">
    <h2>Ultimate Frisbee in Thame</h2>
    <p>Ultimate is a fast-moving team sport enjoyed by millions of players the world over. Beginners find the game easy to learn and fun to play, so come along and discover why many think this is the ultimate team sport.</p>
  </div>
</section>

<!-- Wrapper -->
<section id="wrapper">
  {% for section in site.data.index_sections %}
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
