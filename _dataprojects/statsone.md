---
layout: post
title: Notes From Stats 1
category: "Tri-C Post Degree Cert Classes"
year: 2025
date: 2025-08-10
permalink: /_dataprojects/statsone/
---

<link rel="shortcut icon" href="/assets/favicon.ico" type="image/x-icon">
<link rel="icon" href="/assets/favicon.ico" type="image/x-icon">

<style>
body {
  color: white;
  font-family: monospace;
  font-size: 16px;
  line-height: 1.6;
  margin: 0;
  min-height: 100vh;
  background-image: url('/assets/treedooo.gif');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  position: relative;
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

body::before {
  content: "";
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0, 0, 0, 0.55); /* darken background slightly */
  z-index: -1;
}

a {
  color: #fff;
  text-decoration: underline;
}

/* Strong, crisp shadow outline 
body, a {
  text-shadow: 
    2px 2px 4px rgba(0,0,0,1),    tight drop shadow 
    -2px -2px 4px rgba(0,0,0,1),  outline in opposite direction 
    0px 0px 8px rgba(0,0,0,1);    subtle glow to soften edges 
}
*/

</style>

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




# Summer 2025 Statistics Review – My First Step Toward a New Career 

In the summer of 2025, I started a class that was very different from anything I had done before. I graduated in 2024 with a degree in Jazz and Contemporary Music from The New School. Back then, my world was mostly about playing music, improvising, and performing. But during college, I took a class that introduced me to data visualization. That means using pictures and maps to show information.

We did not do heavy math or complicated analysis. Instead, we used tools like **Leaflet** and **OpenStreetMap** to create interactive maps from survey data. It was a creative and artistic way to work with data. That experience sparked my interest. I realized I liked not just looking at data but also working with it.

After graduating, I moved back to Cleveland and spent some time thinking about my career. Ohio offers “microcredential” programs. These are short courses that teach specific skills. I took classes in Excel, Minitab, Power BI, and data analytics. These were taught by people working in those fields. I quickly learned two things:

- I enjoyed this kind of work much more than I expected
- I wanted to learn a lot more

That is how I decided to enroll in the **Post-Degree Professional Certificate in Data Analytics** at Cuyahoga Community College, also called Tri-C. The classes were affordable and flexible. Most importantly, they help me work toward my goal of getting a Master’s degree in Applied Mathematics and Statistics at Bowling Green State University in Fall 2026. Since my music degree did not include college-level math courses, I need to build that foundation now.

This brings me to the course I took: **Elementary Probability and Statistics I**. It was a 5-week fast-paced class using the textbook *Statistics: Informed Decisions Using Data (6th Edition)* by Michael Sullivan, III. This review talks about what I learned in that class, but it also marks something new, it is the first document I wrote using **LaTeX**.

LaTeX is a special way to write papers, especially those with math, formulas, and tables. It is different from programs like Microsoft Word. LaTeX helps make documents look professional and keeps everything neat, even with lots of numbers and equations. There is a learning curve, but I wanted to get used to it before starting my master’s degree. Writing this review in LaTeX helps me learn the course and practice writing in a way I will need later.

Before you start reading, This note compilation is the first of many I hope to write. It is part summary, part practice, and part record of my journey from music to math.


### Full PDF (still in progress)

<iframe src="{{ site.url }}/assets/test.pdf" width="100%" height="850px"></iframe>