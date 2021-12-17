# MAP675 Final Project - Mapping Crime in NYC

### Mission Statment
In this project my goal was to be able to toggle the different areas of hotspots for certain types of crime and maybe have some demographic elements to it

### Data Source - NYC Open Data
- NYPD Arrest Records: https://data.cityofnewyork.us/Public-Safety/NYPD-Arrest-Data-Year-to-Date-/uip8-fykc

### Process Outline
1. I was originally going to just use their available API to fetch data on the front end, but I noticed that they were limiting the selections to 1000 per fetch. I wanted to work with a little more data than that so I exported a GeoJSON from their site and used Mapshaper to slim it down from 62 mb to 29 mb
    - `mapshaper nypd_data.geojson -filter-fields age_group,latitude,longitude,perp_race,perp_sex,ofns_desc -simplify dp 15% -o precision=.00001 format=geojson nypd_records_slim.json`
2. Next I need to filter out only the Manhattan borough:
    - `ogr2ogr -f "GeoJSON" -where "boro_name='Manhattan'" manhattan-borough.geojson boroughs.geojson`
3. Now I'll clip the streets with the Manhattan-borough.geojson:
    - `ogr2ogr -clipsrc manhattan-borough.geojson -clipsrclayer geoexport manhattan-streets.geojson nycStreetCenterline-simplified.geojson nycStreetCenterline-simplified -f "GeoJSON"`
4. The final step in this process is to create the web map. I decided to go with the Carto labels (similar to the exercise) and a dark base map. Some interesting challenges that arose in this process was adding an additional map pane for the hover labels, so they would be on top of the Carto labels, and struggling to get the order correct on the clipsrc OGR script. Some final additions I would improve upon is adding a 3D basemaps with building so you could look at the bike lanes with an oblique view as well as maybe adding some pictures of the bicklanes on hover similar to streetview or something.

https://data.cityofnewyork.us/Public-Safety/NYPD-Arrest-Data-Year-to-Date-/uip8-fykc