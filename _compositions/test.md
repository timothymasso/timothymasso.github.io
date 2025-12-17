---
layout: post
title: Milestones Arrangment
category: "New School"
year: 2022
date: 2022-07-21
permalink: /_compositions/test/
---
<iframe src="/assets/compositions/test.pdf" width="100%" height="800px"></iframe>


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
  background-image: url('/assets/olddoe.png');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
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



