# Lab 5: Suitability Modeling and Map Algebra

In this lab, students will conduct a suitability analysis.

The data for this week's lab includes:

1. n17_w092_3arc_v2.tif -- A void-filled, 3-arc second SRTM digital elevation model.
2. suelos.shp -- a soil type feature class.
3. INEGICuerposAgua.shp -- a polygon feature class representing lakes.
4. INEGICorrienteAgua.shp -- a polyline feature class representing streams.

Using these datasets and any raster derivatives, run a suitability analysis to determine likely site locations. Choose any parameters you think are relevant. Follow the workflow [here](https://pro.arcgis.com/en/pro-app/latest/help/analysis/spatial-analyst/suitability-modeler/the-general-suitability-modeling-workflow.htm). 

Submit the following:

1. A map showing the results of your suitability analysis.
2. After classifying the suitability analysis raster into 5 quantiles, create a new surface by reclassifying just the upper 20% quantile to an integer value of your choosing and the rest to NoData. Create a map of these upper 20% quantile zones, displayed with a legend showing classes based on each of their areas in square kilometers.
