# Who's Still Riding the CTA?
- An analysis of changes in CTA ridership between 2019 and 2022

This project looks at which Chicago Transit Authority (CTA) train stations recovered the most, and which stations recovered the least, of their pre-pandemic ridership levels. Because the pandemic began impacting transit in March 2020, I chose to compare full-year ridership totals between 2019 and 2022.

I'm also attempting to set the stage for future demographic analysis by aggregating ridership stats for the 143 stations up to 77 community areas.

Here's my story, [Who's Still Riding the CTA](https://reliablerascal.github.io/cta_ridership/) as published on GitHub.

## Key Findings
My key findings are as follows:
* Citywide train ridership in 2022 is at 49% of pre-pandemic (2019) levels
* Stations ranged from 33% to 71% ridership recovery
* The stations with the best recovery (from 66% to 71%) were all on the Pink Line, serving South Lawndale and the Lower West Side
* The station with the weakest recovery is the suburban Oak Park Blue Line station, at 33% retention
* The next four weakest stations are all in the Loop, Chicago's downtown area and primary job center

Interestingly, I have not seen the Pink Line trend reported in Chicago. Prior reporting from 2021 by the Tribune and the Urban Institute highlighted different stations as recovering most (Pulaski and Garfield Conservatory) by that time.

## Data sources
|Data|Source|Description|
|---|---|---|
|CTA daily ridership by station| https://data.cityofchicago.org | Count of # of riders on CTA each day |
| CTA station info | https://data.cityofchicago.org |Additional station info including GPS coordinates and community area IDs of each station |
| CTA station info 2 | Additional station info 
| Community Area Names | https://data.cityofchicago.org | Corresponding names for each station |


## Overview of Data Analysis Process
Socrata markup
...hand coded
...note my steps in Jupiter 

manual effort
grabbed CTA train colors from https://en.wikipedia.org/wiki/Chicago_%22L%22 


## Data Quirks and Other E-Varmints Standing in My Righteous Path
lots of data cleaning, etc.
mismatched community area numbers
drop 4x red line stations
perception of circles. I honestly noted this.


## What I Learned
Above all this project provided me with practical experience with Pandas. I love this approach over Google Sheets, because it is so well documented, reproducible, and easy to retrace my oft-forgotten steps.

Importantly, I also became comfortable with API access (Socrata's API platform in particular), GitHub, and scaling back my emotionally-unregulated ambitions.

## What I'd Like to Learn Next to Advance this Project
Sandhya challenged me to improve the orientation of the map, by layering multiple GeoJSON files- the natural landscape (including the lake), suburban boundaries, and the path of the CTA. She suggested QGIS or MapShaper for this- neither of which I've yet used.

I also hoped to layer demographic data about the community areas, which I sort of know how to do by using Census Reporter's custom geography tool to calculate census stats by community area. Alternatively, I'd like to learn point-in-polygon mapping so that I could map stations to PUMAs- Chicago's 19 statistical areas which are more easily mapped to Census data.

## Guide to the Repository
Most data for this project is collected directly in Python via API. You'll also find in this folder:
results includes exported data analysis

* [results](results/)
* [source_data](source/data/)- includes only my own manually-entered lookup table for CTA stations
* [Jupyter Notebook](cta_ridership.ipynb)- this steps through the analysis