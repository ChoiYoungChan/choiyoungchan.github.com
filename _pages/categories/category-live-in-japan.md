---
title: "Live in Japan Diary"
layout: archive
permalink: categories/liveinjapan
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['Live in Japan Diary'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}