# Euclidean Distance

Straight line distance can be an important variable when working with raster data. This type of distance is known as Euclidean distance. The [Distance Accumulation tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/distance-accumulation.htm) in ArcGIS Pro creates a new raster where each cell represents the horizontal distance between the center of that cell and the center of the nearest of a designated set of cells on an existing grid or a feature class.

The following grid is an example of straight line distance accumulation between a set of input points. Each cell represents the distance to the nearest input cell or feature class of interest.

```{image} /images/distance.jpg
:alt: Distance
:class: bg-primary mb-1
:width: 80%
:align: center
```

The Euclidean distance raster is similar to results that can be achieved with a tool like [Multiple Ring Buffer](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/multiple-ring-buffer.htm), however the raster output of Distance Accumulation is continuous.

The input to the Distance Accumulation tool can be a feature class (in the previous example points) or a raster with values assigned to pixels of interest over a NoData background. If a raster is used as an input, the output raster will have the same processing extent and cell size (resolution) as the input raster. If a feature class is used as an input, the processing extent will match the minimum bounding rectangle of the feature class and the cell size will be automatically calculated. Alternatively, the processing extent and cell size of the output raster can be specified in the Environments tab of the Distance Accumulation tool.

The appropriate tool in QGIS is Proximity (raster distance) under GDAL. The input layer must be in raster format. Therefore, any points must first be converted to raster using Rasterize, defining the cell size and output extent. The Proximity Raster tool under SAGA has similar functionality.

Note that a similar visualization to that achieved with the Buffer or Multiple Ring Buffer tool can be achieved by changing the symbology of the distance accumulation raster, namely by changing the Stretch symbology to Classify in ArcGIS Pro or to Discrete in QGIS.

```{image} /images/distanceclass.jpg
:alt: Distance
:class: bg-primary mb-1
:width: 80%
:align: center
```

## Euclidean Direction

An optional Output Back Direction raster can also be generated. An example of such a raster is shown below:

```{image} /images/direction.jpg
:alt: Direction
:class: bg-primary mb-1
:width: 80%
:align: center
```

In this raster, each pixel represents the direction to the nearest pixel or feature of interest. The Euclidean direction raster is not generally useful on its own but can be an important intermediate raster for subsequent analyses.

In QGIS, the Proximity Raster tool under SAGA can generate an optional Direction output. Note that the default symbology is continuous, but compass directions are best displayed with a discrete visualization, an example available here (under Layer Properties -> Symbology, select Singleband pseudocolor and Load color map from file): {download}`direction.txt </direction.txt>`.

## Euclidean Allocation

The [Distance Allocation tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/distance-allocation.htm) in ArcGIS Pro assigns each raster area of interest or feature class to its own zone, based on proximity to other raster areas of interest or feature classes. The resulting raster surface shows these zones with their boundaries marking the midpoint between these raster areas of interest or feature classes. Each pixel is assigned a unique value that matches the value of the nearest input cell or feature class of interest.

```{image} /images/allocation.jpg
:alt: Allocation
:class: bg-primary mb-1
:width: 80%
:align: center
```

Euclidean allocation produces a set of zones known by several names, including Thiessen polygons or Voronoi regions. Note that a similar tool, [Create Thiessen Polygons](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/create-thiessen-polygons.htm) creates a similar output, however as a feature class rather than a raster grid.

In QGIS, use the Proximity Raster tool under SAGA and generate an optional Allocation raster. The input must be in raster format, and each point of interest must have a unique value (assigned during the Rasterize process).
