# Lab 6: Viewshed Analysis

In this lab, students will conduct a viewshed analysis.

The data for this week's lab includes:

1. ASTGTMV003_N14W092_dem.tif -- an ASTER DEM tile
2. sites.shp -- a feature class of points representing archaeological sites

Prepare your data to run either the planar or geodesic viewshed tools. Run the following analyses and provide screenshots or maps of your workflow (assume that all observers are at a height of 1.5 m):

1. Run a viewshed analysis from San Andres Semetabaj. What is the location of the point representing the site in relation to the site's architecture (refer to your digitized map from Lab 2 or your interpolated surface from Lab 4)? How many of the mapped mounds are visible from this location according to the viewshed analysis? What other sites are visible from San Andres Semetabaj? (You can visually check the output raster, or refer to the [Extract Values to Points tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/extract-values-to-points.htm)).
2. Run a viewshed/visibility analysis from all sites (with the Frequency option). What does the output raster represent? What are the three most frequently visible sites?
3. Run a viewshed/visibility analysis from these three sites (with the Observer option). What does the output raster represent? Adjust the symbology and legend to aid in the visualization of this map.
4. Run a viewshed analysis from San Andres Semetabaj, but incorporate distance into the symbology to highlight that visibility diminishes as distance increases.
5. Run a viewshed/visibility analysis from San Andres Semetabaj and any other sites visible from San Andres Semetabaj but restrict the visibility only to the azimuths that include a 20° field of view where each site is visible from the other. Adjust the symbology and legend to aid in the visualization of this map.
6. Identify the nearest site to San Andres Semetabaj. How much higher would the architecture at San Andres Semetabaj have to be to make this nearest site visible?
