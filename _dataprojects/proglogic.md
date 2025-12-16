---
layout: post
title: IT1050 Programming Logic
category: "Tri-C Post Degree Cert Classes"
year: 2025
date: 2025-10-28
permalink: /_dataprojects/proglogic/
---

# Learning Log — IT1050 Programming Logic: Lab-by-Lab Reflections

*Repository: [timothymasso/IT1050-Programming-Logic](https://github.com/timothymasso/IT1050-Programming-Logic) · CRN 81766*  

Over the semester I completed a sequence of focused C# labs that built up programming fundamentals step-by-step. Below is a concise blog-style walkthrough of each lab, the core concepts I learned, and why they matter. This progression is practical: begin with I/O and data, add control flow and math, then model real-world entities with objects and collections.



## Lab One — Getting Started (LabOneContent)

What I learned
- C# console application structure (Main, namespaces).
- Primitive types: int, double, string, bool.
- Console I/O with `Console.ReadLine()` and `Console.WriteLine()`.
- Parsing input (`int.Parse`, `double.Parse`, `TryParse`) and basic arithmetic.



## Lab Two — Decisions and Branching (LabTwoContent)

What I learned
- Comparison operators: `>`, `<`, `>=`, `<=`, `==`, `!=`.
- Boolean operators: `&&`, `||`, `!`.
- Control flow with `if`, `else if`, and `else`.
- Simple input validation using conditional checks.



## Lab Three — Commission Calculations (CommissionLab)

What I learned
- Applying percentages and basic finance math (commissions, rates).
- Tiered logic: different rates for sales ranges or thresholds.
- Numeric formatting (currency, rounding).



## Lab Four — Speed Calculations (SpeedLab)

What I learned
- Translating formulas into code (e.g., `speed = distance / time`).
- Using conditionals to classify numerical results (within limit vs speeding).
- Handling edge cases (zero or negative time).



## Lab Five — Odd/Even (OddEven)

What I learned
- The modulus operator `%` to get remainders.
- Determining parity (odd vs even) of integers.
- Using the result in `if`/`else` branches.



## Lab Six — Parking Fee Calculator (ParkingCalculator)

What I learned
- Time arithmetic: computing elapsed time, rounding up to billing increments (e.g., next hour).
- Piecewise fee computation: different billing rules for different durations.
- Breaking real-world logic into clear program steps.



## Lab Seven — Employee Model (EmployeeLab)

What I learned
- Intro to object-oriented design: creating an Employee class with properties.
- Methods to encapsulate behavior (e.g., CalculatePay()).
- Encapsulation: grouping related data and functionality.



## Lab Eight — Employee Lab II (Employeelab2)

What I learned
- Extending classes with constructors, additional properties, and behaviors.
- Managing multiple objects using arrays or `List<T>`.
- Potential introduction to persistence (file I/O) or more advanced methods (raises, benefits).




## Lab Nine — Faculty Records (FacultyLab)

What I learned
- Managing collections of records: searching, sorting, and filtering.
- Iterating collections with loops and applying selection criteria.
- Introduction to library helpers (and optionally LINQ) to query data.



## Lab Ten — Lists and Dynamic Collections (LabList)

What I learned
- `List<T>` operations: add, remove, insert, iterate.
- Differences between fixed arrays and dynamic lists.
- Common list-based algorithms: search, indexing, and simple mutations.




## Mini Exams (Mini Exam 1 & Mini Exam 2)

What I learned
- Rapid reinforcement of fundamentals: variables, conditionals, loops, and arithmetic.
- Timed or constrained problem solving to solidify understanding.




## VSCode Bonus Lab

What I learned
- IDE productivity: running code, debugging, breakpoints, and stepping through code.
- Useful extensions and shortcuts that speed development.
- Formatting and diagnostic tools (linting, IntelliSense).




## Final Quiz

What I learned
- A comprehensive review across types, control flow, collections, and OOP.
- Reinforced concepts and identified remaining areas to practice.




## Final Project

What I learned
- Integrating topics: class design, collections, validation, user interaction, and program flow.
- Designing a program: breaking problems into classes and methods, iterative implementation, and testing.
- Delivering an end-to-end solution that demonstrates cumulative skills.





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
