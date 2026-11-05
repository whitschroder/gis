# Lab 8: Least Cost Analysis

In this lab, students will conduct a least cost analysis.

The data for this week's lab includes:

1. ASTGTMV003_N14W092_dem.tif -- an ASTER DEM
2. sites.shp -- point feature class representing archaeological sites
3. hotosm_gtm_waterways_lines_shp -- polyline feature class representing rivers
4. cuerpos_agua_gtm.shp -- polygon feature class representing water bodies

Conduct a cost distance analysis of travel from San Andres Semetebaj to the other archaeological sites. Assume that all travel is by land, aside from river crossings (no travel over lakes). Generate the following:

1. A cost distance surface showing 4-hour travel time from San Andres Semetebaj, based on the Tobler function. How many sites are within this radius?
2. A set of least cost paths connecting all sites to San Andres Semetebaj. You can select any parameters, and you may optionally incorporate direction of travel. Explain your parameters and workflow.
