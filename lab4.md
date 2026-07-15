# Lab 4: Introduction to Rasters and Surface Models

In this lab, students will acquire low resolution elevation data and generate higher resolution digital elevation models. Using these models, students will explore different ways of modelling terrain, as well as compare interpolation and density tools.

The data for this week's lab includes:

1. semcombinedUTM.txt -- a tab separated text file representing a table of coordinates in Zone 15N.
2. semetebaj2005_figurines.shp -- a feature class showing the locations of recovered figurines.
3. In addition, you will need to acquire SRTM data for this lab and refer to the mounds you digitized in Lab 2.

For this lab: 

1. Download SRTM (Shuttle Radar Topography Mission) digital elevation model (DEM) data over the archaeological site of San Andres Semetebaj. Download both the SRTM 1 Arc-Second Global and the SRTM Void Filled rasters. What are the differences between these two rasters? Are there any issues with these data in the study region? Note that to view differences appropriately, you must have a single layer checked in the Contents at a time.

2. Generate a hillshade of the 1-Arc-Second Global raster. Are there any issues with the hillshade? What is the problem and how can you fix it? Be sure to check the coordinate system of the data. Once fixed, generate the hillshade again and compare.

3. Now generate a slope. Adjust the symbology as needed.

4. Is there enough detail to make out any of the archaeological features? Add the semcombinedUTM.txt and generate points. What do these points represent?

5. Are there any patterns to the points? Run a density analysis to determine where the most points were recorded.

6. Generate a TIN model using the semcombinedUTM points. Now run several of the interpolation tools (e.g., IDW, Spline, Spline with Barriers). What are the advantages and disadvantages of each approach?

7. Compare your surfaces with your map from Lab 2. How close do your annotations match the surfaces you have generated? Adjust your annotated mounds accordingly.

8. Create a density surface of Semetebaj figurines.

9. Overlay your figurine density surface on top of your interpolated map of San Andres Semetebaj, over your SRTM data.

The final product of this lab should be a narrative describing your workflow with images or screen captures of the process.
