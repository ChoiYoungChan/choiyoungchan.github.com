---
title: "Sort"
layout: archive
permalink: categories/sort
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['Sort'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}