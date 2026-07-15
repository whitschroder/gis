# Focal Statistics, Resampling, and Aggregating Raster Data

Raster data can be resampled to create a smoother surface, a coarser/lower resolution surface, or a higher resolution surface.

## Raster Symbology

To temporarily create a smoother surface, the symbology of a raster file can be changed by selecting the layer in Contents, then clicking Raster Layer at the top of the ArcGIS Pro window, and selecting the options under Rendering.

```{image} /images/rendering.jpg
:alt: Rendering
:class: bg-primary mb-1
:width: 80%
:align: center
```

Selecting DRA, or Dynamic Range Adjustment, will adjust the symbology when zooming in and out.

Under Resampling Type, several options are available. The default selection is Nearest Neighbor, where each cell is assigned its own value. Bilinear resampling will average the values from the four nearest cells, similar to the way a rook moves in chess. Cubic resampling will sample the nearest 16 cells.

In QGIS, these options are available in Layer Properties -> Symbology. To adjust the symbology when zooming in and out, under Min/Max Value Settings, set the Statistics extent to Updated canvas. For resampling, under Resampling, set Zoomed in to Bilinear or Cubic.

## Focal Statistics

In ArcGIS Pro, the [Focal Statistics tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/focal-statistics.htm) defines a neighborhood of cells, measured in map units or pixels, where a statistic (sum, maximum, minimum, mean, etc.) is applied. The output raster will assign each cell the value of the statistic of that cell and its surrounding cells within this defined neighborhood.

Selecting "mean" as the statistic will average the raster values inside the neighborhood, creating a smoother surface. Note that Focal Statistics will not change the resolution of the output raster but will rather preserve the input's resolution while summarizing the statistics inside the neighborhood.

QGIS does not have a built-in Focal Statistics equivalent. The best alternative is [r.neighbors](https://grass.osgeo.org/grass-stable/manuals/r.neighbors.html) under GRASS. Unfortunately, installing GRASS on a Mac is not straightforward. Another option is the Focal Statistics tool available under SAGA. Finally, if these other options do not work, install the Whitebox Workflows Plugin for QGIS from Plugins -> Manage and Install Plugins. If you receive errors, you may need to install backend files by following these [instructions](https://www.whiteboxgeo.com/manuals/qgis/installation-and-setup.html).

Once installed, under Whitebox Workflows, use the Mean Filter tool to compute focal statistics (mean). Other filters, for example, Maximum Filter, Minimum Filter, etc., are available.

## Aggregate

The [Aggregate tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/aggregate.htm) will apply a statistic to a defined neighborhood and output a lower resolution raster surface. The Aggregation technique includes several similar statistics as in the Focal Statistics tool, including sum and mean. The Cell factor will define the output resolution based on a multiplication factor. If the input cell size is 30 m, and the cell factor is set to 3, the output resolution will be 90 m.

## Resample

The [Resample tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/resample.htm) will permanently output a new raster with a defined cell size (resolution). The Output Cell Size can be specified (pay attention to the horizontal units of the input raster). This value can be higher or lower than the input raster. The Resampling Technique can then be specified, using the same options as under Raster Layer -> Rendering, although the Resample tool will output a new raster.

## Resampling in QGIS

The Warp (reproject) tool under GDAL [Raster projections](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/gdal/rasterprojections.html) can be used to generate lower or higher resolution rasters. To resample to a lower resolution, select the Resampling method to use (Average, for example), then set the Output file resolution in target georeferenced units to the desired resolution. To resample to a higher resolution, select the Resampling method to use (Nearest Neighbor, Bilinear, or Cubic), then set the Output file resolution in target georeferenced units to the desired resolution.

The Nearest Neighbor method is best for discrete data (for example, when numbers represent categories), while Bilinear or Cubic are best for continuous data.
