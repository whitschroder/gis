# Zonal Statistics

Broadly, zonal statistics refer to GIS techniques used to summarize statistics from one raster layer within zones defined by another raster or feature class layer.

## Zonal Statistics as Table

The [Zonal Statistics as Table tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/zonal-statistics-as-table.htm) will output a table that summarizes a set of statistics (including mean, median, maximum, minimum, etc.) within the zones of a raster layer or feature class.

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

The [Zonal Geometry tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/zonal-geometry.htm), like the Zonal Statistics tool, summarizes values in raster form, namely values based on a geometry calculation defined in the tool parameters.

The following output raster displays each zone generated from the distance allocation tool with its area value (calculated from the units of the coordinate system):

```{image} /images/zonal4.jpg
:alt: Zonal
:class: bg-primary mb-1
:width: 80%
:align: center
```

## Region Group

The [Region Group tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-analyst/region-group.htm) will take a raster layer as input that has several separated cell zones with the same value. The output of the Region Group tool will be a new raster where each zone has been assigned its own unique value. 

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
