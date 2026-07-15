# Introduction to ArcScene

Digital terrain data is often better visualized three dimensionally. In ArcGIS Pro, ArcScene provides a user interface to model digital elevation models and derivatives in 3D. QGIS offers similar functionality in 3D Map Views.

## ArcScene

ArcScene can be opened from the ArcGIS Pro splash screen by selecting Local Scene under New Project. Alternatively, in an existing project, a new ArcScene can be added through Insert -> New Map -> New Local Scene.

The Contents of an ArcScene are more complicated than the Contents of a Map Frame. Contents are separated into 3D Layers, 2D Layers, and Elevation Surfaces. The Ground under Elevation Surfaces defaults to an ArcGIS Pro basemap.

To begin, add a DEM through Add Data. The raster layer will automatically be loaded as a 2D Layer. Using a mouse, you can rotate the scene by holding down the mouse scroll wheel and moving around. Alternatively, you can click the up arrow at the top left of the Navigator to select Show full control. If not visible, you can turn on the Navigator by right-clicking inside the scene and clicking Navigator.

The resulting 3D image is based on the elevation of the ArcGIS Pro basemap. To view the 3D image using the elevation values from the loaded digital elevation model, copy the layer from 2D Layers into Elevation Surfaces (by right-clicking copy). Then turn off the basemap under Elevation Surfaces. With Ground selected in the Contents, you can click Elevation Surface Layer at the top of the ArcGIS Pro window to make additional adjustments, including Vertical Exaggeration.

You can add additional 2D Layers, including feature classes and raster derivatives, which will be modelled in three dimensions over the selected Elevation Surface in the Contents.

## 3D Map View (QGIS)

In QGIS, 3D Map View is available under View -> 3D Map Views -> New 3D Map View. To drape a raster surface over a DEM, navigate to Configure -> Terrain. Change Type to DEM (Raster Layer), and select the appropriate Elevation source, then click Apply. Additional information on 3D Map Views in QGIS is available [here](https://docs.qgis.org/3.44/en/docs/user_manual/map_views/3d_map_view.html).