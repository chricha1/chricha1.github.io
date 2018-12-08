---
title: Lab 5
feature_image: "lab5_feature.png"
---

#### Chapter 8

1. The first_script.py script doesn’t check to see if the data layer is valid.
Modify first_script.py to implement this check.

```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

world_borders = iface.addVectorLayer('Z:/ges486/Lab_4/data/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
world_borders.isValid()

def load_layer():
    iface.addVectorLayer('Z:/ges486/Lab_4/data/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')

def change_color():
    active_layer = iface.activeLayer()
    renderer = active_layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(Qt.red))
    active_layer.triggerRepaint()
    iface.layerTreeView().refreshLayerSymbology(active_layer.id())

def open_attribute_table():
    iface.showAttributeTable(iface.activeLayer())
load_layer()
change_color()
open_attribute_table()
```

2. Modify the change_color method in the FirstScript class to accept a color value
instead of defaulting to Qt.red. Your change should allow specifying a color value
using named colors, RGBA values, and hex color notation.

```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

def load_layer():
    iface.addVectorLayer('Z:/ges486/Lab_4/data/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')

def change_color():
    active_layer = iface.activeLayer()
    renderer = active_layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(255,0,0,255))
    active_layer.triggerRepaint()
    iface.layerTreeView().refreshLayerSymbology(active_layer.id())

def open_attribute_table():
    iface.showAttributeTable(iface.activeLayer())
load_layer()
change_color()
open_attribute_table()
```

3. Modify the load_layer method in FirstScript to accept a user-specified layer name
and path instead of loading the world_borders layer.

```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

class FirstScript:
    def __init__(self,iface):
        self.iface = iface
    def load_layer(self,filename,layername):
        layer = self.iface.addVectorLayer(filename, layername, 'ogr')
        if not layer.isValid():
            print("Layer is invalid")
            exit()

def change_color_hex_name(self,color):
    print(color)
    active_layer = self.iface.activeLayer()
    renderer = active_layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(color))
    active_layer.triggerRepaint()
    self.iface.layerTreeView().refreshLayerSymbology(active_layer.id())

def change_color_rgba(self,color_r,color_g,color_b,color_a):
    print(color_r,color_g,color_b,color_a)
    active_layer = self.iface.activeLayer()
    renderer = active_layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(color_r,color_g,color_b,color_a))
    active_layer.triggerRepaint()
    self.iface.layerTreeView().refreshLayerSymbology(active_layer.id())

def open_attribute_table(self):
    self.iface.showAttributeTable(self.iface.activeLayer())
```

4. Create a new script to run in Script Runner with a
single method load_raster that loads the Natural Earth raster.

```python
from PyQt5.QtGui import QColor
from PyQt5.QtCore import Qt
from qgis.utils import iface

class FirstScript:
    def __init__(self, iface):
        self.iface = iface
    def load_raster(self):
        self.iface.addRasterLayer('Z:/ges486/Lab_4/data/NE1_50M_SR/NE1_50M_SR.tif', 'NE1_50M_SR')

def run_script(iface):
    print("creating object")
    fs = FirstScript(iface)
    print("loading layer")
    fs.load_raster()

run_script(iface)
```

Output:

![alt text](https://chricha1.github.io/Ch8Ex4.PNG)

#### Chapter 9

1. Find the qgis.utils module in your QGIS install and open it in a text editor.
Examine the methods and data structures available.

```python
help(qgis.utils)

# returns:
c:\progra~1\qgis3~1.2\apps\qgis\python\qgis\utils.py
```

![alt text](https://chricha1.github.io/Ch9Ex1.PNG)

![alt text](https://chricha1.github.io/Ch9Ex1-2.PNG)

2. Create a point memory layer with an id and name field,
add some features to it, and add it to the map canvas.

```python
mem_layer = QgsVectorLayer("Point?crs=epsg:4326&field=id:integer" "&field=road_name:string&index=yes", "Points", "memory")

QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
feature = QgsFeature()
point = QgsPointXY(3, 27)
feature.setGeometry(QgsGeometry.fromPointXY(point))
feature.setAttributes([1, 'QGIS Point'])
mem_layer.addFeature(feature)
mem_layer.commitChanges()
```

Output:
![alt text](https://chricha1.github.io/Ch9Ex2.PNG)

3. Write a script to turn on labeling for the point layer you created
and label each feature using the name field.

```python
from qgis.PyQt.QtCore import QVariant
mem_layer = QgsVectorLayer("Point?crs=epsg:4326&field=id:integer" "&field=road_name:string&index=yes", "Points", "memory")
QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
feature = QgsFeature()

point = QgsPointXY(3, 27)
feature.setGeometry(QgsGeometry.fromPointXY(point))
feature.setAttributes([1, 'QGIS Point'])

mem_layer.addFeature(feature)
mem_layer.commitChanges()

label = QgsPalLayerSettings()
label.enabled = True
label.fieldName = "Name"
label.placement = QgsPalLayerSettings.AroundPoint
label.setDataDefined(QgsPalLayerSettings.Size,True,True,'8',"")
label.writeToLayer(mem_layer)
QgsMapLayerRegistry.instance().addMapLayers(mem_layer)

# could not get label to appear
```

4. Using the point layer, write a script that allows you to edit
the name for a selected feature by prompting for the new name,
then saving it to the attribute table.

```python
from qgis.PyQt.QtCore import QVariant
from PyQt5 import QtGui
from PyQt5.QtGui import *

layer = iface.activeLayer()

qid = QInputDialog()
text, ok = QInputDialog.getText(qid, title, label, mode, default)
label = "Name: "
mode = QLineEdit.Normal

layer.addFeature(feature)
layer.commitChanges()

text = fields.at(field).name()
layer.renameAttribute(text, newName)

#simply printing text yields a string and a boolean, but we only want a string
print text[0]
```
