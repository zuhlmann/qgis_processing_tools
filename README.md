# Python Processing Tools for QGIS </br>
**SUMMARY OF WORKFLOW:** This repository contains Python Processing Tools for QGIS.  Similar to ArcGIS, these tools are self-contained Python (**.py**; or ***.pyt*** in ArcGIS) files that are formatted to create Processing Tools in QGIS the Processing Toolbox.
Instructions will be provided below, but essentially you will download these Python (**.py**) files to your computer, and move them to the `...processing/scripts` directory in QGIS file structure and simply use them from QGIS directly in their Processing Toolbox.  
This README will serve as reference for these and future QGIS Python Processing Tools, and serve as a Tutorial to use tools within QGIS.

Each Python Script should be self-contained and formatted to work with QGIS Processing Toolbox. These were developed on QGIS 3.34.7 in June 2024.

## Tiling and Mosaicing </br>
*The current (June 2024) files should be used sequentially to:*</br>
1) `create_gdal_input_file.py`: Create a text file itemizing raster files in a directory.
2) `gdal_from_slxn.py`:         From text file in Step 1, create tile index shapefile
3) `gdalbuildvrt_from_slxn.py`: From index file, create Virtual Raster (.vrt) with option to interactively select tiles to mosaic. </br>

At this point, the VRT can be used directly OR to:
1) reproject
2) resample (i.e. 3m to 6m)
3) clip
4) ...anything possible in [gdalwarp](https://gdal.org/programs/gdalwarp.html)

### 1. Download this GitHub Repository and save python scripts to QGIS script location:</br>
*NOTE: This only needs to be done ONE time!*</br>
C:\Users\<**YOUR_USERNAME**>\AppData\Roaming\QGIS\QGIS3\profiles\default\processing\scripts </br>
ADD PHOTO </br>
### 2. Create text file inventorying sample data </br>
- 
