# Aquaculture-Suitability

![Lobster in the sea. Source: English Plus Podcast](https://englishpluspodcast.com/wp-content/uploads/2022/01/Episode-13-Lobsters.jpg)
## Purpose

As the global population continues to grow exponentially, the sustainability of current protein sources can be called into question. Marine aquaculture provides a potential solution through this problem, as mapped by [Gentry et al.](https://www.nature.com/articles/s41559-017-0257-9), where marine aquaculture potential was analyzed based on restraining factors such as bottom depth. They found that they could fulfill the global seafood demand by using less than 0.015% of the ocean area.

This repository contains an analysis similar to the Gentry et al. study, where we determine what percent of Exclusive Economic Zones (EEZ) on the West Coast of the US can support our marine animals of interest. We will look finding suitable locations for each animal based on their ideal depth and temperature conditions, using data from the NOAA and GEBCO respectively.
Workflow was generalized into a function where 4 different inputs of minimum and maximum temperature, along with minimum and maximum depth can be inputted to yield a map of suitable area within each EEZ.

## Repository Structure
```
│   README.md
│   aquaculture-suitability.qmd
└───data
     └───average_annual_sst_2008.tif
     └───average_annual_sst_2009.tif
     └───average_annual_sst_2010.tif
     └───average_annual_sst_2011.tif
     └───average_annual_sst_2012.tif
     └───depth.tif
     └───wc_regions_clean.dbf
     └───wc_regions_clean.prj
     └───wc_regions_clean.shp
     └───wc_regions_clean.shx
     └───coast
          └───cb_2018_us_state_20m.cpg
          └───cb_2018_us_state_20m.dbf
          └───cb_2018_us_state_20m.prj
          └───cb_2018_us_state_20m.shp
          └───cb_2018_us_state_20m.shp.ea.iso.xml
          └───cb_2018_us_state_20m.shp.iso.xml
          └───cb_2018_us_state_20m.shx
```

## Data Access

Sea surface temperature data was sourced from the [NOAA’s 5km Daily Global Satellite](https://coralreefwatch.noaa.gov/product/5km/index_5km_ssta.php), where average annual temperatures from 2008 to 2012 were used. All years were combined into a raster stack, where the mean of all years was calculated and reclassified to the animal of interest. Data was read in using the `rast()` function, and concatenated via `c()`.

Bathymetry data was sourced from the [General Bathymetric Chart of the Oceans](General Bathymetric Chart of the Oceans (GEBCO)). Similar to the sea surface temperature data, once depth was cropped and resampled to match temperature data, it was then reclassified to the animal of interest. Data was read in using the `rast()` function.

Exclusive Economic Zone data was sourced from [Marineregions.org](https://www.marineregions.org/eez.php), which contains a shapefile of Exclusive Economic Zones along the west coast of California. Data was read in using `st_read`.

The States Boundary data was sourced from the United States Census Bureau via their [Cartographic Boundary Files - Shapefile Data](https://www2.census.gov/geo/tiger/GENZ2018/shp/cb_2018_us_state_20m.zip) Data was filtered to states present in EEZ data. Data was read in using `st_read`. 

All data was placed in the data folder and was read in using R. 

## Data References

  "Sea Life Base", "Palomares, M.L.D. and D. Pauly. Editors. 2024. SeaLifeBase. World Wide Web electronic publication. Retrieved: 11/14/24 from www.sealifebase.org, version (08/2024).","[Lobster Data ](https://www.sealifebase.ca/summary/Homarus-americanus.html)", 
   
  "Sea Surface Temperature Data", "NOAA Coral Reef Watch Version 3.1 (2018). Retrieved: 11/14/24", "[SST Data](https://coralreefwatch.noaa.gov/product/5km/index_5km_ssta.php)",
  
  "Bathymetry Data", "British Oceanographic Data Centere. Retrieved 11/14/24 from https://www.gebco.net/data_and_products/gridded_bathymetry_data/#area", "[Depth Data](https://www.gebco.net/data_and_products/gridded_bathymetry_data/#area)",
  
  "Cartographic Boundary Files - Shapefile Data", "United States Census Bureau. Retrieved 11/28/24 from https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html", "[US Coast Data](https://www2.census.gov/geo/tiger/GENZ2018/shp/cb_2018_us_state_20m.zip)",
  
  "Exclusive Economic Zones Data", "MarineRegions.org. Retrieved 11/14/24 from https://www.marineregions.org/eez.php", "[EEZ Data](https://www.marineregions.org/downloads.php)",
  
  "American Lobster", "Defenders of Wildlife. Retrieved 11/28/24 from https://defenders-cci.org/landscape/climate-factsheets/ClimateChangeFS_American_Lobster.pdf", "[Lobster Temperature Range Data](defenders.org/climatechange)"




