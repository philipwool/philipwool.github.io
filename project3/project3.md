---
title: Project 3
feature_image: "Bloede_Pano.jpg"
feature_text: |
  ## Bloede Dam Removal Analysis
  Using Structure From Motion to model changes in channel morphology.
  
---

The removal of the Bloede Dam on the Patapsco river provides a unique opportunity to model phenomena such as the release of large amounts of previously impounded sediment, and morphologic changes caused a completely new set of upstream flow conditions.

This particular project has several objectives, of which the first is to create a digital elevation model (DEM) of the entire Patapsco study area using structure from motion (SFM). This area includes the dam pond upstream of the Bloede dam, and reaches all the way down to the lower floodplain. The second component of this project is to compare the digital elevation values developed using SFM to those associated with Maryland Geological Survey (MGS) transects to assess the accuracy of the model. In the long term, if these techniques for creating DEMs prove to be accurate, they can be used to monitor and model characteristics of dam removal such as the evacuation and deposition of sediment that was impounded behind the dam, as well as changes to channel morphology. When compared to traditional methods, SFM offers the opportunity to observe these phenomena over the entire stream reach rather than using transect data to interpolate conditions over what can be a substantial unobserved area.

![alt text](https://philipwool.github.io/project3/Drone2.gif)

![alt text](https://philipwool.github.io/project3/Patapsco_3D.png)

In order to achieve this, aerial drone imagery was first loaded into Agisoft Photoscan. 

![alt text](https://philipwool.github.io/project3/Aligned.PNG)

The imagery is assessed for quality and aligned in order to create a sparse point cloud.  Known ground control points (GCPs) are added to the sparse point cloud and identified in the constituent images. A process known as gradual selection is applied to help identify and eliminate any points in the sparse point cloud that do not meet standards of accuracy.

![alt text](https://philipwool.github.io/project3/SPC.PNG)

This is an important step as the sparse point cloud is the foundation on which the dense point cloud (DPC) is built.

__Dense Point Clouds__
![alt text](https://philipwool.github.io/project3/DPC.PNG)

__They are Capable of modeling bathymetric features in shallow water...__
![alt text](https://philipwool.github.io/project3/DPCzoom.PNG)

__...providing unique views in a three-dimensional environment...__
![alt text](https://philipwool.github.io/project3/DPCzoom2.PNG)

__...and capturing a suprising level of detail.__
![alt text](https://philipwool.github.io/project3/DPCzoom3.PNG)

Once a DPC is built, groundpoints are classified and seperatated from other data points.

![alt text](https://philipwool.github.io/project3/Groundpts.PNG)

From these ground points, a georeferenced DEM can be built.

__Digital Elevation Model Images__
![alt text](https://philipwool.github.io/project3/DEM.PNG)

These DEMs can capture extremely detailed bathymetric features such as depositional sand bars.

![alt text](https://philipwool.github.io/project3/DEMzoom.PNG)

![alt text](https://philipwool.github.io/project3/DEMzoom2.PNG)

We can also create georeferenced orthomosaics of all the contributing photos.

![alt text](https://philipwool.github.io/project3/Ortho.PNG)

![alt text](https://philipwool.github.io/project3/Orthozoom.PNG)

After the DEM is built, it can be brought into Arcmap in order to perform error analysis. In addition to the channel DEM, the MGS transect shapefile is brought in, and the Values to Points tool is used to create a new point shapefile, with identical x,y values, but with an additional column of elevation (z) values in its attribute table. Using the Field Calculator tool it is possible to create a new column of values that quantify the difference between the MGS transect elevation values and the DEM elevation values, essentially characterizing the error on the model.

![alt text](https://philipwool.github.io/project3/Channel_DEM_Complete.png)

![alt text](https://philipwool.github.io/project3/Values_to_Points.PNG)

The next part of the analysis is done in QGIS. Using a Python script, the DEM is brought in, as well as the MGS transect points, which are displayed in red. Additionally, within Python an SQL query is performed in order to create a selection of points that lie within an acceptable margin of error, in this case one foot. The script then proceeds to write the selection to file as a new shapefile, add this new shapefile to the map, and display the new points in green.

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
__Initial Transect Points__
![alt text](https://philipwool.github.io/project3/Transect_Exam.JPG)

__Points in green are withing one foot of elevation values reported by MGS transect point values__
![alt text](https://philipwool.github.io/project3/Transect_Eval.JPG)

![alt text](https://philipwool.github.io/project3/Transect_Eval.gif)

![alt text](https://philipwool.github.io/project3/Transect_Eval2.gif)

This DEM can then be used as the Raster layer in 3D Viewer to create a three-dimensional map of the entire stream reach.

![alt text](https://philipwool.github.io/project3/Channel_3D2.JPG)


# __Why do this?__


The Patapsco river and its surrounding areas produce some of the flashiest watersheds in the US. This technology would have been ideally suited to study such a highly variable channel for that reason alone.

The following images were taken in March and July respectively, pre and post 2018 Ellicott City Flood storm event. An event of this maginitude can cause substantial morphologic change in the channel, as evidenced below. Structure From Motion can capture these changes.

__Analysis of Transect__
![alt text](https://philipwool.github.io/project3/Upstream_Via.PNG)

__Sand Bars__
![alt text](https://philipwool.github.io/project3/March_UpstreamVia_Ortho_Highlight.jpg)

__Sand Bar Modeled in DEM__
![alt text](https://philipwool.github.io/project3/March_Leaf_Off_Highlight.png)

__Bathymetry Alteration, Bars Buried Under Sediment__
![alt text](https://philipwool.github.io/project3/July_UpstreamVia_DEM.jpg)

__Deposition of sediment and alteration of channel can be seen__
![alt text](https://philipwool.github.io/project3/July_Leaf_On_Highlight.png)

__Considerable Bank Erosion__
![alt text](https://philipwool.github.io/project3/July_UpstreamVia_Ortho_Highlight.jpg)

__Stream Profile, Pre and Post Ellicott City 2018 Flood__
![alt text](https://philipwool.github.io/project3/Pre_Flood.PNG)
![alt text](https://philipwool.github.io/project3/March_And_July.PNG)



# __More importantly...__



![alt text](https://philipwool.github.io/project3/Bloede_Demo.jpg)


<iframe width="560" height="315" src="https://www.youtube.com/embed/nINVNlcLoeo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


The removal of the Bloede dam takes alterations to flow patterns and sediment budgets to an unparalleled level. With structure from motion we can sense and model changes in channel morphology over the entire stream reach, rather than relying on widely spread and infrequent transect data.

__This photo was taken by me immediately following the breach__
![alt text](https://philipwool.github.io/project3/Bloede_Demo2.jpg)

It is evident from this image that substantial change has occurred in the section of the stream that was formerly the dam pond.

![alt text](https://philipwool.github.io/project3/Before_After.JPG)

This removal evacuated huge amounts of sediment that were previously impounded behind the dam in a short amount of time.

With Structure From Motion we can not only model the change in elevation of the dam pond, but quantify the amount of sediment that has been evacuated.

__Kristian Nelson recently completed this analysis of elevation change in the dampond section since its removal.__

![alt text](https://philipwool.github.io/project3/Elev_Diff.jpg)

This type of analysis can be applied to the entire stream reach in the future, giving us the ability to track morphological changes after major events and over time.
