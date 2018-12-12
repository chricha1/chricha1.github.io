---
title: Project 1
feature_image: "project1_feature.png"
---

#### Exploring the Effect of Art Tax Credit on Baltimore City Ground Rent
Baltimore City has three Arts & Entertainment (A&E) Districts: Bromo Seltzer, Highlandtown, and Station North. Artists or A&E enterprises may receive a 10-year property tax credit for renovated buildings that provide space for artists to live and work. The property tax credit is prorated to reflect the proportion of a renovated building and only applies to improvements made to the property. Property owners renovating live-work spaces in an A&E district can contact the MD State Department of Assessments and Taxation to determine the building’s eligibility. Within 90 days following receipt of a tax assessment, property owners must file a tax credit application with the City’s Department of Finance. Property owners must annually re-certify that the building is being used in compliance with the property tax credit.

#### Procedure
1. I changed the projection to WGS 84 Pseudo-Mercator.
2. I added the Real Property shapefile, using a graduated colors symbology based on Ground Rent for Map 1 and based on Art Tax Base for Map 2.  I also added a shapefile of Baltimore City's neighborhood boundaries (as of the year 2010). The data was found on Open Baltimore and provided by MOIT - GIS.
3. I used the Centroids algorithm, which created a new layer of points representing the centroid of the geometries in an input layer, in order to make a 3D map for Ground Rent (map 1) and summarize density with a hexagonal grid for Art Tax Base (map 2).
4. I used IDW Interpolation to create a raster for the Ground Rent 3D map.
5. I used Clip Raster with Polygon, then used this clipped layer for the "elevation" in the 3D Configuration window. I also used a vertical scale of 0.25 and tile resolution of 100 px, which looked the best for visualizing the Ground Rent Data.

[![Alt Text]](https://github.com/chricha1/chricha1.github.io/blob/master/Project1/3D.PNG)

#### Conclusions
I found the highest ground rent to be around the inner city.
