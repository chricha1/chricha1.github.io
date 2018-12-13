---
title: Final Project
feature_image: ""
---

#### Process
Question: Does the presence of art organizations affect crime rates in Baltimore City?

```python
lyrPts = iface.addVectorLayer("Z:/ges486/final_proj/all2014homi_shoot.shp", "Crimes", "ogr")
selection = lyrPts.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"Neighborho" = \'Beechfield\''))
lyrPts.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()
```


![Heatmap](heatmapreal.PNG "heatmapreal.PNG")

* Added delimted text layer
* Used Wikimedia Map for basemap

![3D Heatmap](3Dreal1.PNG "3Dreal1.PNG")

#### Data

#### Tools Used

#### Findings

![Moran's I step 1](morani1.PNG "morani1.PNG")

![Moran's I step 2](morani2.PNG "morani2.PNG")

#### Future Research

