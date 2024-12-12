# QGIS Practice: Digitize a Rautjarvi Forest Inventory
This is a part of a series of lessons completed by following the tutorials outlined in the [QGIS Training Manual](https://docs.qgis.org/3.34/en/docs/training_manual/index.html), which is a component of the QGIS Documentation. The purpose was to learn and practice QGIS and geospatial skills. The lesson and data used in the practice is not my own, but was provided either by the QGIS Training Manual or Open Street Map.
**Specific Skills**
- Map digitization
- Map georeferencing
- Geospatial data management
- Aerial image digitizing
- Aerial image georeferencing
- Systemic sample plot generation
- Atlas systemic map generation

## Problem
The ultimate objective is to create field maps for a team to go and take samples for some forestry stands in Rautjarvi, Finland. The maps must include some conservation information about the specific locations of some squirrel species, as well as some information about protected forestry areas near a specific stream. 

There is an analog map and forestry stand inventory data from 1994 which should be compared to more recent (2012) aerial imagery and stand inventory. 

### Data Source
The aerial images, LiDAR data and basic maps were provided and adapted by the QGIS Training Manual, sourced from the National Land Survey of Finland open data service. The forestry map and data were provided by the training, sourced from the EVO-HAWK forestry school.

## Solution
### Digitizing & Georeferencing
The last inventory from 1994 was taken analogically. The manual provided a scanned map, so the first step was to georeference it. Using the `Georeferencer` tool in QGIs, some points selected from cross-hairs in the map were used to georefence the scanned map. Then an aerial image of the forest from 2012 was added to the map for comparison and to ensure that the scanned map is positioned correctly. 

Then an image manipulation program was used to extract out the forestry stand borders from the scanned 1994 map. These green borders were then imported into QGIS, polygonized, and the centroids of the resulting polygons were used to digitize the forestry stands. Then 1994 inventory data was imported and joined based on stand id. 

Then a colour-infrared image (CIR) from 2012 was imported and the stands were re-digitized. A 15m buffer was added around two locations with protected species of squirrel, and a 20m buffer was added around a stream that is also protected. This information was then joined into the attribute table of the updated forestry stands.

![](/images/1994map.png) ![](/images/map_w_aerial.png) ![](/images/green.png) ![](/images/1994_stands.png) ![](/images/2012protect.png) 

### Sampling & Atlas
The `Research Tools > Regular Points` tool was used to create an array of spaced points masked to the extent of the forestry stands.

Then the `Atlas` tool was used to generate multiple maps spanning the different sample areas that include the conservation information in the appropriate locations. The final Atlas can be viewed in `atlas.pdf`

![](/images/samples.png)

## Final Result
Finally, some data was provided as if the maps had been used to collect some information from the sample plots. These were joined to the stand layer and the field calculator was used to calculate the area, volume and number of stems in each stand. The volume data was then represented on a final map.
![](/images/final.jpg)
