---
layout: home
---

<h2>Performances</h2>
<ul>
{% assign grouped_categories = site.performances | group_by: "category" %}
{% for category in grouped_categories %}
<li class="category">
  {{ category.name }}
  <ul>
    {% assign grouped_years = category.items | group_by: "year" | sort: "name" | reverse %}
    {% for year in grouped_years %}
    <li class="year">
      {{ year.name }}
      <ul>
        {% assign sorted_performances = year.items | sort: "date" | reverse %}
        {% for performance in sorted_performances %}
        <li><a href="{{ performance.url }}">{{ performance.title }}</a></li>
        {% endfor %}
      </ul>
    </li>
    {% endfor %}
  </ul>
</li>
{% endfor %}
</ul>

{% assign desired_order = "Tri-C Post Degree Cert Classes,New School" | split: "," %}
{% assign grouped_dataprojects = site.dataprojects | group_by: "category" %}
{% assign reordered_dataproject_categories = "" | split: "" %}
{% for category_name in desired_order %}
  {% for category in grouped_dataprojects %}
    {% if category.name == category_name %}
      {% assign reordered_dataproject_categories = reordered_dataproject_categories | push: category %}
    {% endif %}
  {% endfor %}
{% endfor %}
{% for category in grouped_dataprojects %}
  {% unless desired_order contains category.name %}
    {% assign reordered_dataproject_categories = reordered_dataproject_categories | push: category %}
  {% endunless %}
{% endfor %}

<h2>Data Projects</h2>
<ul>
{% for category in reordered_dataproject_categories %}
<li class="category">
  {{ category.name }}
  <ul>
    {% assign grouped_years = category.items | group_by: "year" | sort: "name" | reverse %}
    {% for year in grouped_years %}
    <li class="year">
      {{ year.name }}
      <ul>
        {% assign sorted_projects = year.items | sort: "date" | reverse %}
        {% for dataproject in sorted_projects %}
        <li><a href="{{ dataproject.url }}">{{ dataproject.title }}</a></li>
        {% endfor %}
      </ul>
    </li>
    {% endfor %}
  </ul>
</li>
{% endfor %}
</ul>

<!-- <h2>Typewriter Projects</h2>
<ul>
  {% assign grouped_types = site.typewriters | group_by: "type" %}
  {% for type in grouped_types %}
  <li class="category">
    {{ type.name }}
    <ul>
      {% assign grouped_years = type.items | group_by: "year" | sort: "name" | reverse %}
      {% for year in grouped_years %}
      <li class="year">
        {{ year.name }}
        <ul>
          {% assign sorted_posts = year.items | sort: "date" | reverse %}
          {% for post in sorted_posts %}
          <li><a href="{{ post.url }}">{{ post.title }}</a></li>
          {% endfor %}
        </ul>
      </li>
      {% endfor %}
    </ul>
  </li>
  {% endfor %}
</ul>
-->

<div id="scrollTrack">
  <div id="verticalScrollProgress"></div>
</div>

<style>
#scrollTrack {
  position: fixed;
  top: 25%;
  left: 50%;
  transform: translateX(-700px);
  width: 5px;
  height: 50%;
  background-color: rgba(255, 255, 255, 0.1);
  z-index: 9998;
}

#verticalScrollProgress {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 0%;
  background-color: #5bff32;
  z-index: 9999;
}

body {
  color: white;
  font-family: monospace;
  font-size: 16px;
  line-height: 1.4;
  margin: 0;
  min-height: 100%;
  overflow-wrap: break-word;
  background-image: url('/assets/backgroundme.jpg'); 
  background-size: cover; 
  background-position: center; 
  background-attachment: fixed;
  text-shadow: 
  0 0 0 black,
  1px 0 0 black,
  -1px 0 0 black,
  0 1px 0 black,
  0 -1px 0 black,
  1px 1px 0 black,
  -1px -1px 0 black,
  1px -1px 0 black,
  -1px 1px 0 black,
  2px 0 0 black,
  -2px 0 0 black,
  0 2px 0 black,
  0 -2px 0 black;
}

a {
  color: rgb(91, 255, 50);
  text-decoration: underline;
}
</style>

<script>
window.onscroll = function() {
  const track = document.getElementById("scrollTrack");
  const bar = document.getElementById("verticalScrollProgress");
  
  const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
  const scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
  const scrollPercent = (scrollTop / scrollHeight) * 100;
  
  // Keep the green bar inside the track
  bar.style.height = scrollPercent + "%";
};
</script>
