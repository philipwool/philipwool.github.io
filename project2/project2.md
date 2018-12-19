---
title: Project 2
---

#### __Objective__

To create a map that shows commercial development in Baltimore, MD over the last
century, both spatially and temporally.

#### __Process__

* Using the Real_Property dataset I wrote a python code designed to:

  1. Add in the Real_Property Layer

  2. Change the fill color to gray

  3. Update the layer tree

  4. perform a selection commercial lots present during the desired time period in twenty year increments.

  5. Save this selection to file as a new Shapefiles

  6. Add the new shapefile to the map.

* __That code is as follows:__


```python
Real_Property = QgsVectorLayer('C:/Users/ges_student/Desktop/Project_2/Shapefiles/Real_Property_Proj.gpkg', 'Real_Property')
Real_Property.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(Real_Property)
# Should return "<qgis._core.QgsVectorLayer object at 0x000001714E5500D8>"

renderer = Real_Property.renderer()
renderer
#Should return "<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>"
symbol = renderer.symbol()
symbol.dump()
#Should return 'FILL SYMBOL (1 layers) color 152,125,183,255'
symbol.setColor(Qt.gray)
Real_Property.triggerRepaint()

layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(Real_Property.id())

selection = Real_Property.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"YEAR_BUILD" >= 1900 and "YEAR_BUILD" <= 2018 and "USEGROUP" = \'C\''))
Real_Property.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()

QgsVectorFileWriter.writeAsVectorFormat(Real_Property, r'C:/Users/ges_student/Desktop/Project_2/Shapefiles/Comm_Poly_Test2.gpkg', 'utf-8', Real_Property.crs(),'GPKG', True)

Comm_Poly_Test2 = QgsVectorLayer('C:/Users/ges_student/Desktop/Project_2/Shapefiles/Comm_Poly_Test2.gpkg', 'Real_Property')
Comm_Poly_Test2.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(Comm_Poly_Test2)
```

* __The individual components of the code are shown below:__


1. Add in the Real_Property Layer

```python
Real_Property = QgsVectorLayer('C:/Users/ges_student/Desktop/Project_2/Shapefiles/Real_Property_Proj.gpkg', 'Real_Property')
Real_Property.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(Real_Property)
# Should return "<qgis._core.QgsVectorLayer object at 0x000001714E5500D8>"
```

2. Change the fill color to gray

```python
renderer = Real_Property.renderer()
renderer
#Should return "<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>"
symbol = renderer.symbol()
symbol.dump()
#Should return 'FILL SYMBOL (1 layers) color 152,125,183,255'
symbol.setColor(Qt.gray)
Real_Property.triggerRepaint()
```

3. Update the layer tree

```python
layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(Real_Property.id())
```

4. perform a selection commercial lots present during the desired time period in twenty year increments.

```python
selection = Real_Property.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"YEAR_BUILD" >= 1900 and "YEAR_BUILD" <= 2018 and "USEGROUP" = \'C\''))
Real_Property.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()
```

__Script Selection__
![alt text](https://philipwool.github.io/project2/Script_Selection.JPG)

5. Save this selection to file as a new Shapefiles

```python
QgsVectorFileWriter.writeAsVectorFormat(Real_Property, r'C:/Users/ges_student/Desktop/Project_2/Shapefiles/Comm_Poly_Test2.gpkg', 'utf-8', Real_Property.crs(),'GPKG', True)
```

6. Add the new shapefile to the map.

```python
Comm_Poly_Test2 = QgsVectorLayer('C:/Users/ges_student/Desktop/Project_2/Shapefiles/Comm_Poly_Test2.gpkg', 'Real_Property')
Comm_Poly_Test2.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(Comm_Poly_Test2)
```

__New Layer Addition__
![alt text](https://philipwool.github.io/project2/Layer_Addition.JPG)

* From this layer I also created centroids of each polygon.

* Next I performed a kernel analysis resulting a heatmap of commercial development for each time period.

#### __Results__

* By creating shapefiles for commercial properties in twenty year increments and
overlaying them on top of the Real_Property Layer, I was able to make a map that
displays not only the spatial pattern of commercial development, but also the
temporal pattern by assigning a graduated red to yellow scale in which older commercial
properties are red, newer properties in yellow.

* From this, I was able to use Adobe Photoshop to create a GIF that animates the
development process over time and space in Baltimore.

![alt text](https://philipwool.github.io/project2/Comm_Map.gif)

* To create a three-dimensional view of this process, I used these same shapefiles
to similarly create an animated GIF of the same commercial development patterns
in QGIS 3D map view, using a Baltimore elevation data as the base raster.

![alt text](https://philipwool.github.io/project2/3d_Comm.gif)

* Lastly, as a unique and different way of visualizing commercial development,
both spatially and temporally, I used the heatmaps created by the kernel
analysis in QGIS 3D map view and selected them as the elevation raster to be used.
* This essentially results in displaying commercial density as elevation in the
three-dimensional view.

![alt text](https://philipwool.github.io/project2/3D_Heatmap.gif)

