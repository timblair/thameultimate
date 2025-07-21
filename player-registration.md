---
layout: default
title: Thame the Disc: Player Registration
---

<!-- Banner -->
<section id="banner">
  <div class="inner">
    <h2>Playing with Thame the Disc</h2>
    <p>To play or train regularly with Thame the Disc, we need to collect some information about you. For insurance purposes, you'll also need to be a member of the UK Ultimate Association, and under-18s will need a parent or guardian to complete a consent form.</p>
  </div>
</section>

<!-- Wrapper -->
<section id="wrapper">
  {% for section in site.data.player_registration_sections %}
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