---
layout: page
title: 幻灯片
header: 幻灯片
group: navigation
---
{% include JB/setup %}

<ul>
{% assign slideshows_list = site.static_files %}
{% include JB/slideshows_list %}
</ul>
