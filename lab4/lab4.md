## Part 1
#### Figure 7.5:

Code:
```python
>>> wb = QgsVectorLayer('Z:/ges486/Lab_4/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
>>> wb.isValid()
True
>>> QgsProject.instance().addMapLayer(wb)
<qgis._core.QgsVectorLayer object at 0x00000294897A1F78>
```
Output:

![alt text](https://chricha1.github.io/Figure7.5.PNG)


#### Exercises in 7.7

1. Add the World_Borders layer to the map canvas
```python
>>> wb = iface.addVectorLayer('Z:/GES486/lab_4/data/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
```

2. Change the color to green with 50% Transparency
```python
>>> renderer = wb.renderer()
>>> renderer
<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>
>>> symbol = renderer.symbol()
>>> symbol.dump()
FILL SYMBOL (1 layers) color 152,125,183,255
>>> symbol.setColor(QColor(0,255,0,127))
>>> wb.triggerRepaint()
```

3. Update the layer and legend
```python
>>> layer_tree = iface.layerTreeView()
>>> layer_tree.refreshLayerSymbology(wb.id())
```

## Part 2
#### Loading a vector layer from a file sample:

Code:
```python
>>> layer = QgsVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "New York City Museums", "ogr")
>>> layer.isValid()
True
>>> QgsProject.instance().addMapLayer(layer)
<qgis._core.QgsVectorLayer object at 0x0000019EF111DB88>

```

Output:
![alt text](https://chricha1.github.io/VectorFromFile.PNG)

#### Examining vector layer features:

Code:
```python
>>> layer = QgsVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "New York City Museums", "ogr")
>>> features = layer.getFeatures()
>>> f = next(features)
>>> g = f.geometry()
>>> g.asPoint()
```

Ouput:
```python
<QgsPointXY: POINT(-74.01375579573735308 40.70381655004537436)>
```

#### Examining vector layer attributes:

Code:
```python
>>> layer = QgsVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "New York City Museums", "ogr")
>>> features = layer.getFeatures()
>>> f = next(features)
>>> f.attributes()
```

Output:
```python
['Alexander Hamilton U.S. Custom House', '(212) 514-3700', 'http://www.oldnycustomhouse.gov/', '1 Bowling Grn', NULL, 'New York', 10004.0]
```

###### There's more...

```python
>>> [c.name() for c in f.fields().toList()]
['NAME', 'TEL', 'URL', 'ADRESS1', 'ADDRESS2', 'CITY', 'ZIP']
```

#### Filtering a layer by geometry:
- Select a subset of a point layer based on the points contained in an overlapping polygon layer:
```python
lyrPts = QgsVectorLayer("Z:/ges486/Lab_4/data/MSCities_Geo_Pts.shp", "MSCities_Geo_Pts", "ogr")
lyrPoly = QgsVectorLayer("Z:/ges486/Lab_4/data/GIS_CensusTract_poly.shp", "GIS_CensusTract_poly", "ogr")
QgsProject.instance().addMapLayers([lyrPts,lyrPoly])
ftsPoly = lyrPoly.getFeatures()
for feat in ftsPoly:
    geomPoly = feat.geometry()
    featsPnt = lyrPts.getFeatures(QgsFeatureRequest().setFilterRect(geomPoly.boundingBox()))
    for featPnt in featsPnt:
        if featPnt.geometry().within(geomPoly):
            print (featPnt.id())
            lyrPts.select(featPnt.id())
iface.setActiveLayer(lyrPoly)
iface.zoomToActiveLayer()
```

Output:
![alt text](https://chricha1.github.io/Filter1.PNG)

- Subset a layer by its attributes:
```python
>>> lyrPts = iface.addVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "Museums", ogr")
>>> selection = lyrPts.getFeatures(QgsFeatureRequest()set.FilterExpression(u'"ZIP" = 10002'))
>>> lyrPts.selectByIds([s.id() for s in selection])
```

Output:
![alt text](https://chricha1.github.io/Filter2.PNG)

#### Buffering a feature intermediate:

Code:
```python
lyr = QgsVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "Museums", "ogr")
QgsProject.instance().addMapLayers([lyr])
fts = lyr.getFeatures()
ft = next(fts)
lyr.selectByIds([ft.id()])
buff = ft.geometry().buffer(.2,8)
buffLyr = QgsVectorLayer('Polygon?crs=EPSG:4326', 'Buffer' , 'memory')
pr = buffLyr.dataProvider()
b = QgsFeature()
b.setGeometry(buff)
pr.addFeatures([b])
buffLyr.updateExtents()
buffLyr.setOpacity(0.3)
QgsProject.instance().addMapLayers([buffLyr])
```
Output:
![alt text](https://chricha1.github.io/Buffer1.PNG)

#### Measuring the distance between two points:

Code:
```python
import qgis.core
lyr = QgsVectorLayer("Z:ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "Museums", "ogr")
fts = lyr.getFeatures()
first = next(fts)
last = next(fts)
for f in fts:
    last = f
d = QgsDistanceArea()
m = dist.measureLine(first.geometry().asPoint(), last.geometry().asPoint())
x = d.convertLengthMeasurement(m, 0)
print(x)
```

Output:
```python
4401.1622240174165
```

#### Measuring the distance along a line sample:

Code:
```python
>>> import qgis.core
>>> lyr = QgsVectorLayer("Z:/ges486/Lab_4/data/paths/paths.shp", "Route", "ogr")
>>> fts = lyr.getFeatures()
>>> route = next(fts)
>>> dist = QgsDistanceArea()
>>> d.willUseEllipsoid
>>> e = QgsEllipse
>>> m = d.measureLine(route.geometry().asPolyline())
>>> x = d.convertLengthMeasurement(QgsUnitTypes.DistanceMeters, QgsUnitTypes.DistanceNauticalMiles)
>>> print(x)

# setEllipsoidalMode() was removed in QGIS 3.0

```

#### Calculating the area of a polygon:

Code:
```python
>>> import qgis.core
>>> lyr = QgsVectorLayer("Z:/ges486/Lab_4/data/mississippi.shp", "Mississippi", "ogr")
>>> fts = lyr.getFeatures()
>>> boundary = next(fts)
>>> dist = QgsDistanceArea()
>>> m = d.measureArea(boundary.geometry())

# convertMeasurement was removed.
```

Output:

![alt text](https://chricha1.github.io/PolygonArea.PNG)


#### Creating a spatial index:
```python
lyr = QgsVectorLayer("Z:/ges486/Lab_4/data/NYC_MUSEUMS_GEO.shp", "Museums", "ogr")
fts = lyr.getFeatures()
first = next(fts)
index = QgsSpatialIndex()
index.insertFeature(first)
    True
for f in fts:
    index.insertFeature(f)
hood = index.nearestNeighbor(first.geometry().asPoint(), 4)
print(hood)
#
```

Output:
```python
[0, 79, 33, 105]
```
