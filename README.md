# nys-k12-financing
## Latest Updates
This is work in progress.  Here are the latest updates and current areas of focus:
- ✅ Geographic data shapefiles and metadata for counties, school districts, and their intersection
- ✅ Census SAIPE data
- 🔜 Census Annual Survey of School System Finances

## Abstract
Information about public financing for New York’s K-12 schools is spread across multiple data sources, including the U.S. Census Bureau, the U.S. Department of Education, and the New York State Education Department (NYSED).  This data model brings together these disparate data sources to get a more holistic view of public financing for K-12 schools in New York.

School year 2019-2020 data was retrieved from the sources listed below along with appropriate data dictionaries and technical documentation.  For each data set, data elements were categorized and analyzed in three main areas: geospatial boundaries, finances (revenues and expenditures), and demographics.  Grouped data elements were consolidated following dimensional modeling standards and best practices (Kimball & Ross, 2013).

# Geography
## Geographic Boundaries 
School district boundary information is updated annually via the [School District Review Program](https://www.census.gov/programs-surveys/sdrp.html).  The resultant GIS data is available via the Census Bureau's TIGER/LINE Shapefiles or via the NCES Education Demographic and Geographic
Estimates (EDGE) Program website.
- [TIGER/Line Shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)
- [TIGER/Line Documentation](https://www.census.gov/programs-surveys/geography/technical-documentation/complete-technical-documentation/tiger-geo-line.html)
- [NCES EDGE Program](https://nces.ed.gov/programs/edge/Geographic/DistrictBoundaries)
- [NCES EDGE Documentation](https://nces.ed.gov/programs/edge/docs/EDGE_SDBOUNDARIES_COMPOSITE_FILEDOC.pdf)

### Geographic Relationships
School districts don't fit into standard geographic hierarchies at all.  They can cross state lines, counties, cities, towns, villages, and even a single Census block may have multiple school districts within its boundaries.  NCES provides a set of relationship files to help determine how school districts overlap with other entities.
- [Geographic relationship files](https://nces.ed.gov/programs/edge/Geographic/RelationshipFiles)

### Geographic Metadata
In the census_gis_counties table provided in this data set, the Statewide (GEOID=36000) INTPTLAT and INTPTLON come from the Census bureau's [State Area Measurements and Internal Point Coordinates](https://www.census.gov/geographies/reference-files/2010/geo/state-area.html).  However, the area calculations were done by summing the respective columns (ALAND and AWATER) to provide data that is consistent with the 2020 SDRP GIS files.

# Finances
## US Census Bureau
### Annual Survey of School System Finances
- [Landing page](https://www.census.gov/programs-surveys/school-finances.html)
- [Data tables](https://www.census.gov/programs-surveys/school-finances/data/tables.html)
- [Documentation](https://www.census.gov/programs-surveys/school-finances/technical-documentation.html)

# Demographics
## US Census Bureau
### Small Area Income and Poverty Estimates
- [Landing page](https://www.census.gov/programs-surveys/saipe.html)
- [Data tables](https://www.census.gov/programs-surveys/saipe/data/datasets.html)
- [Documentation](https://www.census.gov/programs-surveys/saipe/technical-documentation.html)
- [Guidance for data users](https://www.census.gov/programs-surveys/saipe/guidance.html)

### American Community Survey – Education Tabulation (ACS-ED)
- [ACS Data](https://www.census.gov/programs-surveys/acs/data.html)
- [ACS Documentation](https://www.census.gov/programs-surveys/acs/technical-documentation.html)
To download the ACS Data tables, I used data.census.gov.
1. Geography: School Districts (Unified) > New York > All = https://data.census.gov/all?g=040XX00US36$9700000 
2. Surveys: American Community Survey > 5-Year Estimates > Data Profiles = https://data.census.gov/all?g=040XX00US36$9700000&d=ACS+5-Year+Estimates+Data+Profiles

## National Center for Education Statistics
