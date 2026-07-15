# Reclassify and Slice Tools

## Classifying Rasters

The default symbology of raster grids in ArcGIS Pro usually loads as a Stretch symbology or a continuous surface, as shown below: 

```{image} /images/elevstretch.jpg
:alt: Elevation Stretch
:class: bg-primary mb-1
:width: 80%
:align: center
```

Rasters can also be displayed as categories, changing the Stretch symbology to Classify. The following image shows a digital elevation model classified into 5 categories:

```{image} /images/elevclass.jpg
:alt: Elevation Classified
:class: bg-primary mb-1
:width: 80%
:align: center
```

This visualization is only temporary, however, and the actual raster values remain unchanged.

## Reclassify

We might want to make such a classification permanent by generating a new raster grid where each cell now has a value representing a category rather than an elevation. To do so, we can use the [Reclassify tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/reclassify.htm). After opening the Reclassify tool and loading the appropriate input raster surface, the tool will automatically populate the reclassification table with the values from the symbology. Alternatively, if the raster layer is currently set to a stretch symbology, we can click the Classify button to define a classification.

```{image} /images/reclassifytool.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

According to this table, all values in the range from Start to End will be reclassified to the value under the New column. NODATA will remain unchanged. The output raster will look similar to the classified output, but now the range of cell values is only 1 to 5, rather than -22 to 1925.

The Reclassify tool is most useful when establishing inputs of equal weights when developing models. For example, different input variables (e.g., elevation, soil type, precipitation) can be scaled between 1 to 10 to assist with comparison.

Alternatively, a single range of values can be isolated, as seen in the table below:

```{image} /images/reclassifytool2.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

This reclassification will assign all values to NODATA except for valley zones between 80 and 352 m of elevation:

```{image} /images/valley.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

We can also reverse values with NODATA values, for example in the following 1-arc second global SRTM with voids:

```{image} /images/srtmvoid.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

When loaded into the Reclassify tool with a single range of values, the reclassification table is populated as the following:

```{image} /images/reclassifytool3.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

We can now assign the range of values to NODATA, and assign NODATA as 1:

```{image} /images/reclassifytool4.jpg
:alt: Reclassify Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

We then generate the following raster with voids isolated:

```{image} /images/voids.jpg
:alt: Voids
:class: bg-primary mb-1
:width: 80%
:align: center
```

Note that the Reclassify method only allows for integer outputs (although values can be positive or negative).

## Slice

The [Slice tool](https://pro.arcgis.com/en/pro-app/3.3/tool-reference/spatial-analyst/slice.htm) is similar to Reclassify, but the specific ranges of values for the reclassification do not need to be defined. Instead, the required parameters are the number of slices (or output zones), the starting value for the output, an optional value to reclassify NODATA, and a slice method. The resulting output will be similar to the Reclassify tool.

The advantage of the Slice tool is that a reclassification method can be assigned to multiple input rasters that may have very different ranges. This approach is most useful when automating processes, where several rasters can be input with the same parameters to create scaled outputs.
