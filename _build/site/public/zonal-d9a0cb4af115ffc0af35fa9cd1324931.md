# Zonal Statistics

Broadly, zonal statistics refer to GIS techniques used to summarize statistics from one raster layer within zones defined by another raster or feature class layer.

## Zonal Statistics as Table

The [Zonal Statistics as Table tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/zonal-statistics-as-table.htm) will output a table that summarizes a set of statistics (including mean, median, maximum, minimum, etc.) within the zones of a raster layer or feature class.

In QGIS, use Raster layer zonal statistics under [Raster analysis](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html). The input layer represents the raster to be summarized, and the Zones layer is a raster surface representing the zones in which the input raster will be summarized. The output can be in csv format, or if shapefile is chosen, a dbf will be output (note that the only output is a table without a shapefile).

Let's take the following example of our distance allocation surface generated from archaeological site points. We can summarize several statistics related to another raster layer, in this case the digital elevation model. The following image shows the distance allocation surface displayed over the DEM with a 30% transparency:

```{image} /images/zonal1.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

After running the Zonal Statistics as Table tool, we generate the following table showing various statistics within each zone defined by the distance allocation raster:

```{image} /images/zonaltable.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

## Zonal Statistics

The [Zonal Statistics tool](https://pro.arcgis.com/en/pro-app/3.3/tool-reference/spatial-analyst/zonal-statistics.htm) performs a similar operation as the Zonal Statistics as Table tool, however, the output is a raster layer with cells assigned to a given statistic within zones. The following raster layer shows the maximum elevation recorded from the input DEM, summarized within each zone generated from the distance allocation of input point data (archaeological sites):

```{image} /images/zonal2.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

In QGIS, the Zonal Statistics tool under [Raster analysis](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html) is similar. However, this tool takes an input polygon to define zones, rather than an input raster. The raster to be summarize must be input as the Raster layer. The statistics can then be defined under Statistics to calculate. The output will also be in shapefile format. This output can be optionally converted to raster using Rasterize and selecting the desired statistic from the attribute table.

A more similar tool to the ArcGIS Pro Zonal Statistics in QGIS is [r.stats.zonal](https://grass.osgeo.org/grass-stable/manuals/r.stats.zonal.html) in GRASS. This tool takes a Base raster to define the zones and a Cover raster representing the values to be summarized. The Base raster must be in an integer format, meaning that the bit depth must be 8-bit unsigned (Byte), 8-bit signed (Int8), 16-bit unsigned (UInt16), or 16-bit signed (Int16). The Base raster can be converted to the appropriate bit depth using Warp (reproject) in GDAL. A single statistic can then be selected to be used as the value of the output raster.

## Zonal Geometry as Table

The [Zonal Geometry as Table tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/zonal-geometry-as-table.htm) summarizes in tabular form several geometry statistics based on a raster of zones (each represented by a single value). In contrast to the Zonal Statistics tools, the Zonal Geometry tools require only a single layer. This single layer must represent zones of interest. In contrast, no additional raster is needed to summarize statistics because all of the geometry statistics are inherent to the input zonal raster.

The following table summarizes several geometry statistics from the distance allocation grid:

```{image} /images/zonal3.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

## Zonal Geometry

The [Zonal Geometry tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/zonal-geometry.htm) in ArcGIS Pro, like the Zonal Statistics tool, summarizes values in raster form, namely values based on a geometry calculation defined in the tool parameters.

The following output raster displays each zone generated from the distance allocation tool with its area value (calculated from the units of the coordinate system):

```{image} /images/zonal4.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

QGIS does not have a similar tool. Several options are available, including running one of the Zonal Statistics tools set to count, then using Raster Calculator to multiple by the cell size (width * height). I have found such results to be inaccurate. Another option is to convert rasters to vectors and use the field calculator in the attribute table to create a new field with the expression $area. The result can then be converted back to raster.

The most accurate results I have found are by using the Raster layer unique values report under [Raster analysis](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html). When an output Unique values table is generated in shapefile format, the shapefile fails to generate, but a table in dbf format is generated. This dbf file can be added to QGIS under Layer -> Add Layer -> Add Vector Layer. The dbf should have a value, count, and m2 fields. You will need to create minimum and maximum values to reclassify your zone layer based on the values. Open the attribute table of the dbf layer, then use the Field Calculator to create a new field using "value" + 1. Next run Reclassify by layer under Raster analysis. Set the raster layer to your zones, and select your output from Raster layer unique values report as your Layer containing class breaks. Set the Minimum class value field to the value from your table, set the Maximum class value field to the value plus one from your table, and set the Output value field to m2 from your table. Then change the Range boundaries to min <= value < max.

## Region Group

The [Region Group tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/region-group.htm) in ArcGIS Pro will take a raster layer as input that has several separated cell zones with the same value. The output of the Region Group tool will be a new raster where each zone has been assigned its own unique value. 

In QGIS, use the [r.clump](https://grass.osgeo.org/grass-stable/manuals/r.clump.html) tool in GRASS. You may need to open Layer Properties in the resulting output file, go to Symbology, and click Classify under Band Rendering to remove values outside of the range of the output.

When the following raster layer is input, where each zone has the same value (in this case 0 over NoData):

```{image} /images/polyraster2.jpg
:alt: Polygon Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

The following output raster is returned, where each zone has been separated into its own value:

```{image} /images/regiongroup.jpg
:alt: Region Group
:class: bg-primary mb-1
:width: 80%
:align: center
```
