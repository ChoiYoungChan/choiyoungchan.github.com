---
title: "DataStructure"
layout: archive
permalink: categories/data-structure
author_profile: true
sidebar_main: true
---

***

{% assign posts = site.categories['datastructure'] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}