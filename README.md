# Python Processing Tools for QGIS </br>
**SUMMARY:** </br>
This repository contains Python Processing Tools for QGIS.  Similar to ArcGIS, these tools are self-contained Python (**.py**; or ***.pyt*** in ArcGIS) files that are formatted to create Processing Tools in the QGIS Processing Toolbox.</br></br>
Step by Step instructions will be provided below, but to enable tools on QGIS you must download these Python (**.py**) files to your computer, and move them to the `...processing/scripts` directory in QGIS file structure This will activate them for use in QGIS directly through the Processing Toolbox as a GUI.  Note that each Python Script is self-contained and formatted to work with QGIS Processing Toolbox. </br>*These were developed on QGIS 3.34.7 in June 2024.* </br></br>
This README will serve as reference for these and future QGIS Python Processing Tools, and serve as a Tutorial to use tools within QGIS.</br></br>
**WHY?**</br>
- No intermediary files
- Process entire directories full of tiles quickly and interactively
- Efficiency and Replicable Workflow


## General Workflow: Tile and Mosaic </br>
*The current (June 2024) files should be used sequentially to:*</br>
1) `create_gdal_input_file.py`: Create a text file itemizing raster files in a directory.
2) `gdaltindex_from_list.py`:   From text file in Step 1, create tile index shapefile
3) `gdalbuildvrt_from_slxn.py`: From index file, create Virtual Raster (.vrt) with option to interactively select tiles to mosaic. </br>

At this point, the VRT can be used directly OR to:
1) reproject
2) resample (i.e. 3m to 6m)
3) clip
4) ...anything possible in [gdalwarp](https://gdal.org/programs/gdalwarp.html)

## Download Tools</br>
- Before procededing, DOWNLOAD this GitHub Repository and copy the 3 python scripts to QGIS script location.</br>
*NOTE: This only needs to be done ONE time!* </br></br>
SAVE PYTHON SCRIPTS HERE:</br>
---> <ins>General Path:</ins>   C:\Users\<**YOUR_USERNAME**>\AppData\Roaming\QGIS\QGIS3\profiles\default\processing\scripts </br>
---> <ins>Example Path:</ins>  C:\Users\\**UhlmannZachary**\AppData\Roaming\QGIS\QGIS3\profiles\default\processing\scripts </br>
![step1](https://github.com/zuhlmann/markdown_images/blob/assets/qgis_processing_tools/scripts_qgis.png) </br></br>

## Tutorial: Tile and Mosaic
### 1. `gdal_input_file` <br>
Create a text file itemizing raster files in a directory. </br>
**Parameters:**
- <ins>Filename</ins> <Output File Name> i.e. `wallowa_tiles` </br>
- <ins>Raster Type</ins> Simply a file extension to filter search in folder. Dropdown is currently limited to `.tif` and `.vrt`</br>
- <ins>Full Filepath Checkbox:</ins> Want `full/file/path/tile.tif` to tiles contained or just filename, i.e.`tile.tif`</br> 
CHECKED   = `full/pathto/tile.tif` will be written to `location` field in index file (shapefile) attribute table </br>
UNCHECKED = Only the filename will be written to `location` field </br>
- <ins>Output Directory</ins>
  - This Parameter will be both **1)** the directory containing the input rasters, and **2)** the output directoy for the output from this tool: a list of all files in this directory</br>
  - The Path provided below contains sample data to use for this tutorial: *10 small DEMs from Wallowa Dam area in OR from the USGS* </br>
  `C:\Box\MCMGIS\GIS_Data\tutorials\qgis_processing_tools\gdal_utils_mosaics\tiles` </br>
  
![step1](https://github.com/zuhlmann/markdown_images/blob/assets/qgis_processing_tools/gdal_input_file1.png) </br></br>
  
**Results**</br>
Text File listing `full/path/` to all tiles in `Output Directory`

### 2. `gdaltindex_from_list` </br>
From list, create tile index shapefile</br>
**Parameters:**
- <ins>Input File</ins> select `.txt` file from Step1 </br>
- <ins>Filename for Index</ins> Filename for shapefile - i.e. `wallowa_tiles_idx`</br>
- <ins>Select Output Directory to save Index File</ins></br>

![step1](https://github.com/zuhlmann/markdown_images/blob/assets/qgis_processing_tools/gdaltindex_from_list.png) </br></br>

**Results**</br>
Index Files with one feature per tile contained in `Output Directory`.  Each feature's geometry (polygon) are the bounding extents of tile.

### 3. `gdalbuildvrt_from_slxn`
From index file, create Virtual Raster (.vrt) with option to interactively select tiles to mosaic. </br>
**Parameters:**
- <ins>Input Layer</ins> Ideally load Index File from Step2 into map, and select shapefile from dropdown. Can also Browse to File </br>
- <ins>Select features only</ins> **Note - only available if features selected from attribute table</br> 
CHECKED   = Create VRT from ONLY selected features</br>
UNCHECKED = Create VRT from ALL features in Index File</br>
- <ins>Filename for Index</ins> Output Name for VRT file - i.e. `2015_OLC_Wallowa_3DEP_AOI_15ft`</br>
- <ins>Select Output Directory to save Index File</ins> Where the file will be saved </br>

![step1](https://github.com/zuhlmann/markdown_images/blob/assets/qgis_processing_tools/wallowa_index_composite.png) </br></br>
![step1](https://github.com/zuhlmann/markdown_images/blob/assets/qgis_processing_tools/gdalbuildvrt_from_slxn.png) </br></br>

**Results**</br>
A Virtual Raster (.vrt; text file) created from selected or all tiles in Index File.  </br>

### 4. Use VRT as input file for all QGIS Raster Processing Tools: `Hillshade`, `Clip by Raster Extent` (gdal_translate), `Warp` (gdalwarp)
**Now you can easily:**
- Reproject
- Clip to Canvas 
- Clip to Shapefile 
- Upsample or Downsample Spatial Resolution
- Assign `NaN`
- and quite a bit more!


