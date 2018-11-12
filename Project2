### Project 2

##### Data Analysis
```python
MdCounties = QgsVectorLayer('Z:/ges486/Project_2/MD_AtlasHCB/MD_Historical_Counties/MD_Historical_Counties.shp', 'Historical_Counties', 'ogr')
MdCounties.isValid()
# should return True
QgsProject.instance().addMapLayer(MdCounties)

TP1 = MdCounties.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"START_N" = 16380124')
MdCounties.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()
# should add NCA_1 and ST. MARYS

TP2 = MdCounties.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"START_N" >= 16851113 and "END_N" < 17891229')
MdCounties.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()
# should add NCA_1, ANNE ARUNDEL, BALTIMORE, CECIL, KENT, TALBOT, DORCHESTER, SOMERSET, CHARLES, CALVERT, ST MARYS
```

##### Animated Map
![alt text](https://chricha1.github.io/MDcounties.gif)

##### Description

This map presents data about the creation and all
subsequent changes (marked with the date) in the
size, shape, and location of every county in the
state of Maryland. County boundaries changed often within the past 4 centuries.
Counties are important because nearly every aspect of American life
can be described, analyzed, and illuminated through data
gathered and organized by county or available in county records.

Furthermore, county governments in the United States function as local
administrative arms within the states. All states except Connecticut and
Rhode Island have functioning county governments. Starting in the colonial period,
county functions expanded from legal proceedings and law enforcement
to probating wills, recording deeds, and providing courts for civil actions.
Naturally, recording marriages, births, and deaths was added.
Eventually most of the work of census-taking was organized around the county.

##### Procedure

Data for this map were obtained from the Atlas of Historical County Boundaries.
Map design and data analysis were completed by Christine Chang.

Time Period 1:
![alt text](https://chricha1.github.io/TP1.png)

Time Period 2:
![alt text](https://chricha1.github.io/TP2.png)

Time Period 3:
![alt text](https://chricha1.github.io/TP3.png)

Time Period 4:
![alt text](https://chricha1.github.io/TP4.png)

Time Period 5:
![alt text](https://chricha1.github.io/TP5.png)
