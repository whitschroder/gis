# Summarizing Vector Data

This tutorial describes several methods for summarizing data in ArcGIS Pro and exporting to Excel or R, for example, for further analysis.

The following list includes a series of questions you might want to ask about your spatial data in vector format, and you can likely come up with many more questions you can answer. Many of these questions can be answered intuitively with small datasets just by visualizing the data, but with large datasets, you will want to automate these calculations. Much of GIS involves a process of first visualizing data and then problem solving to come up with ways to automate analysis for larger and more complex datasets.

1. What are the dimensions of your vector data (extent, length, area, etc.)?

2. How many records of a certain type are represented?

3. What areas have high vs. low densities of features?

4. How do your various vector records relate to each other?

More specific questions can of course be asked based on the context of your data. ArcGIS Pro's Geoprocessing Toolbox has several tools that can be used for these types of summary statistics on vector data.

## Add Geometry

In ArcGIS Pro, the geometries of feature classes can be documented by using the Measure tool under Map -> Inquiry -> Measure Distance. In QGIS, the Measure Line tool (and Measure Area) can be used. Here distances, perimeters, areas, and angles can be easily measured using the cursor. However, these values are not saved anywhere and would require manual copying and data entry to store them. Alternatively, we can add the geometry of vectors to their attribute table for further analysis.

In ArcGIS Pro, when creating a feature class as part of a geodatabase, two fields may be automatically added to the attribute table, depending on the geometry of the feature class. For polygons, these two fields are Shape_Length and Shape_Area; for polylines, only Shape_Length is added; and since points are zero dimensional, no geometry fields are added. When editing records, these columns will automatically be populated with values measured in the units of the coordinate system.

Shapefiles do not have this advantage, however, even when creating feature classes in a geodatabase, you may want to add additional information to the attribute table or specify different units (particularly if your coordinate system is geographic and units are measured in degrees rather than meters or feet). To add geometry to vector attribute tables, use the [Calculate Geometry Attributes tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/calculate-geometry-attributes.htm). This tool takes a feature class as an input along with parameters including, geometry attributes, units, and an optional coordinate system (the input's coordinate system is the default).

For polygons, the geometry attributes are area, perimeter, number of parts (for merged polygons), number of vertices, number of holes, number of curves, central coordinates, and min/max coordinates (extent). A field must be specified in the attribute table where these values will be populated. You can select an existing field or type a header for a new field that will be automatically created. Note that fields like Shape_Length and Shape-Area are read only and cannot be edited. The units can then be specified. For lines, several similar geometry attributes can be calculated, along with line length and line bearing. For points, only coordinates can be added (note that doing so essentially replicates the functionality of the [Add XY Coordinates tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/add-xy-coordinates.htm)).

The appropriate tool in QGIS is Add geometry attributes under [Vector geometry](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html). The geometry attributes can be set to match the layer's coordinate reference system.

## Summarize Within

A very useful tool in ArcGIS Pro, [Summarize Within](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/summarize-within.htm) calculates summary and attribute statistics for a feature class inside a polygon. Note that this tool can only output to a geodatabase. The tool takes as input a polygon representing the region of interest and the summary features, which is the feature class to be summarized. The tool will output a new feature class that summarizes a statistic (sum, mean, minimum, maximum, or standard deviation) based on a specified column value. A separate box can be checked to add summary geometry values. Keep all input polygons is automatically checked, meaning that all polygons will be preserved in the output, even if they have no data to summarize in them. Unchecking this box will eliminate polygon records that have no data. When working with sample areas, you want to keep track of which samples have no data, so you should usually leave this box checked.

A similar tool in QGIS is Join attributes by location (summary) under [Vector general](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeneral.html). This tool adds summary statistics from a joined layer (mean, maximum, minimum, sum, etc.). This tool will not calculate geometries, but combining this tool with the Add geometry attributes tool will approximate the functionality of the Summarize Within tool.

## Feature to Point (Centroid)

The [Feature to Point tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/feature-to-point.htm) can be useful when polygon or polyline data needs to be converted to point data (to add coordinates, conduct point pattern analysis, etc.). This tool takes a polygon or polyline feature class as input and outputs the feature's centroid. Note that for complex shapes, the centroid/center of mass will not necessarily intersect with the original shape. This occurs especially with linear data where the centroid will usually be positioned outside of the line. Polygons like donuts or L-shaped features will have their centroids outside of the shape. To force the output centroid to intersect with the input feature class, check the Inside box.

In QGIS, the Centroid tool under [Vector geometry](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html) will generate centroids, while the Point on surface tool will force the point to overlap with the input line or polygon.

The Feature to Point tool is essentially the opposite of tools like [Buffer](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/buffer.htm) and [Minimum Bounding Geometry](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/minimum-bounding-geometry.htm). For example, Buffer and Minimum Bounding Geometry can be used to convert zero dimensional point data into a polygon, which could help with spatial joins and other summary tools.
