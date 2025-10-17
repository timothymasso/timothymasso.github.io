---
layout: post
title: Internet Geographies Project
category: "New School Class"
year: 2024
date: 2024-04-20
permalink: /_dataprojects/internetgeo/
---
<link rel="shortcut icon" href="/assets/favicon.ico" type="image/x-icon">
<link rel="icon" href="/assets/favicon.ico" type="image/x-icon">

[comment]: link to github repo of the project

# Project Process

![2024 Haneda Airport runway collision](/assets/Project2All/3240.webp)
2024 Haneda Airport runway collision

# Aviation Accidents Data Project  
**Mapping 40 Years of Commercial Air Crashes**   
[Code on GitHub](https://github.com/timmasso/Internet-Geo-Project-1-and-2)

[Finished Site](https://timothymasso.com/Internet-Geo-Project-1-and-2/PlaneMap.html)


## Introduction
Earlier this year, several major air incidents hit the news, including the Alaskan Airlines flight where a door panel came off mid-flight and the Japan Airlines crash involving a Coast Guard plane. It made me wonder how often serious aviation accidents actually happen.  
The media made it sound like flying had suddenly become dangerous again. I wanted to find out if that was true or if these were rare exceptions in an industry that is generally very safe.  
For this project, I decided to map aviation accidents using historical data. My goal was to visualize more than forty years of incidents and see whether any long-term trends existed in commercial air safety.


## Getting the Data
The main data source was the **NTSB’s CAROL database**, which lists every aviation accident in the United States. It’s a detailed resource where you can filter by year, aircraft type, operation category, and other factors.  
Since it was my first time using CAROL, I had to experiment with the search functions and data exports. I eventually learned that scheduled passenger flights fall under **Part 121 operations**, which include airlines like United, Delta, and Alaska.  
I downloaded all Part 121 airplane accidents from **1982 through 2025**, giving me a dataset covering more than forty years of commercial aviation history. I exported the results as a CSV file for further analysis.


## What’s in the Data
The CSV contained many fields. The most useful were:

- Case number  
- Date and location  
- Injury counts (fatal, serious, minor)  
- Aircraft make and model  
- Airport information  
- Aircraft damage level  
- Weather and probable cause  

For this project, I focused on:

- Date (for identifying trends)  
- Coordinates (for mapping)  
- Make and model (to see which manufacturers were most common)  
- Damage level (to filter for serious incidents)


## Filtering and Cleaning the CSV
I used **PapaParse**, a JavaScript library for reading and filtering CSV data, inside a Node.js environment.  

I wanted to keep only the rows that met these conditions:

- Aircraft made by Boeing, Airbus, Embraer, and other major manufacturers  
- Incidents that occurred in the United States  
- Aircraft listed as *Destroyed* or having *Substantial* damage  

The filtering function looked like this:

```javascript
function findRows(csvData, makeColumn, targetMakes, damageColumn, targetDamage, countryColumn, targetCountry) {
  return csvData.filter((row) =>
    targetMakes.includes(row[makeColumn]) &&
    targetDamage.includes(row[damageColumn]) &&
    targetCountry.includes(row[countryColumn]) &&
    row["Latitude"] !== "" &&
    row["Longitude"] !== ""
  );
}
```

After filtering, I exported the results into a new CSV file. This smaller dataset was ready for mapping.

## Converting to GeoJSON
The next step was converting the CSV into **GeoJSON**, a format used by mapping libraries such as **Leaflet**.  

GeoJSON represents data as geographic features, each with coordinates and custom properties. I started by defining the structure:

```javascript
var geoJson = {
  type: "FeatureCollection",
  name: "CommercialAirCrashes",
  features: []
};
```

Each CSV row is converted to a Feature with properties and Point geometry; example conversion loop:

```javascript
for (let i in r.data) {
  var b = {
    type: "Feature",
    properties: {
      NtsbNo: r.data[i].NtsbNo,
      EventDate: r.data[i].EventDate,
      Country: r.data[i].Country,
      City: r.data[i].City,
      State: r.data[i].State,
      AccidentLat: parseFloat(r.data[i].Latitude),
      AccidentLong: parseFloat(r.data[i].Longitude),
      AirportName: r.data[i].AirportName,
      AirportID: r.data[i].AirportID,
      Registration: r.data[i].N,
      FatalInjuryCount: r.data[i].FatalInjuryCount,
      SeriousInjuryCount: r.data[i].SeriousInjuryCount,
      MinorInjuryCount: r.data[i].MinorInjuryCount,
      AirCarrier: r.data[i].Operator,
      Make: r.data[i].Make,
      Model: r.data[i].Model,
      AirCraftDamage: r.data[i].AirCraftDamage,
      ProbableCause: r.data[i].ProbableCause,
      ObjectId: parseInt(i)
    },
    geometry: {
      type: "Point",
      coordinates: [
        parseFloat(r.data[i].Longitude),
        parseFloat(r.data[i].Latitude)
      ]
    }
  };
  geoJson.features.push(b);
}
```

Each row of the CSV became a feature in this GeoJSON file, including values such as the aircraft model, damage level, and number of injuries. After populating the data, I saved it as a JSON file.  
A typical entry looked like this:

Example GeoJSON entry (trimmed):

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "NtsbNo": "DCA24LA065",
        "EventDate": "2024-01-10",
        "Make": "BOEING",
        "Model": "737",
        "AirCraftDamage": "Substantial",
        "AirCarrier": "UNITED AIRLINES INC"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [-95.34, 29.99]
      }
    }
  ]
}
```


## Linking Airport Coordinates
Once the crash sites were plotted, I wanted to add the coordinates of the **origin airports**.  
To do that, I used a separate CSV of U.S. airport codes that included latitude and longitude. I matched each incident’s airport ID or name to the airport data and added the coordinates.  
Some airport fields were missing or formatted differently, so I added fallback logic, if no airport match was found, the program used the accident coordinates instead.


## Visualizing with Leaflet
With the GeoJSON ready, I used **Leaflet** to display everything on an interactive map.  

I created two marker types:  
✈️ for crash sites  
🗼 for airports  

Then I drew red lines connecting each airport to the corresponding accident location.

Here is the minimal Leaflet initialization and marker snippet I used:

```javascript
let map = L.map("map").setView([25, -90], 4);
L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", { maxZoom: 19 }).addTo(map);

