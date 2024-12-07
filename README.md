# Analysis of Blackouts in Houston, Texas
![Image](https://s.hdnux.com/photos/01/24/10/56/22055870/6/rawImage.jpg)
Image Credit: Brett Coomer, Houston Chronicle

### Purpose 
This repository aims to investigate household blackouts in Houston, Texas due to storms in February 2021. Climate change is increasing extreme weather events all over the world. In February of 2021, three winter storms transversed the United States on the 10th-11th, 13th-17th, and 15th-20th. During this storm surge, Houston, Texas was affected with a number of household blackouts throughout the city. 

This analysis will use remotely-sensed night light data from the [Visible Infrared Imaging Radiometer Suite (VIIRS)](https://en.wikipedia.org/wiki/Visible_Infrared_Imaging_Radiometer_Suite) on the Suomi satellite. This data will be paired with US Census Bureau data to investigate whether or not the number of homes in Houston was felt disproportionately throughout socioeconomic groups. 

### Structure
```{r}
houston-blackouts  
│   .gitignore
|   README.md
|   houston-blackouts.Rproj
│   houston-blackouts.html
│   houston-blackouts.qmd
│
└── houston-blackouts_files
```

### Highlights of Analysis
- Load in geospatial data using `sf` and `stars`
- Merge rasters with `st_mosaic`
- Create blackout `mask` of Houston
- Exclude highways using `st_buffer`
- Identify households homes affected by blackouts
- Identify census tracts affected by blackouts
- Map households and census tracts that experienced blackouts
- Compare `histograms` of median incomes of households that did and didn't experience blackouts

### Dataset Descriptions

#### Night Light Data
The night light data used is from February 7th, 2021 and February 16th, 2021 because these dates compare Houston before and after the storm without strong cloud coverage. NASA's [Level-1 and Atmospheric Archive & Distribution System Distributed Active Archive Center (LAADS DAAC)](https://ladsweb.modaps.eosdis.nasa.gov/) collects VIIRS data that will be used in this repository. This data is distributed in 10x10 degree tiles in sinusoidal equal-area projection. Two tiles per date are used because Houston is inbetween tiles h08v05 and h8v06.

#### Roads data
For our roads data, we used a shapefile from [Geofabrik's download sites](https://download.geofabrik.de/) that was subsetted for roads that intersected with the Houston area. Original road data was taken from the [OpenStreetMap (OSM)](https://planet.openstreetmap.org/), but as this was a large file, Geofabrik's data was used instead. 

#### Houses
Likewise with the roads, houses data was downloaded from [Geofabrick](https://download.geofabrik.de/) as a subset of [OpenStreetMap](https://planet.openstreetmap.org/).

#### Socioeconomic
We used 2019 census tract data from the [U.S. Census Burea's American Community Survey](https://www.census.gov/programs-surveys/acs). The folder used was `ACS_2019_5YR_TRACT_48.gdb` which is an ArcGIS [file geodatabase](https://desktop.arcgis.com/en/arcmap/latest/manage-data/administer-file-gdbs/file-geodatabases.htm). The geometry layer `ACS_2019_5YR_TRACT_48_TEXAS` was extracted and used for comparioson with census tracts. 

### Refereces and Acknowledgements 

Menzel, W.P., Frey, R.A., and Baum, B.A. (2015). Terra/MODIS Cloud Product 5-Min L2
Swath 1 km and 5 km, C6, NASA Level-1 and Atmosphere Archive & Distribution System
(LAADS) Distributed Active Archive Center (DAAC), Goddard Space Flight Center,
Greenbelt, MD. http://dx.doi.org/10.5067/MODIS/MOD06_L2.006

OpenStreetMap contributors. (2015) Planet dump North America. Retrieved from
https://planet.openstreetmap.or

U.S. Census Bureau. (2019). 2019 American Community Survey Public Use Microdata
Samples. Retrieved from
https://factfinder.census.gov/faces/nav/jsf/pages/searchresults.xhtml?refresh=t

A special thanks to [Ruth Oliver](https://github.com/ryoliver) for guidance in [EDS 223](https://eds-223-geospatial.github.io/) in the completion of this work. 
