---
title: Lab 6
feature_image: "lab6_feature.png"
---

#### Process

1 . Created a Queen contiguity weight based on the ID variable
"OBJECTID" (instead of "CSA2010" because it is a string) in the
"Vital_Signs_16_Arts_and_Culture" shapefile.

![alt text](https://chricha1.github.io/Fig2-1.PNG)

2 . Ran a regression report to observe the correlation between
"cebus16" (Number of Businesses that are Arts-Related
per 1000 Residents) and "libcard16" (Number of Persons with
Library Cards per 1,000 Residents).

I compared the probability of Lagrange Multiplier (lag)
with the probability of Lagrange Multiplier (error). Both were
significant (p < 0.05), but LM (error) was more significant
than LM (lag).

![alt text](https://chricha1.github.io/Part2Fig2.PNG)

I found that the Moran's I was a positive number so that means
there is a correlation between the number of persons with library cards
and the number of art-related businesses.

3 . Created the Bivariate Local Moran's I map.

![alt text](https://chricha1.github.io/Part2Fig3.PNG)

#### Findings

The high-high (dark red) Downtown, Mount Vernon, and Charles Village neighborhoods
are bordered by neighborhoods with low numbers that are not significant enough
to cluster and split into low and high numbers when compared with the
rest of Baltimore City.

The low-high (light blue) neighborhoods have low numbers but are bordered by
neighborhoods with high numbers.
