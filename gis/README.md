## Instructions for downloading Census shapefiles
Main website for Census shapefiles: https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

First, choose the appropriate year for the shapefiles you'd like.  <br />
Because I'm starting with school fiscal year 2019-20, I chose to use the [2020 shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2020.html).

You can either use the web interface or the FTP archive to download files, or can choose to download a Complete Set of Shapefiles by State near the bottom of the page.
The entire NY set of shapefiles comes to about 1.6 GB zipped (4.1 GB unzipped), so it makes a lot more sense to just download the files you need; in our case the county and unified school district files are the ones we are interested in.

For the [web interface](https://www.census.gov/cgi-bin/geo/shapefiles/index.php), choose the year first and then the type of shapefile.
- Select year: 2020
- Select a layer type: Counties (and equivalent)
- Submit

The national file of counties is fine for our purposes, even though we are only interested in NY.<br />
I took the national file into QGIS and stripped out all the non-NY data, and am including it in this directory.<br />
Directory file: tl_2020_36_county.zip

The web interface lets you choose an individual state for school districts:
- Select year: 2020
- Select a layer type: School Districts
- Submit
- Unified School District (current) / Select a state: New York
- Download
Directory file: tl_2020_36_unsd.zip

## Instructions for QGIS transformations
### Deleting non-NY counties from the national file
1. Unzip tl_2020_us_county.zip
2. Open tl_2020_us_county.shp in QGIS
3. Edit > Select > Select Features by Value 
4. STATEFP 36 Not equal to 
5. Select Features
6. Layer > Toggle Editing
7. Edit > Delete Selected
8. "3172 selected features are about to be deleted. Would you like to continue?" Delete 3172 Features
9. Layer > Save Layer Edits
10. Layer > Toggle Editing
11. Layer > Save As..
12. Format: ESRI Shapefile<br />File name: tl_2020_36_county.shp<br />CRS: EPSG:4269 - NAD83
13. Put all resulting files into a single folder and zip it.

### Creating an intersection file for counties and school districts

