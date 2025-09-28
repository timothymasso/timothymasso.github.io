---
layout: post
title: "Olivetti Studio 46 (in progress)"
date: 2025-04-19
type: "Desktop"          # now the top-level category
year: 1974
permalink: /_typewriters/olivettistudio/
---

<link rel="shortcut icon" href="/assets/favicon.ico" type="image/x-icon">
<link rel="icon" href="/assets/favicon.ico" type="image/x-icon">

The Olivetti Studio 46 is an Italian-made portable typewriter from the mid-1970s, designed by Ettore Sottsass and his team at Olivetti. Introduced in 1974, the Studio 46 represents a bridge between the elegance of Olivetti’s earlier machines and the practical durability required for professional and educational use.  

## History  

Olivetti, known for its fusion of industrial design and technological innovation, had established itself globally by the 1960s with iconic machines such as the Lettera 22 and 32. In 1974, the Studio 46 was released as a heavier-duty portable, intended to serve schools, offices, and writers who required a robust yet still mobile typewriter. Its design reflects the bold, modernist aesthetic of the 1970s while retaining Olivetti’s tradition of sleek, functional form. As a successor to the Studio 45, the 46 offered incremental refinements and became one of Olivetti’s most popular educational and institutional models through the late 1970s and early 1980s.  

## Features  

The Olivetti Studio 46 is a large-bodied portable, housed in a rugged plastic shell with smooth, geometric lines characteristic of Sottsass-era Olivetti design. It employs a basket-shift mechanism, providing a lighter and more consistent touch than older carriage-shift models. The keyboard layout is spacious and responsive, paired with a clear typeface that ensured legibility for long typing sessions. Standard features include a tabulator, margin release, line-spacing selector, and a bright, audible bell. Its carrying case, though substantial, preserved its portability. The Studio 46 was produced in several striking color variations, most famously in Olivetti’s bold blues and greens, aligning with the company’s distinctive design philosophy.  

## 1974 Release Context  

The 1974 debut of the Olivetti Studio 46 coincided with Olivetti’s continued expansion into global markets and its commitment to typewriter design even as word processors were beginning to emerge. The Studio 46 is emblematic of the company’s ability to merge utility with modernist style, making it a favorite in classrooms and offices of the era. Today, surviving machines are valued not only for their durability but also for their place in the lineage of Olivetti’s design history. The Studio 46 captures the essence of 1970s Italian industrial design — practical, stylish, and built to endure.  




<style>
body {
  color: #ffffffff; /* vivid lime green */
  font-family: monospace;
  font-size: 16px;
  line-height: 1.6;
  margin: 0;
  min-height: 100vh;
  background-image: url('/assets/oli.webp');
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

a {
  color: #5bff32;
  font-size: 18px;
  text-decoration: underline;
  text-shadow: none !important;  /* Remove text-shadow from body */
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

