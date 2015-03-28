---
layout: page
title: Articles
---
Articles are ordered chronologically.
<p class="message">
  In the near future, I will whip up a more elegant solution for traversing articles by category.
</p>

{% for post in site.posts reversed%}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
