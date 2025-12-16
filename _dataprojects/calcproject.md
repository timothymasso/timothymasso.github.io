---
layout: post
title: Honors Calculus Project
category: "Tri-C Post Degree Cert Classes"
year: 2025
date: 2025-12-15
permalink: /_dataprojects/calcproject/
---

This project was completed as part of Math 161H Honors Calculus I at Cuyahoga Community College under Professor Sean Sheridan during the Fall 2025 semester. The course uses Calculus: Early Transcendental Functions (8th edition) by Larson and Edwards as the primary textbook.


Calculus I introduces fundamental concepts for analyzing change and motion. The course begins with limits, which describe the behavior of functions as inputs approach specific values, and continuity, which ensures functions have no breaks or jumps. Building on limits, we study derivatives—the instantaneous rate of change of a function—using techniques like the power rule for polynomial functions, the product and quotient rules for combinations of functions, and the chain rule for composite functions. We also explore implicit differentiation for equations that aren't solved for a single variable and calculate higher-order derivatives to analyze acceleration and concavity.


These derivative tools enable us to solve optimization problems by finding maximum and minimum values, analyze related rates where multiple quantities change simultaneously, and use the Mean Value Theorem to understand average versus instantaneous rates of change. The course also covers curve sketching using derivatives to identify increasing/decreasing intervals, concavity, inflection points, and asymptotes.


In the second half of the course, we study antiderivatives and integration. The Fundamental Theorem of Calculus connects differentiation and integration, showing that these operations are inverses. We learn to evaluate definite integrals to calculate areas, volumes, arc lengths, and other accumulated quantities. Throughout the course, we apply these concepts to real-world problems in physics, engineering, economics, and the natural sciences.


This project applies these calculus concepts to determine the optimal descent path for an aircraft landing.


The prompt:
<iframe src="{{ site.url }}/assets/Proj 2.pdf" width="100%" height="850px"></iframe>



My analysis: 
<iframe src="{{ site.url }}/assets/Timmasso proj.pdf" width="100%" height="850px"></iframe>



My presentation:
<iframe src="{{ site.url }}/assets/Timmasso pres.pdf" width="100%" height="850px"></iframe>


<style>
body {
  color: white;
  font-family: monospace;
  font-size: 16px;
  line-height: 1.6;
  margin: 0;
  min-height: 100vh;
  background-image: url('/assets/tc.jpg');
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
