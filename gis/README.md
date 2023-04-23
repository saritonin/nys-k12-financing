## Instructions for downloading Census shapefiles
Main website for Census shapefiles: https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

First, choose the appropriate year for the shapefiles you'd like.  <br />
Because I'm starting with school fiscal year 2019-20, I chose to use the [2020 shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2020.html).

You can either use the web interface or the FTP archive to download files, or can choose to download a Complete Set of Shapefiles by State near the bottom of the page.
The entire NY set of shapefiles comes to about 1.6 GB zipped (4.1 GB unzipped), so it makes a lot more sense to just download the files you need; in our case the county and unified school district files are the ones we are interested in.

### tl_2020_us_county.zip
For the [web interface](https://www.census.gov/cgi-bin/geo/shapefiles/index.php), choose the year first and then the type of shapefile.
- Select year: 2020
- Select a layer type: Counties (and equivalent)
- Submit

For the [FTP archive](https://www2.census.gov/geo/tiger/TIGER2020/)
- [COUNTY/](https://www2.census.gov/geo/tiger/TIGER2020/COUNTY/)
- tl_2020_us_county.zip

The national file of counties is fine for our purposes, even though we are only interested in NY.

### tl_2020_36_county.zip
I took the national file into QGIS and stripped out all the non-NY data.  See below for step-by-step instructions to recreate this file.

### tl_2020_36_unsd.zip
The [web interface](https://www.census.gov/cgi-bin/geo/shapefiles/index.php) lets you choose an individual state for school districts:
- Select year: 2020
- Select a layer type: School Districts
- Submit
- Unified School District (current) / Select a state: New York
- Download

The [FTP archive](https://www2.census.gov/geo/tiger/TIGER2020/) is arranged by [FIPS code](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code).
- [UNSD/](https://www2.census.gov/geo/tiger/TIGER2020/UNSD/)
- tl_2020_36_unsd.zip

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
12. Format: ESRI Shapefile<br />File name: tl_2020_36_county.shp<br />CRS: EPSG:4269 - NAD83 <-- All Census files should already have this CRS.
13. Put all resulting files into a single folder and zip it.

### Creating an intersection file for counties and school districts
1. Double-click each .shp file in your file browser to open layers tl_2020_36_county and tl_2020_36_unsd in the same QGIS project. 
2. Vector > Geoprocessing tools > Intersection
3. Input layer: tl_2020_36_county [EPSG:4269]<br />Overlay layer: tl_2020_36_unsd [EPSG:4269] <br /> Advanced Parameters > Overlay fields prefix [optional]: UNSD_<br /> [✓] Open output file after running algorithm<br />Run

Output: 
```QGIS version: 3.30.0-'s-Hertogenbosch
QGIS code revision: f186b8efe0
Qt version: 5.15.2
Python version: 3.9.5
GDAL version: 3.3.2
GEOS version: 3.9.1-CAPI-1.14.2
PROJ version: Rel. 8.1.1, September 1st, 2021
PDAL version: 2.3.0 (git-version: Release)
Algorithm started at: 2023-04-23T12:19:11
Algorithm 'Intersection' starting…
Input parameters:
{ 'GRID_SIZE' : None, 'INPUT' : '/tl_2020_36_county.shp', 'INPUT_FIELDS' : [], 'OUTPUT' : 'TEMPORARY_OUTPUT', 'OVERLAY' : '/tl_2020_36_unsd.shp', 'OVERLAY_FIELDS' : [], 'OVERLAY_FIELDS_PREFIX' : 'UNSD_' }

Creating spatial index
Calculating intersection
Execution completed in 1.78 seconds
Results:
{'OUTPUT': 'Intersection_b98716c9_3ead_45f2_8b99_a7bb49d0f104'}

Loading resulting layers
Algorithm 'Intersection' finished
```

4. Vector > Geometry Tools > Add Geometry Attributes
5. Input layer: Intersection<br />Calculate using: Layer CRS<br /> [✓] Open output file after running algorithm<br />Run

Output:
```QGIS version: 3.30.0-'s-Hertogenbosch
QGIS code revision: f186b8efe0
Qt version: 5.15.2
Python version: 3.9.5
GDAL version: 3.3.2
GEOS version: 3.9.1-CAPI-1.14.2
PROJ version: Rel. 8.1.1, September 1st, 2021
PDAL version: 2.3.0 (git-version: Release)
Algorithm started at: 2023-04-23T12:22:44
Algorithm 'Add geometry attributes' starting…
Input parameters:
{ 'CALC_METHOD' : 0, 'INPUT' : 'memory://MultiPolygon?crs=EPSG:4269&field=STATEFP:string(2,0)&field=COUNTYFP:string(3,0)&field=COUNTYNS:string(8,0)&field=GEOID:string(5,0)&field=NAME:string(100,0)&field=NAMELSAD:string(100,0)&field=LSAD:string(2,0)&field=CLASSFP:string(2,0)&field=MTFCC:string(5,0)&field=CSAFP:string(3,0)&field=CBSAFP:string(5,0)&field=METDIVFP:string(5,0)&field=FUNCSTAT:string(1,0)&field=ALAND:long(14,0)&field=AWATER:long(14,0)&field=INTPTLAT:string(11,0)&field=INTPTLON:string(12,0)&field=UNSD_STATEFP:string(2,0)&field=UNSD_UNSDLEA:string(5,0)&field=UNSD_GEOID:string(7,0)&field=UNSD_NAME:string(100,0)&field=UNSD_LSAD:string(2,0)&field=UNSD_LOGRADE:string(2,0)&field=UNSD_HIGRADE:string(2,0)&field=UNSD_MTFCC:string(5,0)&field=UNSD_SDTYP:string(1,0)&field=UNSD_FUNCSTAT:string(1,0)&field=UNSD_ALAND:long(14,0)&field=UNSD_AWATER:long(14,0)&field=UNSD_INTPTLAT:string(11,0)&field=UNSD_INTPTLON:string(12,0)&uid={5b98ba4d-34b9-44f9-b12d-1ab95a8c6bd1}', 'OUTPUT' : 'TEMPORARY_OUTPUT' }

Execution completed in 0.25 seconds
Results:
{'OUTPUT': 'Added_geom_info_84d01dd2_425b_4d5d_a081_ce24a0365bec'}

Loading resulting layers
Algorithm 'Add geometry attributes' finished
```

6. Save the new "Added geom info" layer. Layer > Save As..
7. Format: ESRI Shapefile<br />File name: tl_2020_36_county_unsd_intersect.shp<br />CRS: EPSG:4269 - NAD83 <-- All Census files should already have this CRS.
8. Put all resulting files into a single folder and zip it.

### Extracting metadata from any shapefile
1. Open the shapefile in QGIS.
2. Layer > Save As...
3. Format: Comma Separated Value [CSV]<br /> File name: my_shapefile_attributes.csv<br />OK
