# Terrain Analysis

Terrain analysis in ArcGIS Pro and QGIS requires the use of a digital elevation model (or digital terrain model), where the digital numbers represent elevation (usually relative to sea level or the ellipsoid datum). A digital elevation model alone may not provide enough detail to analyze subtle terrain differences. Usually, raster derivatives highlight variation better.

## Define Vertical Projection

Before producing raster derivatives, you must understand the coordinate system and units of your data. In ArcGIS Pro, you can right-click any raster layer in Contents and select Properties -> Source -> Spatial Reference. In QGIS, you can right-click any raster layer in Layers and select Properties -> Information. The horizontal and vertical units must be the same to conduct terrain analysis. If your data are in a planar coordinate system (UTM or State Plane), these units likely already match (either meters or feet). However, if your raster layer has horizontal units measured in degrees (geographic coordinate system), you will have to make adjustments. Fortunately, you have several options. 

First, you can reproject your geographic coordinate system into a planar coordinate system using the [Project Raster tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/project-raster.htm) in ArcGIS Pro or Warp (reproject) under GDAL in QGIS. 

Second, you can preserve the horizontal coordinate system as geographic (measured in degrees), and define a vertical coordinate system. Using the [Define Projection tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/define-projection.htm), you can define the vertical coordinate system to be in the correct units. Note that you will have to know the correct vertical coordinate system and units of your data. SRTM vertical coordinates, for example, are usually measured in meters above mean sea level in relation to the Earth Gravitational Model 1996 geoid (EGM 1996 Geoid). Once correctly defined, your data will be measured horizontally in degrees and vertically in meters. This option is generally not available in QGIS.

Third, you can do nothing and manually alter the Z factor when running any Surface or terrain analysis tools. The Z factor is a multiplicative/scale factor that is used to convert the vertical units into the appropriate horizontal units on the fly. The Z factor for converting meters to degrees will depend on the precise location but can be estimated around 0.00001. Note that if the vertical coordinate system is correctly defined, ArcGIS Pro will automatically calculate and populate this value (QGIS does not automatically update the Z factor, but it can be edited manually).

## Contours

The [Contour tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/contour.htm) in ArcGIS Pro can be run to generate contour lines based on an input DEM. The appropriate Contour interval can be specified (measured in the units of the input raster). If the resulting contour lines appear jagged, they can be smoothed by running the [Simplify Line tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/cartography/simplify-line.htm).

In QGIS, use the Contour tool under [Raster extraction](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/gdal/rasterextraction.html) in GDAL. Jagged countour lines can be smoothed by running the Simplify tool under [Vector geometry](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html).

## Hillshade

Hillshading or shaded relief is a technique used to model how light and shadow might fall across a landscape, available in the [Hillshade tool](https://pro.arcgis.com/en/pro-app/3.3/tool-reference/spatial-analyst/hillshade.htm) in ArcGIS Pro or in QGIS under [Raster terrain analysis](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/rasterterrainanalysis.html). The Azimuth represents the hypothetical direction of the light source, while Altitude or Vertical Angle represents the vertical angle of the light source relative to the viewer. The convention is to have the direction of the light source coming from the northwest, although this direction would of course change throughout the day and year based on the position of the sun. An analytical hillshade is technically a type of slope-aspect map.

## Slope

Slope refers to the rate of change in elevation from one location to the next, in other words, the first derivative of elevation. A Slope map can be generated using the [Slope tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/slope.htm) in ArcGIS Pro or in QGIS under Raster terrain analysis and can highlight topography more dramatically than a Hillshade. The drawback is that a Slope map will not show the direction of the slope, so elevated areas can be impossible to distinguish from low lying areas.

## Aspect

Aspect refers to the direction of slope. The [Aspect tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/aspect.htm) in ArcGIS Pro or in QGIS under Raster terrain analysis generates a raster surface categorized into compass directions. Aspect alone may not be useful for visualizing topography, but it represents an important intermediate variable that can be used in topographic analyses.

## Transparency and Blending

Several visualizations can be displayed at once using transparency or blending. Adding a 50% transparency to an upper layer over a lower layer can be useful, for example placing a transparent DEM over hillshade or slope. Blending, in contrast, more evenly combines two layers. Multiply is commonly used to darken imagery, where whiter areas become transparent in the top layer and blacker areas become darker by multiplying the colors of the base and upper layer.

Transparency and Layer Blend options are available in ArcGIS Pro under Raster Layer -> Effects when the relevant raster layer is selected under Contents. In QGIS transparency and blending are available under Layer Properties in the Symbology (Layer Rendering) and Transparency (Global Opacity) menus. Note that ArcGIS Pro uses transparency, while QGIS uses opacity, which are opposite, meaning that 25% transparency is equivalent to 75% opacity.
