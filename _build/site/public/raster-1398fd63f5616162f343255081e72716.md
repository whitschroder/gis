# Introduction to Raster Tools

Raster data in GIS refers to imagery displaying continuous data in pixels or cells. Rasters can be interpreted as tabular data where each pixel has a horizontal location, resolution, and a value (or digital number). The data is best visualized in this format when output as a text file, for example using the [Raster to ASCII tool](https://pro.arcgis.com/en/pro-app/latest/tool-reference/conversion/raster-to-ascii.htm) in ArcGIS Pro or Raster -> Conversion -> Translate (Convert Format) in QGIS setting the output file extension to .asc.

The following table represents a digital elevation model raster:

```{image} /images/ascii.jpg
:alt: Raster ASCII
:class: bg-primary mb-1
:width: 80%
:align: center
```

In this example, the table is defined by 9 columns and 7 rows. The location of the raster is defined by the coordinate of the lower left corner cell, and the resolution as cellsize (measured in degrees). The NODATA value is assigned the arbitrary value -9999. The additional values all represent the value of each pixel, each known as a digital number.

When viewed as an image, the digital elevation model has the following digital numbers displayed along a grayscale. Each digital number represents the elevation in meters at that location:

```{image} /images/Rplot.jpeg
:alt: Rplot
:class: bg-primary mb-1
:width: 80%
:align: center
```

Here is another example, but this raster image represents a black and white photo where the digital numbers represent the relative brightness or darkness of the photo:


```{image} /images/rasterdn.jpg
:alt: Digital Numbers
:class: bg-primary mb-1
:width: 80%
:align: center
```
Source: <https://gsp.humboldt.edu/olm/Courses/GSP_216/online/lesson5/raster-models.html>

The following digital numbers represent inches of precipitation (left) and ground cover type (right). In the right example, the data are categorical rather than continuous.

```{image} /images/Rplot1.jpeg
:alt: Digital Numbers
:class: bg-primary mb-1
:width: 80%
:align: center
```

## No Data

A critical concept in raster GIS is that at times no data is available in a particular cell. Note that No data is not the same as zero.

No data can occur when there is a gap in data at that specific location, or the data are outside the boundaries of the region of interest.

In the following example, the raster image is not rectangular:

```{image} /images/bene.jpg
:alt: Benemerito
:class: bg-primary mb-1
:width: 30%
:align: center
```

However, the symbology here is misleading because, in reality, the raster image is rectangular. Under Symbology -> Mask, we can assign a background color (in this case black), which applies to No Data areas. We can do the same in QGIS by right-clicking the layer in Layers, selecting Properties -> Transparency, and under NoData Value, setting a value and the display color for NoData.

```{image} /images/bene2.jpg
:alt: Benemerito
:class: bg-primary mb-1
:width: 30%
:align: center
```

So, in fact, the raster is rectangular. Areas outside of the region of interest have been assigned No Data. In addition, we can also see that some areas inside the region of interest have the same No Data value. These are areas where no elevation data is available. If we use the Explore tool in ArcGIS Pro (Identify Features in QGIS) to identify the values in these locations, we will see they are assigned NoData.

```{image} /images/nodata.jpg
:alt: NoData
:class: bg-primary mb-1
:width: 80%
:align: center
```

NoData, however, is not actually a numeric value but rather a character string. In reality, NoData values are assigned an actual numeric value. We can view this value in ArcGIS Pro by right-clicking the layer in Contents and opening Properties. Under Source -> Raster Information, we see in this case the NoData value is 91919. In QGIS, we can right-click the layer in Layers and go to Properties -> Information. Scrolling down to the Bands section, we can view the NoData value.

```{image} /images/rasterprop.jpg
:alt: Raster Properties
:class: bg-primary mb-1
:width: 80%
:align: center
```

In our previous example above, however, we saw that NoData was assigned the value -9999:

```{image} /images/rasterprop1.jpg
:alt: Raster Properties
:class: bg-primary mb-1
:width: 80%
:align: center
```

NoData, therefore, must be defined with a numeric value. However, when defining NoData, we have to select a value that is outside of the range of our data. In the last two examples, we had not elevation data equal to 91,919 meters or -9,999 meters, so we could arbitrarily select those values to represent NoData. We cannot just choose any random value, however; we must ensure the value is within the bit depth of our raster.

## Bit Depth

We can also see additional information in the previous examples, namely pixel depth. In QGIS, pixel depth is visible in Layer Properties -> Information under Information from provider and Data type. In one example, pixel depth is 32 bit floating point, and in the other example pixel depth is 32 bit signed integer. These categories refer to the range of possible values in our rasters. Just as when we create a new field in a feature class attribute table or a standalone table, we have to define the type of data, including text, numeric, integer, or floating point (decimals), alongside the length and precision. For raster, we can only define numeric values. The following are the most common bit depths seen in GIS. As a rule of thumb, we can calculate the range of possible values by raising 2 to the power of the bit.

1 Bit -- 2<sup>1</sup> possible values, or 2 total values, only positive integers. This pixel depth represents binary data that stores only values of 0 and 1. If NoData were to be defined in this example, the value would have to be either 0 or 1, which would leave only a single possible value for the raster grid.  

2 Bit -- 2<sup>2</sup> possible values, or 4 total values, only positive integers. Data ranges from 0 to 3.  

4 Bit -- 2<sup>4</sup> possible values, or 16 total values, only positive integers. Data ranges from 0 to 15.  

8 Bit unsigned -- 2<sup>8</sup>, or 256 total values, only positive integers. The range of 8 bit unsigned data is usually 0 to 255, with either 0 or 255 assigned to NoData. This pixel depth is most commonly used with grayscale photos and imagery (when using 3 bands, these data can be displayed with RGB values).  

8 Bit signed -- 2<sup>8</sup>, or 256 total values, including negative and positive integers. The data range is -128 to 127. NoData could be assigned either -128 or 127. 
 
16 Bit unsigned -- 2<sup>16</sup>, or 65,536 total values, only positive integers. The range is 0 to 65,535. NoData would likely be assigned either 0 or 65,535.  

16 Bit signed -- 2<sup>16</sup>, or 65,536 total values, including negative and positive integers. The range is -32768 to 32767. In this example, NoData could be assigned the value -9999 because it is in range of the data, or NoData could be assigned the minimum or maximum values of the range, -32768 or 32767.  

32 Bit unsigned -- 2<sup>32</sup>, or 4,294,967,296 total values, only positive integers. The range is 0 to 4,294,967,295.  

32 Bit signed -- 2<sup>32</sup>, or 4,294,967,296 total values, including negative and positive integers. The range is -2147483648 to 2147483647.  

32 Bit float -- 2<sup>32</sup>, or 4,294,967,296 total values; the only pixel depth that can handle decimals. Data ranges from -3.402823466e+38 to 3.402823466e+38.  

64 Bit unsigned -- 2<sup>64</sup>, or 18,446,744,073,709,551,616 total values, only positive integers. Data ranges from 0 to 18446744073709551616.

ArcGIS Pro and QGIS will generally automatically select the appropriate pixel depth for the data being used, but it is useful to keep pixel depth in mind. Higher pixel depths take up more memory, and large rasters with a high pixel depth can be huge files, so use only the pixel depth necessary to contain your range of digital numbers. Note that 32 Bit float will likely be the most common pixel depth used, but 8 bit and 16 bit unsigned are also very common.