let crashIcon = L.icon({ iconUrl: "Assets/airplane.png", iconSize: [30, 30] });
let towerIcon = L.icon({ iconUrl: "Assets/tower.png", iconSize: [30, 30] });

L.geoJson(dataFinal, {
  pointToLayer: function (feature, latlng) {
    if (feature.geometry.coordinates[0] !== 0) {
      return L.marker(latlng, { icon: crashIcon }).bindPopup(
        `Date: ${feature.properties.EventDate}<br/>NTSB: ${feature.properties.NtsbNo}<br/>Make: ${feature.properties.Make}`
      );
    } else return null;
  }
}).addTo(map);
```

Each marker includes a popup with details such as the date, aircraft type, and number of injuries. A small legend in the corner shows the total number of serious incidents since 1982.  
The layout is simple, but it conveys the information clearly.


## Kepler Experiments
I also imported the dataset into **Kepler.gl**, a browser-based visualization tool. It allowed me to connect accident sites and airports with arcs and overlay heat grids showing where serious incidents occurred most frequently.  
These visualizations made it easy to see patterns, most events happen near airports or along high-traffic routes.


## What the Data Shows
From 1982 through 2025, the dataset contains **2,529 incidents** involving U.S. commercial airliners. Out of these, **271 were classified as serious**.

### Key Observations
- Serious accidents mostly occur during takeoff, landing, or taxiing.  
- Even when aircraft are heavily damaged, passengers are often unharmed.  
- Considering the number of flights that occur every year, serious accidents are extremely rare.  
- There is some uncertainty about underreporting; minor incidents may go unreported unless the damage is significant.  

Still, the general trend is clear: **commercial air travel is remarkably safe**.

## Closing Thoughts
This project started from curiosity about whether the recent aviation headlines pointed to a larger issue. Based on the data, the answer appears to be no. serious incidents are uncommon and have not become more frequent.  
However, there is growing public attention on manufacturing and maintenance practices, which is a good thing. Greater transparency leads to better safety.  
Now that the base dataset and visualization system are complete, future work could include adding international data or creating a **time-lapse view** of incident trends over the decades.

[Finished Site](https://timothymasso.com/Internet-Geo-Project-1-and-2/PlaneMap.html)

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
    background-image: url('/assets/plane.webp'); 
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

