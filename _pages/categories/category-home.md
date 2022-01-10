---
title: "Home"
layout: archive
permalink: categories/home
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Home %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}