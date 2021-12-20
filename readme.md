# MAP675 Final Project - Mapping Crime in NYC

### Mission Statment
In this project my goal was to be able to toggle the different areas of hotspots for certain types of crime and maybe have some demographic elements to it

### Data Source - NYC Open Data
- NYPD Arrest Records: https://data.cityofnewyork.us/Public-Safety/NYPD-Arrest-Data-Year-to-Date-/uip8-fykc

### Process Outline
1. I was originally going to just use their available API to fetch data on the front end, but I noticed that they were limiting the selections to 1000 per fetch. I wanted to work with a little more data than that so I exported a GeoJSON from their site and used Mapshaper to slim it down from 62 mb to 29 mb
    - `mapshaper nypd_data.geojson -filter-fields age_group,latitude,longitude,perp_race,perp_sex,ofns_desc -simplify dp 15% -o precision=.00001 format=geojson nypd_records_slim.json`
2. Now it's time to make a heatmap of of the data using Mapbox's heatmap styling option.
    - `https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#heatmap`