# Introduction to Automation for GIS

With larger projects, you might want to apply the same set of tools or workflow to different input data, or you might want to design your own tools. Doing so involves automation, typically using Python coding or scripting. However, ArcGIS Pro and QGIS offer simpler interfaces that serve as an introduction to automation.

## Batch Processing

Batch processing refers to applying a single tool with defined parameters to multiple inputs. For example, you may have dozens or hundreds of digital elevation models, and you may want to generate hillshades for each one. Or you might have hundreds of site boundaries or point locations, and you would like to create a 100 m buffer around them. Rather than using the tedious process of running each tool on each input, you can automate the process using batch processing.

Batch processing in ArcGIS Pro is straightforward. When running a tool, rather than clicking on the tool to run it a single time, right-click and select Batch. You will then be able to select the batch parameter, which is the parameter that will vary across inputs. This parameter is typically the input features or the input rasters if the tool is going to be run on several files. Alternatively, any parameter within the tool can be used as the batch parameter. For example, when running Buffer as a batch process, the batch parameter can be the Input Features, in which for each input feature, a buffer will be output with the same settings. Alternatively, the batch parameter can be distance. In this case, a single input feature would be used, but an output buffer would be generated at several different distances. After choosing the input batch parameter and clicking Next, the standard tool interface loads, where the inputs and parameters can be defined.

In contrast, the batch processing interface in QGIS uses a parameters table. In this table, the settings must be chosen for each input dataset. More information is available at the [batch processing interface page](https://docs.qgis.org/3.44/en/docs/user_manual/processing/batch.html).

## ArcGIS Modelbuilder

Batch processing typically only allows a single parameter to vary across large datasets. For more flexibility, ArcGIS Pro provides the graphic Modelbuilder interface to construct complex workflows.

## QGIS Model Designer

Automating workflows is available in QGIS using a slightly different interface. More information is available at the [Model Designer](https://docs.qgis.org/3.44/en/docs/user_manual/processing/modeler.html).