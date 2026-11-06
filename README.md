# Mapping Suitable Aquaculture Habitats Along the U.S. West Coast

## About
This repository presents an analysis of potential marine aquaculture habitats for oysters and Pacific calico scallops (Argopecten ventricosus) along the U.S. West Coast. The analysis integrates sea surface temperature (SST) data from 2008–2012, ocean bathymetry data, and Exclusive Economic Zone (EEZ) boundaries to identify areas with suitable environmental conditions for each species.

The analysis uses raster processing and spatial analysis in R to identify locations that meet the temperature and depth requirements of each species. Two maps illustrate the distribution of suitable habitat area (km²) across West Coast EEZ regions.

The goal of this analysis is to explore how sea surface temperature and ocean depth influence potential aquaculture habitat suitability and compare the geographic distribution of suitable areas between the two species.

## Repository Contents
- `aquaculture_analysis.qmd`: Quarto document containing R code, spatial analysis, maps, and written interpretation.

- `aquaculture_analysis.pdf`: Rendered PDF of the Quarto document.

- `.gitignore`: Excludes the locally stored data/ folder from Git version control.

- `README.md`: Project overview, data information, methods, and references.

## Data
The data are not stored in this repository. Download the course data bundle, unzip it, and place the files in a data/ directory.

## Sources
National Oceanic and Atmospheric Administration (NOAA): Sea surface temperature data originally generated from NOAA's 5km Daily Global Satellite Sea Surface Temperature Anomaly v3.1 product.

General Bathymetric Chart of the Oceans (GEBCO): Ocean bathymetry data used to characterize ocean depth.

Marine Regions: West Coast Exclusive Economic Zone boundaries.

SeaLifeBase: Species information for Pacific calico scallops (Argopecten ventricosus), including preferred temperature and depth range.

## Reproducing the Analysis
Clone or download this GitHub repository.

Download the course data and place the files in the data/ directory.

Install the required R packages.

Open aquaculture_analysis.qmd in RStudio, Positron, or another R-compatible environment.

Check that the file paths in the data-loading chunks match the local folder structure.

Render the Quarto document to PDF to generate the maps and written analysis.

## Methods
Spatial data were processed and visualized in R using the following packages:
- `tidyverse`
- `terra`
- `sf`
- `here`
- `stars`
- `tmap`
- `RColorBrewer`
- `knitr`
- `gt`
- `spData`
- `spDataLarge`

Five annual SST rasters (2008–2012) were combined to calculate mean sea surface temperature and converted from Kelvin to Celsius. Ocean bathymetry data were cropped and resampled using bilinear interpolation to match the SST raster's resolution and extent. Coordinate reference systems were checked for consistency.

A custom R function, `suitable_aquaculutre()`, was developed to identify suitable habitat based on species-specific temperature and depth requirements.

Oysters: SST between 11–30°C and ocean depths between 0–70 meters, based on the environmental requirements provided in the assignment.

Pacific calico scallops: SST between 11–28.5°C and ocean depths between 0–180 meters. Species information was informed by SeaLifeBase, which identifies a preferred temperature of 26°C and a depth range of 0–180 meters. The 11–28.5°C range was used as the temperature threshold for this analysis.

Raster cells meeting both temperature and depth conditions were classified as suitable (1), while cells outside these ranges were classified as unsuitable (0). Map algebra was used to identify locations satisfying both conditions.

Suitable habitat rasters were masked to West Coast EEZ boundaries. The area of suitable raster cells was calculated in square kilometers using `terra::cellSize()`, and `terra::zonal()` was used to summarize total suitable habitat area within each EEZ region.

## Author
Farah Stack

## References
National Oceanic and Atmospheric Administration (NOAA). Coral Reef Watch: 5km Satellite Sea Surface Temperature Products. https://coralreefwatch.noaa.gov/product/5km/index_5km_ssta.php

General Bathymetric Chart of the Oceans (GEBCO). Gridded Bathymetry Data. https://www.gebco.net/

Marine Regions. Exclusive Economic Zones (EEZ). https://www.marineregions.org/eez.php

SeaLifeBase. Argopecten ventricosus (Pacific calico scallop): Species Summary. https://www.sealifebase.ca/country/CountrySpeciesSummary.php?Country=US+America+%28contiguous+states%29&genusname=Argopecten&speciesname=ventricosus

Hijmans, R. J. terra: Spatial Data Analysis. https://rspatial.github.io/terra/

Tennekes, M., & Nowosad, J. tmap: Thematic Maps in R. https://r-tmap.github.io/tmap/

UCSB Master of Environmental Data Science. EDS 223: Geospatial Analysis and Remote Sensing. https://eds-223-geospatial.github.io

## Acknowledgements
Special thanks to Professor Annie Adams and Teaching Assistant Mary Salami for their instruction and guidance throughout EDS 223. Additional appreciation goes to the UCSB MEDS Class of 2027 cohort for their collaboration, shared learning, and support.


