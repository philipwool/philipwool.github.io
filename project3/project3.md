# __Project 3__

![alt text](https://philipwool.github.io/project3/Drone2.gif)

![alt text](https://philipwool.github.io/project3/Patapsco_3D.png)

![alt text](https://philipwool.github.io/project3/Aligned.PNG)

![alt text](https://philipwool.github.io/project3/SPC.PNG)

![alt text](https://philipwool.github.io/project3/DPC.PNG)

![alt text](https://philipwool.github.io/project3/DPCzoom.PNG)

![alt text](https://philipwool.github.io/project3/DPCzoom2.PNG)

![alt text](https://philipwool.github.io/project3/DPCzoom3.PNG)

![alt text](https://philipwool.github.io/project3/Groundpts.PNG)

![alt text](https://philipwool.github.io/project3/DEM.PNG)

![alt text](https://philipwool.github.io/project3/DEMzoom.PNG)

![alt text](https://philipwool.github.io/project3/DEMzoom2.PNG)

![alt text](https://philipwool.github.io/project3/Ortho.PNG)

![alt text](https://philipwool.github.io/project3/Orthozoom.PNG)

![alt text](https://philipwool.github.io/project3/Channel_DEM_Complete.png)

![alt text](https://philipwool.github.io/project3/Values_to_Points.PNG)

```python
#Add Patapsco Raster

Patapsco = QgsRasterLayer('Z:/GES486/Project_3/Shapefiles/Patapsco_DEM.tif', 'Patapsco')
Patapsco.isValid()
QgsProject.instance().addMapLayer(Patapsco)



#Add MGS Points, change to red, update layer tree

MGS_Points = QgsVectorLayer('Z:/GES486/Project_3/Shapefiles/MGS_Points.shp', 'MGS_Points')
MGS_Points.isValid()
QgsProject.instance().addMapLayer(MGS_Points)

renderer = MGS_Points.renderer()
renderer
#Should return "<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>"
symbol = renderer.symbol()
symbol.dump()
#Should return 'FILL SYMBOL (1 layers) color 152,125,183,255'
symbol.setColor(Qt.blue)
MGS_Points.triggerRepaint()

layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(MGS_Points.id())




#Perform comparison betw raster and MGS points in Arcmap


#Add DEMError points, choose good points with SQL, Save as new shapefile, Bring in as Green

MarchDEMError = QgsVectorLayer('Z:/GES486/Project_3/Shapefiles/MarchDEMError.shp', 'MarchDEMError')
MarchDEMError.isValid()
QgsProject.instance().addMapLayer(MarchDEMError)

renderer = MarchDEMError.renderer()
renderer
#Should return "<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>"
symbol = renderer.symbol()
symbol.dump()
#Should return 'FILL SYMBOL (1 layers) color 152,125,183,255'
symbol.setColor(Qt.red)
MarchDEMError.triggerRepaint()

layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(MarchDEMError.id())

#Select good points

selection = MarchDEMError.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"DEMerror" >= -1 and "DEMerror" <= 1'))
MarchDEMError.selectByIds([s.id() for s in selection])
iface.mapCanvas().zoomToSelected()

QgsVectorFileWriter.writeAsVectorFormat(MarchDEMError, r'Z:/GES486/Project_3/Shapefiles/MarchDEM_Good.gpkg', 'utf-8', MarchDEMError.crs(),'GPKG', True)

MarchDEM_Good = QgsVectorLayer('Z:/GES486/Project_3/Shapefiles/MarchDEM_Good.gpkg', 'MarchDEM_Good')
MarchDEM_Good.isValid()
# Should Return "True"
QgsProject.instance().addMapLayer(MarchDEM_Good)

renderer = MarchDEM_Good.renderer()
renderer
#Should return "<qgis._core.QgsSingleSymbolRenderer object at 0x000001F6CBC06DC8>"
symbol = renderer.symbol()
symbol.dump()
#Should return 'FILL SYMBOL (1 layers) color 152,125,183,255'
symbol.setColor(Qt.green)
MarchDEM_Good.triggerRepaint()

layer_tree = iface.layerTreeView()
layer_tree.refreshLayerSymbology(MarchDEM_Good.id())
```

![alt text](https://philipwool.github.io/project3/Transect_Exam.JPG)

![alt text](https://philipwool.github.io/project3/Transect_Eval.JPG)

![alt text](https://philipwool.github.io/project3/Transect_Eval.gif)

![alt text](https://philipwool.github.io/project3/Transect_Eval2.gif)

![alt text](https://philipwool.github.io/project3/Channel_3D2.JPG)

