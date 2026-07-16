# Clipping and Merging Features

## Introduction

The Geoprocessing Toolbox (available under Analysis -> Tools) contains three data-editing tools that generate new layers by combining, overlapping, or replacing the point, line, and/or polygon features of one existing layer with those of another: **Clip**, **Merge**, and **Erase**. A fourth tool, **Append** is similar to **Merge**.

The following are two example input polygons for these tools:

```{image} /images/threezones.jpg
:alt: Three Zones
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

```{image} /images/fourstates.jpg
:alt: Four States
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

Note that the tools **Clip**, **Merge**, **Erase**, and **Append** (especially the latter) differ from the Editing tools in that they cannot be undone once they have been executed.

## The Clip Tool

The [Clip](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/clip.htm) tool in ArcGIS Pro generates a new feature class that retains only those portions of a specified input layer that overlap with any one or more of the features on a specified "clip" layer.

```{note}
In QGIS this operation is also called Clip under [Vector overlay](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectoroverlay.html).
```

```{image} /images/cliptool.jpg
:alt: Clip Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

For example, using the Four States layer as an input and the Three Zones as the clip layer, we would generate a new layer like this:

```{image} /images/clipoutput.jpg
:alt: Clip Output
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

Note that the attribute table associated with the output file retains the same information as the input feature class but not the clip layer.

## The Erase Tool

The [Erase tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/erase.htm) in ArcGIS Pro is essentially the opposite of the **Clip** tool. Where the **Clip** tool generates an output where the input and clip layers overlap, the **Erase** tool erases overlapping features and generates an output outside of the clip layer.

```{note}
The same tool is called Difference under [Vector overlay](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectoroverlay.html) in QGIS.
```

Here is an example using the same input and clip layers as the previous **Clip** tool. Note that input features under the circle have been removed.

```{image} /images/eraseoutput.jpg
:alt: Erase Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

## The Merge Tool

As previously noted, the **Clip** and **Erase** tools retain the tabular data associated with the input layer rather than the clip layer. We can instead combine these two layers to include all data from both the input and clip layers. The [Merge](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/merge.htm) tool in ArcGIS Pro creates a new feature class by combining the features of existing layers of the same type (i.e., point, line, or polygon). 

```{note}
In QGIS, use the Merge vector layers tool in [Vector general](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeneral.html). 
```

Merging the states layer with the three zones layer creates a new layer that combines all features into a single layer.

```{image} /images/mergeoutput.jpg
:alt: Merge Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

The output is admittedly odd in this example. Generally, the **Merge** tool is best used to combine relevant data that are meaningfully related. For example, we could use the **Merge** tool to add the state of Rhode Island to our feature class. Or, we could take the outputs of the **Clip** and **Erase** tools to reunite the states to their original format.

```{image} /images/remerged.jpg
:alt: Remerged
:class: bg-primary mb-1
:width: 80%
:align: center
```

<br>

Note, however, that we now have a feature class with the parts of the states that overlap with the three zones included as separate attributes.

## Merge as an Editing Tool

The **Merge** tool in the Arc GIS Pro Geoprocessing toolbox or in the QGIS Processing Toolbox should not be confused with the Merge tool available in the Editing tools. 

```{note}
The equivalent tool is Edit Geometry in QGIS.
```

The latter Merge tool can be used to combine layers in similar fashion to the Geoprocessing **Merge** tool. However the Editing tool is more commonly used to merge multipart features into a single feature or attribute.

To merge multiple records in an attribute table into a single record in ArcGIS Pro, select the records and click Merge under Editing tools. Then save the edits.

```{note}
In QGIS, toggle editing mode on, select the records to merge, then navigate to Edit -> Edit Geometry -> Merge Selected Features. Then toggle editing mode off and save the edits.
```

## The Dissolve Tool

Another way to merge records into a single record is with the [Dissolve tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/dissolve.htm) in ArcGIS Pro.

```{note}
Use Dissolve under [Vector geometry](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorgeometry.html) in QGIS.
```

This tool will take a set of records that share a field and combine them into a single record. These records will be grouped based on that shared field For example, a feature class of U.S. counties could be dissolved based on a column named "state" to create a feature class of U.S. states. Or a feature class of excavation units could be dissolved to create a feature class of excavation operations.

The following shows a feature class of counties in the Southeast U.S.:

```{image} /images/southeastcounties.jpg
:alt: Southeast Counties
:class: bg-primary mb-1
:width: 80%
:align: center
```

When the Dissolve tool is run with the Dissolve Field set to state, all of the counties within each state are merged together:

```{image} /images/dissolvetool.jpg
:alt: Dissolve Tool
:class: bg-primary mb-1
:width: 80%
:align: center
```
<br>

```{image} /images/dissolvestate.jpg
:alt: Dissolve States
:class: bg-primary mb-1
:width: 80%
:align: center
```

## The Append Tool

The [Append Tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/append.htm) essentially shares the same functionality as the [Merge tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/merge.htm) with the important distinction that while the Merge tool creates a new output feature class, the Append tool adds the new fields to the existing input feature class, modifying the feature class. The Append tool, therefore, will override the original file.

```{note}
QGIS does not have a direct equivalent to the Append tool. Instead, use the Merge vector layers tool to create a new output. Another option is the [Append Features to Layer plugin](https://plugins.qgis.org/plugins/AppendFeaturesToLayer/). 
```
