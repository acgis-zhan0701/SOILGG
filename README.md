## Project

Predicted Soil Great Groups Result for Different Ecological Framework

### Description

User uses the selected R tools and packages to extract soil great group information at four different level of ecological framework.
Four ecological zones are: ecozone, ecoprovince, ecoregion, ecodistrict.

### Requirement

Make sure you have R Studio installed on your computer, you can download R Studio from https://www.rstudio.com/products/rstudio/download/.

### R packages

This project requires six open source packages, as shown below:

1. raster          
2. sf                
3. foreign           
4. exactextractr
5. dplyr
6. data.table

 - Raster::raster tool is used to create a raster layer file from an existing file.
 - sf:: st_read tool is used to read shapefile.
 - foreign::wrtie.dbf tool is used to write a dataframe to a .dbf file.
 - exactextractr::extract tool is used to extract value from raster layer. 
 - dplyr and data.table tools are used for sorting and converting list to dataframe.

### Input Data

1. "pred_class_majority.tif". This soil great group predicted result is produced by Juanxia (2019).
2. "soil_great_group_code.csv". This excel file contains soil great group code and great group class name. This excel file is produced by Juanxia (2019).
3. GIS datasets for the different ecological zones. GIS dataset is produced by CanSIS, https://sis.agr.gc.ca/cansis/nsdb/ecostrat/gis_data.html
	- "Ecozone_shp.zip"
	- "Ecoprovince_shp.zip"
	- "Ecoregion_shp.zip"
	- "Ecodistrict_shp.zip"

### Usage

First load packages
```html
library(raster)
library(sf)
library(foreign)
library(exactextractr)
library(dplyr)
library(data.table)
```

If you want to use your own input DEM file or ecological framework file, change the file path to yours.
Example of the format of file path: "C:\\YOUR\\FILE\\PATH.shp"
```html
ecozone <- st_read("your file path") 
```

### Attributes
Output table contains four attributes, including:
| Name          | Description   |
| ------------- |:-------------:|
| ECOXXXX    | Ecological Area ID |
| MIN_ELEV     | Minimum Elevation      |
| code_ID | Soil Great Group Code      |
| GG_Class | Great Group Name     |
| A_Coverage | Percentage of area coverage      |




### Output File

Output files will be named as follows: <br />
	- "zn_soilgg.dbf" for Ecozone <br />
	- "pr_soilgg.dbf" for Ecoprovince <br />
	- "rg_soilgg.dbf" for Ecoregion <br />
	- "dt_soilgg.dbf" for Ecodistrict
  
### Note
1.
Only top three of area percentage are reported in the output file, which does not include NA.  <br />
2.
Estimate processing time can depend on which framework layer that you are choosing. <br />
For ecozone, estimate processing time is 8 minutes. <br />
For ecoprovince, estimate processing time is 7 minutes. <br />
For ecoregion, esitimate processing time is 5 minutes. <br />
For ecodistrict, estimate processing time is 5 minutes. <br />
3.
Exactextractr::extract tool does not support Points vertor data when extracting values from raster layer. 
If you want to extract information from raster layers as points, raster::extract and terra:extract are both support points data.

Speed comparsion for raster::extract, terra:extract and exactextractr:extract. Source:https://tmieno2.github.io/R-as-GIS-for-Economists/extract-speed.html
raster::extract is the slowest.
If you have a small size raster layer (province wide), terra::extract would be the fastest.
If you have a large size raster layer (whole country), exactextractr::extract is the best choice. 
