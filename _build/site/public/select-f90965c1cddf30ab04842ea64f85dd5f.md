# Selecting Layers

We have seen previously that vector elements and records can easily be selected in ArcGIS Pro with the Select button available under Edit -> Selection by clicking the element on the map frame or by selecting the row in the feature class's attribute table. In QGIS, similar options are available in the Selection Toolbar, including Select Features by Area or Single Click. Multiple records can be selected in this manner by holding the shift key, and records can be unselected by holding the control or command keys. This approach generally suffices when selecting single or few records, but when needing to select several dozen records, tools are available to automate such tasks.

## Select Layer By Attribute

At times, we want to select records based on a specific attribute or field that they share. For example, we might want to select all counties in New York or all tools that are bifaces. A simple way to select such records is to reorder the relevant column in the attribute table, which in ArcGIS Pro can be done by right-clicking the column or field name in the attribute table, and clicking the option to sort in ascending or descending order (for text, this will sort from A to Z or Z to A, respectively, and for integer or float values, this will order the data numerically). Once ordered, you can scroll down to the desired entry and select all rows with that same data (they should all be adjacent to each other at this point). In QGIS, simply click on the column header in the attribute table once to sort in ascending order and a second time to sort in descending order.

Another method is to use the [Select Layer by Attribute tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/select-layer-by-attribute.htm) in ArcGIS Pro. This tool takes a feature class or table as input and an expression or set of expressions to define desired attributes to be selected. This tool does not modify the feature class but instead generates a temporary layer that can be used in subsequent analyses until a new selection is prompted or the Clear Selection option is clicked. The expression format typically involves defining where a specific field has a specific value, or numeric values above or below a specific value. The layer that is generated can be a new selection, added to an existing selection, or inverted to a new selection where the opposite of the expression is true. Several expressions can be combined using the options and/or. Once the tool is run, the relevant records will be highlighted in the attribute table and in the map frame. 

```{note}
In QGIS, use the Select by Attribute tool or the Select by expression tool under [Vector selection](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorselection.html). 
```

## Select Layer By Location

We also might want to select layers based not on a specific attribute but instead on a feature class's spatial relationship with another feature class. In ArcGIS Pro, the [Select Layer by Location tool](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/data-management/select-layer-by-location.htm) takes the desired feature class as an input, along with a selection feature class that will define the spatial relationship. The tool has several spatial relationship options, including intersect, entirely within, whose center is within, within a certain distance, etc. Once the tool is run, the relevant records will be highlighted in the attribute table and in the map frame. Determining the correct spatial relationship to select the appropriate records may take some trial and error.   

```{note}
In QGIS, use the Select by location or Select within distance tools under [Vector selection](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorselection.html).
```

## Exporting Selections

What do we do with the records now that they are selected? The layer can be set as the input to any tool, and the tool will only be applied to those selected features. Alternatively, we can export the selection to a new feature class to permanently separate these records from the original feature class (note that the records from the original feature class will be copied to a new feature class but remain in the original feature class; if you want to completely separate the two feature classes, you will have to delete the relevant records from the original feature class).

```{note}
In QGIS, the same selection tools are available with options to extract the selection to a new layer. These tools include Extract by attribute, Extract by expression, Extract by location, and Extract within distance and are available under [Vector selection](https://docs.qgis.org/3.44/en/docs/user_manual/processing_algs/qgis/vectorselection.html). 
```
