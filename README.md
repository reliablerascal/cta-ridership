# Who's Still Riding the CTA?
_An analysis of changes in CTA ridership between 2019 and 2022_

This project looks at which Chicago Transit Authority (CTA) train stations recovered the most, and which recovered the least, of their pre-pandemic ridership levels. Because the pandemic began impacting transit in March 2020, I chose to compare full-year ridership totals between 2019 and 2022.

I'm also attempting to set the stage for future demographic analysis by aggregating ridership stats for the 143 stations up to 77 community areas.

Here's my story, [Who's Still Riding the CTA](https://reliablerascal.github.io/cta_ridership/), as published on GitHub.

## Key Findings
My key findings are as follows:
* Citywide, 2022 train ridership was at 49% of pre-pandemic (2019) levels
* Stations ranged from 33% to 71% ridership retention
* The stations with the **best recovery** (ranging from 66% to 71%) were all **Pink Line** stops serving South Lawndale and the Lower West Side
* The station with the **weakest recovery** is the suburban **Oak Park Blue Line** station, at 33% retention
* The **next four weakest stations** were all in the **Loop**, Chicago's downtown area

Interestingly, I have not seen the Pink Line trend reported in Chicago. [Prior reporting by the Tribune and the Urban Institute](https://archive.is/a3wM8#selection-1181.0-1181.124) highlighted the Pulaski and Garfield Conservatory Green Line stops as recovering the best by December 2021  by that time.

## Data sources
|Data Source|Description|
|---|---|
|[CTA - Ridership - 'L' Station Entries - Daily Totals](https://data.cityofchicago.org/Transportation/CTA-Ridership-L-Station-Entries-Daily-Totals/5neh-572f)|Daily count of # of ridership on CTA by station of entry|
|[CTA - System Information - List of 'L' Stops](https://data.cityofchicago.org/Transportation/CTA-System-Information-List-of-L-Stops/8pix-ypme) |Additional station info including GPS coordinates and community area IDs|
|[CTA station additional info](source_data/lkup_stations_info.csv)|Manually-entered info on city and train line color|
|[Chicago Community Area Names](https://services7.arcgis.com/8kZv9DESIQ1hYuyJ/arcgis/rest/services/Chicago_Community_areas/FeatureServer/0/query?where=1%3D1&outFields=OBJECTID,community&returnGeometry=false&outSR=4326&f=json)| ArcGIS Community Area IDs and Names|
|[Chicago Community Geographic Boundaries](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6)| shapefile I used for mapping train stations in Flourish within Chicago community areas|


## Overview of Data Analysis Process
My data analysis process required the following steps:
* Acquired ridership and station data via API, aggregated through Socrata's query engine. Socrata is an API platform used by the City of Chicago and many other cities. Its [query language](https://dev.socrata.com/docs/queries/) helped me group and sum results more efficiently than possible with Pandas.
* Cleaned up data by removing a previously closed station, re-organizing data structures to get Lat and Lng coordinates as separate columns, dropping duplicate rows representing different entries to the same station
* Merged supplemental info about stations (lat/lng, station line color, city) into station data
* Created an aggregate community-level summary, merging in community names
* Calculated station-level and community-level summary metrics- primarily, percent ridership retention

% retention = ((2022 ridership) - (2019 ridership)) / (2019 ridership)

* Prepared graphics in DataWrapper and Flourish. I found the hex color codes in [Chicago's train wikipedia page](https://en.wikipedia.org/wiki/Chicago_%22L%22) to be helpful in getting the precise colors.

## Data Quirks and Other E-Varmints Standing in My Righteous Path
In addition to some problems mentioned above, I addressed the following problems:
* Removed 4 red line stations from station-level (but not community level) summaries, because two stations closed for renovation in May 2021 while adjacent stations picked up their ridership
* Annoyingly, community area IDs in CTA data did not exactly match IDs in the community area boundary file. I had to match by community area name
* Using a point map, I found it difficult to visually discern the difference between 35% ridership retention and 70% retention. While Youyou argued for mathematical precision, Gurman taught us that humans don't accurately perceive area. I found a helpful explainer on the [ethics of "perceptual scaling"](https://makingmaps.net/2007/08/28/perceptual-scaling-of-map-symbols/) and opted to exaggerate the differences in area, while explaining in full transparency why I had done so in the graphic's footer.

## What I Learned
Above all this project provided me with practical experience with Pandas within Jupyter Notebook. I love this approach over Google Sheets, because it neatly integrates documentation within code, creates a reproducible and automated template, and makes it easy for me to retrace my steps.

I also learned:
* Socrata's API platform, commonly used in city data portals
* GitHub, a means of organizing and sharing my code
* Scaling back my emotionally-unregulated ambitions. I really wanted to delve into demographic patterns, but that will have to wait for a Part II.

## What I'd Like to Learn Next to Advance this Project
Sandhya challenged me to improve the **orientation of the map**, by layering multiple GeoJSON files- the natural landscape (including the lake), suburban boundaries, and the path of the CTA. She suggested QGIS or MapShaper for this- neither of which I've yet used.

I also hope to layer **demographic data about the community areas**. I know how to do this with community areas but it's a lot of work. Alternatively, I could learn **point-in-polygon mapping** which would let me map stations to PUMAs- Chicago's 19 statistical areas which are more easily mapped to Census data.

Other than that, I'm still struggling to get image sizing to look good across platforms, especially desktop vs. mobile. I stuck with the default iframes for now.

## Guide to the Repository
Most data for this project is collected directly in Python via API. You'll also find in this folder:
results includes exported data analysis

* [source_data](source/data/)- includes only my own manually-entered lookup table for CTA stations
* [Jupyter Notebook](cta_ridership.ipynb)- steps through the analysis
* [results](results/)- results output from Jupyter Notebook for mapping/charting in DataWrapper and Flourish