# Introduction to the Hydrology Workflow

In order to conduct several hydrological analyses in ArcGIS Pro or QGIS, we first have to follow a basic hydrology workflow to generate the appropriate input data for modelling. The general workflow consists of starting with an input digital elevation model and:

1. Filling pits
2. Generating a Flow Direction raster
3. Generating a Flow Accumulation raster

## Fill

Before conducting a hydrological analysis, DEM data must be prepared. DEM data can have several errors related to the interpolation of elevation data, namely pits produced by extreme low points. These pits must be removed; otherwise, a hydrological analysis would direct all streams to these pits. In certain landscapes, these pits may actually be real features. Thus, care must be taken when filling in pits to ensure that real features are not lost in the process.

The [Fill tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/fill.htm) in ArcGIS Pro takes a DEM as input, identifies sinks, and then fills in these sinks using additional interpolation. An optional Z limit can be defined to limit the size of sinks that are filled in. Larger values will fill more sinks, while smaller values will fill fewer sinks. If left blank, all sinks will be filled. Best practice is to run the Fill tool with the Z limit setting left blank, assess the results from later tools, and if necessary, run the Fill tool again with a high Z limit (e.g., 100 m), and iterate through decreasing values.

```{note}
In QGIS, the best hydrology tools are available in SAGA and Whitebox Workflows. In SAGA, several Fill Sinks methods are available (QM of ESP is standard). In Whitebox Workflows, use one of the Fill Depressions tools. If using GRASS, try the r.fill.dir tool, which will also output a Flow Direction surface.
```

Another optional step is to smooth the input DEM, using the [Focal Statistics tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/focal-statistics.htm) set to mean. This tool may be iterated several times to produce smoother surfaces as needed. This step is generally needed with higher resolution DEM data.

```{note}
In QGIS, use r.neighbors in GRASS or a mean filter in SAGA or Whitebox Workflows.
```

## Flow Direction

The [Flow Direction tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/flow-direction.htm) in ArcGIS Pro creates a raster representing the direction of flow from each cell to its downslope neighbor. Several methods are available. The most commonly used method is D8, which assigns direction based on a cell's steepest downslope neighbor (using the 8 surrounding cells). The MFD method is more complex, generating a raster that is visualized the same as a D8 raster but with more complex metadata that is incorporated into later operations. The DINF method assigns the steepest downslope neighbor based on a triangular facet. The Force all edge cells to flow outward option addresses how to deal with edge effects. This option should usually remain unchecked, but if planning to run a basin analysis, this option should be checked. The input raster should be either a DEM or the modified DEM output from the Fill tool.

```{note}
Flow Direction is not a separate tool in QGIS but rather an intermediary step when running Flow Accumulation. You can therefore skip this step in QGIS. If you want to generate a Flow Direction raster, you can generate one with the GRASS tool r.fill.dir (though you cannot specify the method; the tool uses D8). Alternatively, you can generate Flow Direction optionally using SAGA's Channel Network and Drainage Basins. For more options, refer to Whitebox Workflows tools under Hydrology - Flow Routing. Any tool with Pointer in the name (for example, D8 Pointer) will generate a Flow Direction raster with the relevant method.
```

## Flow Accumulation

The [Flow Accumulation tool](https://pro.arcgis.com/en/pro-app/3.3/tool-reference/spatial-analyst/flow-accumulation.htm) in ArcGIS Pro takes the flow direction raster as an input and creates a raster surface that shows accumulated flow into each cell. The appropriate flow direction type should match the method used to generate the flow direction raster in the previous step.

```{image} /images/flowacc.jpg
:alt: Flow Accumulation
:class: bg-primary mb-1
:width: 80%
:align: center
```

```{note}
In QGIS, you can generate a Flow Accumulation raster in a single step from the input DEM using the Flow Accumulation (One Step) tool in SAGA. A similar single step tool in GRASS is r.flow, which uses the D-infinity method. To use D8 or MFD, use r.terraflow. In Whitebox Workflows, several flow accumulation tools are available under Hydrology - Flow Routing, for example, D8 Flow Accumulation, D-Infinity Flow Accumulation, MD-Infinity Flow Accumulation, etc. The input can often be a DEM (filled DEM) or pointer raster (Flow Direction). If using the latter, be sure to check the box indicating that the input is a pointer raster.
```

The flow accumulation raster shows a stream network; however, the default visualization may not show enough detail. The symbology can be manually classified into two categories, and a threshold value selected to reveal the desired order of streams; this may take some trial and error. The following image shows the stream network with 5 categories over a geometric interval:

```{image} /images/flowacc1.jpg
:alt: Flow Accumulation
:class: bg-primary mb-1
:width: 80%
:align: center
```

We can reclassify to the following:

```{image} /images/flowacc2.jpg
:alt: Flow Accumulation
:class: bg-primary mb-1
:width: 80%
:align: center
```

And we can convert to polylines using the [Raster to Polyline tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/raster-to-polyline.htm)

```{image} /images/flowacc5.jpg
:alt: Flow Accumulation
:class: bg-primary mb-1
:width: 80%
:align: center
```

If we want higher order streams, we can change the classification and generate a new polyline feature class:

```{image} /images/flowacc3.jpg
:alt: Flow Accumulation
:class: bg-primary mb-1
:width: 80%
:align: center
```
