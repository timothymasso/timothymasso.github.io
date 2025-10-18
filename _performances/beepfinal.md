---
layout: post
title: Beep Ensemble Final Project (under construction)
category: "New School"
year: 2021
date: 2021-11-04
permalink: /_performances/beepfinal/
---


<iframe width="560" height="315" src="https://www.youtube.com/embed/Yga5zG9bOcs?si=yrbleCq-_yyR-rfj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>





<link rel="shortcut icon" href="/assets/favicon.ico" type="image/x-icon">
<link rel="icon" href="/assets/favicon.ico" type="image/x-icon">

<style>
body {
  color: white;
  font-family: monospace;
  font-size: 16px;
  line-height: 1.4;
  margin: 0;
  min-height: 100%;
  overflow-wrap: break-word;
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

body {
    background-image: url('/assets/5thfloor.webp'); 
    background-size: cover; 
    background-position: center; 
    background-attachment: fixed; 
}

a {
    color:rgb(255, 255, 255); /* This changes the link color */
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