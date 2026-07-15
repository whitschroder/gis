# Conversion Tools

We have so far dealt with vector and raster data separately, but several tools are available to convert from vector to raster and vice versa. These conversion tools can be necessary at times to bring in additional categorical data into models based on raster analysis.

In ArcGIS Pro, the conversion tools are available in the Geoprocessing toolbox under Conversion Tools:

```{image} /images/conversion.jpg
:alt: Conversion Tools
:class: bg-primary mb-1
:width: 40%
:align: center
```

The relevant QGIS tools are discussed below.

## Feature Class to Raster

Under the "To Raster" section, several tools are available, including [Feature to Raster](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/feature-to-raster.htm), [Point to Raster](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/conversion/point-to-raster.htm), [Polyline to Raster](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/polyline-to-raster.htm), and [Polygon to Raster](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/polygon-to-raster.htm). In reality, the Feature to Raster has all the functionality needed to convert from a feature class (whether point, polyline, or polygon) to a raster.

In the following example, we input several points representing archaeological sites into the Feature to Raster tool. The Field parameter will determine the values of the output raster. The output cell size will, of course, determine the cell size of the output raster. To snap the raster to an existing dataset, load the appropriate raster layer into Snap Raster under the Environments tab of the Feature to Raster tool. We then get a raster of single pixels in the point locations, aligned to the snapped raster:

```{image} /images/pointraster.jpg
:alt: Point Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

If we input the following line feature into the Feature to Raster tool:

```{image} /images/road.jpg
:alt: Road
:class: bg-primary mb-1
:width: 80%
:align: center
```

with output cell size set to 10 m, we generate the following raster:

```{image} /images/roadraster.jpg
:alt: Road Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

If we input polygons:

```{image} /images/polygons.jpg
:alt: Polygon Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

we achieve an output like the following:

```{image} /images/polyraster1.jpg
:alt: Polygon Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

With higher resolution (smaller cell size), we get an output almost indistinguishable from the vector layer:

```{image} /images/polyraster2.jpg
:alt: Polygon Raster
:class: bg-primary mb-1
:width: 80%
:align: center
```

In QGIS, use Rasterize (vector to raster) to convert a feature class to a raster. An optional field (Field to use for a burn-in value) can be defined from the attribute table to be assigned to the raster value, or a single value (A fixed value to burn) can be set if all input features should have the same raster value. Output raster size units can be set to Georeferenced units, and a width and height for the pixels can be defined based on the coordinate reference system. To snap to another raster, the appropriate extent can be calculated under Output extent with the Calculate from Layer option. An optional NoData value can be defined, but this should generally be set automatically. The Output data type can also be set based on the range of your data. For categorical data without decimals or negative values, Byte or UInt16 usually suffice.

The resulting raster does not typically load properly in QGIS. Right-click the raster output under Layers and select Properties. Under Symbology, change Render type to Paletted/Unique Values, click Classify, Apply, and OK.

## Raster to Feature Class

Under Conversion tools, several additional tools can convert raster layers to feature classes. The [Raster to Point tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/raster-to-point.htm) will generate points located at the center of each cell, with the value of that cell included as a field in the new layer's attribute table. In QGIS, use Raster pixels to points.

The [Raster to Polyline tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/raster-to-polyline.htm) converts a raster grid to a polyline feature class. A background value must be set (either 0 or NoData). The Simplify Polygons option can be checked to reduce the number of vertices in the resulting feature class; alternatively, if unchecked, the output feature class will match exactly the shape of the cells in the input raster. The input raster must be of integer type. In QGIS, use [r.to.vect](https://grass.osgeo.org/grass-stable/manuals/r.to.vect.html) in GRASS with Feature type set to line. In Whitebox Tools, use the RasterStreamsToVector tool.

The [Raster to Polygon tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/raster-to-polygon.htm) converts a raster layer to a polygon feature class. With the following input raster layer representing a classified digital elevation model:

```{image} /images/elevclass.jpg
:alt: Classified Elevation
:class: bg-primary mb-1
:width: 80%
:align: center
```

We generate the following polygon feature class:

```{image} /images/rasterpoly.jpg
:alt: Raster Poly
:class: bg-primary mb-1
:width: 80%
:align: center
```

The Simplify Polygons option will reduce the number of vertices, and the Create multipart features option will create a single record for each output polygon. The input raster must be of integer type.

In QGIS, use the Polygonize (raster to vector) tool under GDAL (not to be confused with the Polygonize tool under Vector geometry). To simplify the result, use the Simplify tool under Vector geometry.
