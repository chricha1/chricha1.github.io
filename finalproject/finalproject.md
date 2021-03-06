---
title: Final Project
feature_image: "final_feature.png"
---

This project aims to shed light on how creative placemaking can impact public safety outcomes in Baltimore City.

Public safety refers to the welfare and protection of the general public, and strives
towards a vibrant community where “people feel free of threats to their persons and
property.”

Creative placemaking is an emerging form of participatory art-making, given increasing attention by
scholars, practitioners, policymakers, and funders over the past decade. Creative placemaking adds
dimensions of art and creative practice to the placemaking field, promoting the belief that
community development should be holistic and human-centered (Bennett 2014). In practice, creative placemaking combines the field of
planning with community relationship-building; it places a high value on streetscapes and is designed to improve economic outcomes by
utilizing undervalued resources and developing strong social networks through artistic practice (Stern 2014).

Projects at the intersection of creative placemaking and public safety fall into five primary
types of activities: projects that promote empathy and understanding, projects that influence
law and policy, projects that provide career opportunities, projects that support well-being, and
projects that advance quality of place.

My final project for GES 486 was inspired by a 2017 report by the Social Impact of the Arts Project (SIAP) at the University of
Pennsylvania. The results of the three-year study showed how cultural resources are significantly linked to better health, schooling,
and security in New York City's lower-income neighborhoods. I performed a similar preliminary analysis on Baltimore City's
neighborhoods, arts organizations (such as museums and dance studios), and violent crimes (specifically homicides and shootings).

### Process

Question: Does the presence of art organizations affect crime rates in Baltimore City?

The first thing I had to do was gather [crime data](https://data.baltimorecity.gov/Public-Safety/BPD-Part-1-Victim-Based-Crime-Data/wsfq-mvij/data) for Baltimore City.
I edited the [original 2014 Crimes .csv file](https://data.baltimorecity.gov/Public-Safety/BPD-Part-1-Victim-Based-Crime-Data/wsfq-mvij/data) to separate addresses and coordinates (https://trumpexcel.com/split-multiple-lines/). Then I added an empty column before
“Crime Date” → =TEXT(B1,"yyyymmdd") which would order all crimes by year, month, then date so that I could later select only 2014 crimes using SQL.

I also edited the [original Art Organizations file](https://data.baltimorecity.gov/Culture-Arts/Baltimore-Arts-Organizations/r4ur-u5nm) to get [coordinates](http://www.gpsvisualizer.com/geocoder/) of each arts organization.

Once I had all homicides and shootings that occurred in Baltimore City in 2014, I used Python to select and count these specific crimes
by neighborhood. I also used [neighborhood census data](https://data.baltimorecity.gov/Neighborhoods/2010-Census-Neighborhoods/r3qj-2ifh) to take into account the population in each neighborhood.

I used Python to count number of arts organizations in each neighborhood. I added 2 new columns in the Neighborhoods 2010 shapefile: count_crimes and count_art in order to perform Moran's I analysis later.

```python
lyrPts = iface.addVectorLayer("Z:/ges486/final_proj/all2014homi_shoot.shp", "Crimes", "ogr")
selection = lyrPts.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"Neighborho" = \'Brooklyn\''))
lyrPts.selectByIds([s.id() for s in selection])
```
![Select](step1.PNG "step1.PNG")
<small>__Figure 1__:  Orange points represent 2014 homicides and shootings, white points represent arts organizations, and yellow points
are selected points in each neighborhood.

I used [Wikimedia Map](https://wiki.openstreetmap.org/wiki/Tile_servers) for the basemap.

I used Kernel Density Estimation to create a density (heatmap) raster. First, I projected all layers to EPSG:2248 -
NAD83/Maryland(ftUS). Then before running the heatmap builder, I increased the radius to 5000 feet and decreased number of rows to 500. For the final step, I made sure to Clip raster by mask layer (input layer: heatmap, mask layer: neighborhoods).

![Heatmap](map1.PNG "map1.PNG")
<small>__Figure 2__:  Heatmap with radius of 5000 feet.

![3D Heatmap](3Dreal2.PNG "3Dreal2.PNG")

<small>__Figure 3__:  3D View of Heatmap, using a vertical scale of 60 and tile resolution of 200.

### Findings

To get a better look at how presence of arts organizations and occurrence of homicides/shootings were spatially correlated with each
other, I ran a Bivariate Moran’s I analysis. 

Bivariate Local Moran's I:

![Moran's I step 1](morani1.PNG "morani1.PNG")

Cluster Map:

![Moran's I step 2](morani2-1.png "morani2-1.png")

Moran's Scatter Plot:

![Moran's I step 2](morani2-2.png "morani2-2.png")

Regression Report:

![Regression Report](report.PNG "report.PNG")

The results show that there is a slight negative correlation.

### Future Research
I would like to use spatial statistics to show percentages of decrease in serious crime rate, and furthermore the percentages of
decrease in cases of child abuse/neglect and increase in kids scoring in the top stratum on English and math exams.

__Author:__ Christine Chang

__Languages:__ Markdown, Python, SQL

__Applications:__ QGIS, GeoDa

__Data Sources:__ All data is from [Open Baltimore](https://data.baltimorecity.gov/).

[Arts Organizations](https://data.baltimorecity.gov/Culture-Arts/Baltimore-Arts-Organizations/r4ur-u5nm), [All Crimes 2012-2018](https://data.baltimorecity.gov/Public-Safety/BPD-Part-1-Victim-Based-Crime-Data/wsfq-mvij/data), [Neighborhood Boundaries 2010](https://data.baltimorecity.gov/Neighborhoods/Neighborhoods-Shape/ysi8-7icr).
