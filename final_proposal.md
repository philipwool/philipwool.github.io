Ryan Wooldridge
GES 486

__Final Project Write Up__

The removal of the Bloede Dam on the Patapsco river provides a unique opportunity to model phenomena such as the release of large amounts of previously impounded sediment, and morphologic changes caused a completely new upstream flow conditions.

This particular project has several objectives, of which the first is to create a digital elevation model (DEM) of the entire Patapsco study area using structure from motion (SFM). This area includes the dam pond upstream of the Bloede dam, and reaches all the way down to the lower floodplain. The second component of this project is to compare the digital elevation values developed using SFM to those associated with Maryland Geological Survey (MGS) transects to assess the accuracy of the model. In the long term, if these techniques for creating DEMs prove to be accurate, they can be used to monitor and model characteristics of dam removal such as the evacuation and deposition of sediment that was impounded behind the dam, as well as changes to channel morphology. When compared to traditional methods, SFM offers the opportunity to observe these phenomena over the entire stream reach rather than using transect data to interpolate conditions over what can be a substantial unobserved area.

In order to achieve this, aerial drone imagery was first loaded into Agisoft Photoscan. The imagery is assessed for quality and aligned in order to create a sparse point cloud. Known ground control points (GCPs) are added to the sparse point cloud and identified in the constituent images. A process known as gradual selection is applied to help identify and eliminate any points in the sparse point cloud that do not meet standards of accuracy. This is an important step as the sparse point cloud is the foundation on which the dense point cloud (DPC) is built. Once a DPC is built, a georeferenced DEM can be built.

After the DEM is built, it can be brought into Arcmap in order to perform error analysis. In addition to the channel DEM, the MGS transect shapefile is brought in, and the Values to Points tool is used to create a new point shapefile, with identical x,y values, but with an additional column of elevation (z) values in its attribute table. Using the Field Calculator tool it is possible to create a new column of values that quantify the difference between the MGS transect elevation values and the DEM elevation values, essentially characterizing the error on the model. Additionally, these table values are exported to a csv in order to apply further analytics in Excel. Upon applying said analytics, the average error of the DEM was found to be about one foot, as was the root mean squares error.

The next part of the analysis is done in QGIS. Using a Python script, the DEM is brought in, as well as the MGS transect points, which are displayed in red. Additionally, within Python an SQL query is performed in order to create a selection of points that lie within an acceptable margin of error, in this case one foot. The script then proceeds to write the selection to file as a new shapefile, add this new shapefile to the map, and display the new points in green. The result is the DEM overlaid with the MGS transect points, highlighting accurate areas with green points, and displaying points that fell outside of the accuracy threshold in red. This DEM can then be used as the Raster layer in 3D Viewer to create a three-dimensional map of the entire stream reach.

Once these DEMs can be shown to be accurate, further imagery taken after major events can be used to create additional DEMs that can be compared to track and model changes in channel morphology over the entire stream reach.

What are you going to do for the final project?

Assessing the Accuracy of DEMs produced by SFM

What is your question?

What is the average error? RMSE? Which areas, if any are problematic?

Where is the data coming from? Provide links? If you don't have - or can't find - the data, pick a different project.

Data for this project was Collected by us.

What three non-superficial elements from the class are you going to incorporate? Python? SQL? Moran's I? 3D mapping? Hexagonal analysis? Analysis in GeoDa? Something else? (Non-superficial meaning doing more than importing the data with python.)

1.	Using Python to perform a query, make a selection and write selection to file.
2.	SQL
3.	3D mapping

How will you know when you've answered your question?

When error has been evaluated and points have been added to the map to create a visualization of any success or problematic areas.

What other component from the class will you incorporate?

Using Python to:

1.	Add shapefiles
2.	Create custom symbology
3.	Update the map’s layer tree

Why is more involved than the labs?

This project required the use of Agisoft, as well as Arcmap and Excel analysis

Why did you choose this component?

I wanted to see if I could incorporate skills I learned in GES 486 into my internship to more effectively analyze and display our results.

Go above and beyond and trying something new - explain what it is that you learned on your own here.

Quantifying the difference between the MGS transects and the elevation values of the model in Arcmap using Values to Points was a new analysis tool for me, and it worked out well, I was very pleased with the error analysis results and their level of improvement over previous iterations of DEM creation.
