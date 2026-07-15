# The Least Cost Path Workflow

The workflow for generating least cost paths in ArcGIS Pro consists of the following steps:

1. Determining origin and destination points.
2. Establishing parameters that will restrict or aid travel.
3. Creating a friction surface based on the destination and parameters.
4. Generating the least cost paths.

## Introduction to Path Modeling

We have already used a variation of least cost path modeling by running the hydrology tools. These tools determine the direction of the flow of water, the least cost (in this case steepest grade), and the flow accumulation for each output cell. Instead of inputting a DEM, we can input a [Euclidean Distance](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/distance-accumulation.htm) raster to the [Flow Direction tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/flow-direction.htm).

To determine paths to the following site:

```{image} /images/pn.jpg
:alt: PN
:class: bg-primary mb-1
:width: 80%
:align: center
```

We can generate a Euclidean distance surface:

```{image} /images/pndistance.jpg
:alt: PN Distance
:class: bg-primary mb-1
:width: 80%
:align: center
```

Inputting this surface into Flow Direction, we generate this surface:

```{image} /images/pndirection.jpg
:alt: PN Direction
:class: bg-primary mb-1
:width: 80%
:align: center
```

Finally, we input the Flow Direction raster into Flow Accumulation, but we also specify an Input weight raster. This parameter is generally left blank when running the hydrological tools, but by inputting a raster that represents specific locations, the tool will run a flow or path model using those cell locations as the source. To create such a raster, use the [Feature to Raster tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/feature-to-raster.htm) to convert another set of origin points to raster.

```{image} /images/origin.jpg
:alt: Origin
:class: bg-primary mb-1
:width: 80%
:align: center
```

Note that all cells should be set to a value of 1, so you may need to add a field to the input point feature class with all values set to 1, or reclassify the resulting surface so that all cells representing origin sites are set to 1. After running Flow Accumulation, we can convert the raster to a polyline feature class to visualize the routes (note that setting output data type to integer will be necessary to run this step):

```{image} /images/eucroutes.jpg
:alt: Euc Routes
:class: bg-primary mb-1
:width: 80%
:align: center
```

The resulting surface shows a dendritic network of paths. We can create more of a spider web network, which more accurately represents the shortest Euclidean distances from each point to the destination; for example, we can input our distance raster into the [Least Cost Path tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/intelligence/least-cost-path.htm). We input the Euclidean distance raster as the input cost surface, and we define the starting and ending points. For best results, use a single start point with travel to ending points that can represent one or many places:

```{image} /images/leastpn.jpg
:alt: Least PN
:class: bg-primary mb-1
:width: 80%
:align: center
``` 
