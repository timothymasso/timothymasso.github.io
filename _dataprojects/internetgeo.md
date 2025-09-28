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

## Introduction

[Code here.](https://github.com/timmasso/Internet-Geo-Project-1-and-2) 



Lately, I’ve been particularly interested in air disasters, especially in light of the recent aviation incidents that occurred earlier this year. Notable events include the Alaskan Airlines flight where a door panel detached mid-flight and the Japan Airlines accident in which a commercial aircraft collided with a Japanese Coast Guard plane. These incidents sparked widespread media coverage and public discussion about air safety, raising concerns about how secure modern air travel really is.

For the class project, I wanted to explore this issue further by mapping aviation accidents and analyzing historical data to determine just how risky air travel is. Are these recent incidents rare, isolated anomalies in an otherwise safe industry, or do they reveal a broader pattern that has been overlooked until now? By visualizing past accidents and examining trends, I aimed to understand whether the media is simply shedding light on an already existing issue or if there has been a recent shift in aviation safety that warrants greater attention



*Gathering Data:*

To gather data for this project, I utilized the **CAROL query website**, the official database of the **National Transportation Safety Board (NTSB)**, which contains detailed records of aviation accident investigations. Since this was my first time working with the platform, I needed to familiarize myself with its search functionality. This involved experimenting with different queries, exporting multiple datasets, and working through CSV files to understand how the information was structured. Initially, this process took some time as I figured out how to refine my searches effectively and ensure I was retrieving relevant data.

Once I became comfortable navigating the database, I had to determine the specific regulatory category under which commercial airline flights fall. After a quick online search, I found that these flights are classified under **Part 121**, which applies to scheduled air carriers operating large aircraft. Knowing this, I adjusted my search criteria accordingly.

For this project, I decided to analyze data starting from **1982**, choosing this year arbitrarily to ensure a dataset spanning over **40 years**, which would provide a broad historical perspective on aviation safety. I set the search parameters to include only **commercial flights** and filtered by **“Airplane”** as the aircraft type. The search yielded a substantial number of records, which I then exported into a **CSV file** for further processing and analysis.

This dataset would allow me to explore long-term trends in commercial aviation incidents and assess whether recent accidents are outliers or part of a larger, ongoing pattern that may have previously gone unnoticed by the media and the public.



### Organizing the Data

Fortunately, the **NTSB** maintains a highly detailed and structured dataset, meaning that most of the key information I needed was already included in the exported CSV file. The dataset contained various columns, such as:

- **NTSB Case Number**
- **Event Type**
- **Event Date**
- **Location Details** (city, state, country)
- **Injury Counts** (fatal, serious, minor)
- **Aircraft Details** (make, model, category)
- **Airport Information**
- **Aircraft Damage**
- **Weather Conditions**
- **Probable Cause**

Among these, the most crucial fields for my analysis were:
- **NTSB Case Number** (to track specific incidents)
- **Date of the Incident** (for historical trend analysis)
- **Geographic Coordinates** (to map the locations of accidents)
- **Airport of Origin and Associated Airports** (to see if certain locations had higher accident rates)
- **Injury Categories** (to assess the severity of each incident)
- **Aircraft Damage** (to distinguish between minor incidents and catastrophic failures)

One of the key aspects I wanted to analyze was the most commonly used **airframe manufacturers** over the given time period. To accomplish this, I needed to filter the dataset based on aircraft make and model. The process involved instructing the code to:

1. Identify the **specific manufacturer names** I was searching for.
2. Scan the relevant **column in the CSV file** for those names.
3. Extract and store **only the full rows** where a match was found.

By applying these filtering techniques, I could determine which aircraft manufacturers appeared most frequently in **over 40 years of commercial aviation accident reports**, helping to identify potential patterns in airframe usage and incident rates.

### Extracting Specific Rows from CSV

To process and analyze the dataset, I chose **PapaParse**, a JavaScript library designed for parsing CSV files. After researching and selecting it for its efficiency and ease of use, I set up a **Node.js** environment and integrated PapaParse into the project.

I began by defining the key parameters for the data I wanted to filter:
- **Aircraft Makes**: This included major manufacturers like **Airbus**, **Boeing**, **Embraer**, and others.
- **Countries**: I focused on incidents occurring in the **United States**.
- **Aircraft Damage**: I specifically looked for incidents where the aircraft was either **Destroyed** or had **Substantial** damage.

Here’s how I set up the filter function to narrow down the dataset:

```javascript
function findRows(csvData, makeColumn, targetMakes, damageColumn, targetDamage, countryColumn, targetCountry) {
  return csvData.filter((row) => 
    targetMakes.includes(row[makeColumn]) && 
    targetDamage.includes(row[damageColumn]) && 
    targetCountry.includes(row[countryColumn]) && 
    row["Latitude"] != "" && 
    row["Longitude"] != ""
  );
}
```

Next, I read in the data and applied the filter using PapaParse:
```javascript
Papa.parse(fileContent, {
  header: true,
  skipEmptyLines: true,
  complete: function (results) {
    const rowsWithData = findRows(
      results.data,
      makeColumn,
      targetMakes,
      damageColumn,
      targetDamage,
      countryColumn,
      targetCountry
    );
    writeRowsToCSVFile(rowsWithData, outputPath);
  }
});
```

The filtered dataset was then exported to a new CSV file:

```javascript
function writeRowsToCSVFile(rows, outputPath) {
  const csvContent = Papa.unparse(rows, { header: true });
  fs.writeFileSync(outputPath, csvContent);
  console.log(`Results exported to ${outputPath}`);
}
```

Once I filtered the data, I was able to focus on the specific incidents I needed for further analysis, such as converting the dataset to GeoJSON format for mapping and visualizing aviation trends over time.

### Converting Data to GeoJSON Format for Leaflet Integration

In order to display the data on an interactive map, I needed to convert the dataset into **GeoJSON** format, which is compatible with mapping libraries like **Leaflet**. The final goal was to create a webpage that shows aviation incidents on a map, so transforming the data into the right format was crucial.

**Setting up GeoJSON structure**: The first step was to structure the GeoJSON file with the necessary headers, ensuring the data was correctly organized for Leaflet.

```javascript
var geoJson = {
    type: "FeatureCollection",
    name: "CommercialAirCrashes",
    features: []
};
```

Populating features: For each row of data, I created a feature with the relevant properties. I made sure numerical values like coordinates were properly formatted and that all string values were correctly assigned.

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
            NumberOfEngines: r.data[i].NumberOfEngines,
            AirCraftCategory: r.data[i].AirCraftCategory,
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
Exporting to JSON: After formatting the data, I converted it into a JSON file, which can be easily loaded into a Leaflet map for visualization.

```javascript
const data = JSON.stringify(geoJson);
fs.writeFile("newnewData27.json", data, (err) => {
    if (err) {
        console.error('Error writing file:', err);
    } else {
        console.log("JSON data is saved.");
    }
});
```
The purpose of this entire process was to prepare the data for integration into a webpage. By converting the CSV data into GeoJSON format, I was able to visualize aviation incidents on a map using Leaflet. The webpage would allow users to interact with the data, providing detailed information about each incident directly on the map, bringing the aviation safety data to life.

Now that I have a clean and organized GeoJSON dataset, it looks like this:

```javascript
{
  "type": "FeatureCollection",
  "name": "CommercialAirCrashes",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "NtsbNo": "DCA24LA065",
        "EventDate": "2024-01-10T12:06:00Z",
        "Country": "United States",
        "City": "Houston",
        "State": "Texas",
        "AccidentLat": 29.990092,
        "AccidentLong": -95.340603,
        "AirportName": "",
        "AirportID": "",
        "Registration": "N62883",
        "FatalInjuryCount": "0",
        "SeriousInjuryCount": "0",
        "MinorInjuryCount": "0",
        "AirCarrier": "UNITED AIRLINES INC",
        "Make": "BOEING",
        "Model": "737",
        "NumberOfEngines": "",
        "AirCraftCategory": "AIR",
        "AirCraftDamage": "Substantial",
        "ProbableCause": "",
        "ObjectId": 0
      },
      "geometry": {
        "type": "Point",
        "coordinates": [
          -95.340603,
          29.990092
        ]
      }
    }
  ]
}
```

With this dataset in hand, my next step was to add the coordinates of the origin airport for each incident. To do this, I needed to find a comprehensive CSV containing airport codes for all airports in the United States. After locating this data, I was able to proceed with linking the airports to each incident.

The initial part of the code follows a familiar structure, similar to previous steps.

It starts by reading the CSV data and creating maps for airport codes and names. I also define a distance calculation variable that I thought would be useful later on, but ultimately, it ended up being unnecessary—a realization I had only after completing the process.

```javascript
let csvData = fs.readFileSync('airport-codes-updated.csv', 'utf8');
let records = Papa.parse(csvData, { header: true }).data;
let csvMap = new Map(records.map(row => [row.ident, { Lat: parseFloat(row.Lat), Long: parseFloat(row.Long) }]));
let csvMapName = new Map(records.map(row => [row.name, { Lat: parseFloat(row.Lat), Long: parseFloat(row.Long) }]));
```

Next, I loop through each feature in the data to match the airport ID or name with the records in the CSV file. Depending on what is available, I update the airport's latitude and longitude:

```javascript
data.features.forEach(feature => {
    let airportId = feature.properties.AirportID;
    let airportName = feature.properties.AirportName;

    if (csvMap.has(airportId)) {
        feature.properties.AirportLongitude = csvMap.get(airportId).Long;
        feature.properties.AirportLatitude = csvMap.get(airportId).Lat;
    } else if (csvMap.has('K' + airportId)) {
        feature.properties.AirportLongitude = csvMap.get('K' + airportId).Long;
        feature.properties.AirportLatitude = csvMap.get('K' + airportId).Lat;
    } else if (csvMap.has('P' + airportId)) {
        feature.properties.AirportLongitude = csvMap.get('P' + airportId).Long;
        feature.properties.AirportLatitude = csvMap.get('P' + airportId).Lat;
    } else if (csvMapName.has(airportName + ' Airport')) {
        feature.properties.AirportLongitude = csvMapName.get(airportName + ' Airport').Long;
        feature.properties.AirportLatitude = csvMapName.get(airportName + ' Airport').Lat;
    }
    // If airport information is missing, I default to using accident coordinates:
    else if (feature.properties.AirportName === "") {
        feature.properties.AirportLatitude = feature.properties.AccidentLatitude;
        feature.properties.AirportLongitude = feature.properties.AccidentLongitude;
    } else if (feature.properties.AirportID === "") {
        feature.properties.AirportLatitude = feature.properties.AccidentLatitude;
        feature.properties.AirportLongitude = feature.properties.AccidentLongitude;
    } else if (feature.properties.AccidentLat === "") {
        feature.properties.AccidentLat = feature.properties.AirportLatitude;
    } else if (feature.properties.AccidentLong === "") {
        feature.properties.AccidentLong = feature.properties.AirportLongitude;
    }

    // Calculate the distance (although I realized it wasn't needed):
    let distance = haversineDistance(
        feature.properties.Lat,
        feature.properties.Long,
        feature.properties.AirportLatitude,
        feature.properties.AirportLongitude
    );

    feature.properties.Distance = distance;
});
```

Finally, I exported the dataset to a new file with all the necessary information:

```javascript
fs.writeFileSync('newnewDatacord42.json', 'let data = ' + JSON.stringify(data, null, 2) + ';');
console.log('Updated data written to New File');
```

This gave me the complete dataset, now ready for the next steps in the process.


Leaflet Code:

My leaflet code is very simple. It is just an icon code plus two sets of Marker functions one for airports one for incident locations, a line function and legend.

```javascript
let map = L.map("map").setView([25, -90], 4);

L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
    maxZoom: 19,
    attribution:
        '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
}).addTo(map);

let crashIcon = L.icon({
    iconUrl: "Assets/airplane.png",
    iconSize: [30, 30],
});

let towerIcon = L.icon({
    iconUrl: "Assets/tower.png",
    iconSize: [30, 30],
});

L.geoJson(dataFinal, {
    pointToLayer: function (feature, latlng) {
        if (feature.geometry.coordinates[0] !== 0) {
            console.log(feature.geometry.coordinates[0]);
            let marker = L.marker(latlng, { icon: crashIcon });
            marker.bindPopup(
                "Date: " +
                feature.properties.EventDate +
                "<br/>" +
                "NtsbNo: " +
                feature.properties.NtsbNo +
                "<br/>" +
                "Make: " +
                feature.properties.Make +
                "<br/>" +
                "Model: " +
                feature.properties.Model +
                "<br/>" +
                "Dead: " +
                feature.properties.FatalInjuryCount +
                "<br/>" +
                "Serious: " +
                feature.properties.SeriousInjuryCount +
                "<br/>" +
                "Minor: " +
                feature.properties.MinorInjuryCount +
                "<br/>" +
                "ProbableCause: " +
                feature.properties.ProbableCause
            );
            return marker;
        } else {
            return null;
        }
    },
}).addTo(map);





L.geoJSON(dataFinal, {
    onEachFeature: function (feature, layer) {
        if (
            typeof feature.properties.AirportLatitude !== "undefined" &&
            feature.geometry.coordinates[0] !== 0
        ) {
            let marker = L.marker(
                [
                    feature.properties.AirportLatitude,
                    feature.properties.AirportLongitude,
                ],
                { icon: towerIcon }
            );
            marker.bindPopup(
                "Date: " +
                feature.properties.EventDate +
                "<br/>" +
                "Airport:Name: " +
                feature.properties.AirportName +
                "<br/>" +
                "Corresponding Accident: " +
                feature.properties.NtsbNo,


            );
            marker.addTo(map);
            var polyline = L.polyline(
                [
                    [
                        feature.properties.AirportLatitude,
                        feature.properties.AirportLongitude,
                    ],
                    feature.geometry.coordinates.reverse(),
                ],
                { color: "red" }
            ).addTo(map);
        } else {
            return null;
        }
    },
});

let legend = L.control({ position: "topright" });

legend.onAdd = function (map) {
    let div = L.DomUtil.create("div", "legend");
    div.style.backgroundColor = "white";
    div.style.padding = "10px";
    div.innerHTML = "Number of Serious Harmful Incidents Since 1982: " + dataFinal.features.length;
    return div;
};

legend.addTo(map);
```

My HTML code is very basic just referencing where I get my code and data from.
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="map.css">
    <meta charset="utf-8" />
    <title>Leaflet Map</title>
   
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
   <!-- <script src="Data.js" type="text/javascript"></script> -->
    <script src="DataFinal.js" type="text/javascript"></script>
</head>
<body>
    <div id="map" style="height: 1000px;"></div>

    <script src="MarkerCode.js"></script>
</body>
</html>
```
Kepler Process

In the Kepler process, I began by importing my geojson data and then plotting the points for each incident on the map. Each point is connected by arcs to the corresponding airports involved in the accidents. Additionally, I created a grid that visually displays the number of injuries for each incident, allowing for better insight into where the most serious events occurred.
Why This Data is Interesting

The dataset includes a total of 2,529 incidents from 1982 through March of this year, with 271 being classified as serious. A closer look reveals that most serious incidents tend to occur during critical phases of flight, such as landing, takeoff, or while at the airport. Interestingly, even in cases of significant damage to the aircraft, passengers often remain unharmed. When you consider the millions of flights that occur each year, these incidents are relatively rare.

Through my own research into aviation incidents, I have come to learn that some pilots and airlines may choose not to report incidents unless the damage is severe enough. This raises the question of how many incidents go unreported, a figure that remains uncertain.

Overall, the data shows that serious incidents are uncommon. However, in light of recent revelations regarding corporate negligence in airplane construction and maintenance, there is a growing awareness of dangerous practices within the industry. This newfound transparency is crucial because it provides an opportunity to eliminate these harmful practices, ensuring greater safety in the future.

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

