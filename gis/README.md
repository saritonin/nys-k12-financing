## Instructions for downloading Census shapefiles
Main website for Census shapefiles: https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

First, choose the appropriate year for the shapefiles you'd like.  Because I'm starting with school fiscal year 2019-20, I chose to use the [2020 shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.2020.html).

You can either use the web interface or the FTP archive to download files, or can choose to download a Complete Set of Shapefiles by State near the bottom of the page.
The entire NY set of shapefiles comes to about 1.6 GB zipped (4.1 GB unzipped), so it makes a lot more sense to just download the files you need; in our case the county and unified school district files are the ones we are interested in.

For the [web interface](https://www.census.gov/cgi-bin/geo/shapefiles/index.php), choose the year first and then the type of shapefile.
- Select year: 2020
- Select a layer type: Counties (and equivalent)
- Submit

The national file is fine for our purposes, even though we are only interested in NY.
I took the national file into QGIS and stripped out all the non-NY data, and am including it in this directory.


