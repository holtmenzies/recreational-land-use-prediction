# recreational-land-use-prediction

## Notebooks

Five notebooks detail the steps required for cleaning, visualization, and model training.

- `building_trails_parks.ipynb`: Shows the steps to create a unified data set of mountain biking trails and public land that does not allow mountain biking
- `creating_raster_images.ipynb`: Shows the process of using the data set created previously to mask out the appropriate elevation values for each area included in the analysis
- `creating_semivariograms.ipynb`: This uses the elevation values obtained to compute a measure of texture. This step creates the features the models are trained on
- `model_training_evaluation.ipynb`: Establishes training and testing data sets. Also evaluates the predictive performance of the models
- `visualization_exploration.ipynb`: Explores the distribution of areas involved in the study and what ares the models failed to correctly predict

## Motivation and Problem Statement

Parks and access to nature represent an enormous good for those with access to them. Our language and books are filled with expressions of this sentiment. In Walden, author Henry David Thoreau extols the virtues of a life lived close to nature. “A walk in the park” is a common phrase used to denote something easy, straightforward, and pleasant.

This influence isn’t just an existential concept, parks contribute in measurable ways to the health of people using them (Foderaro, Klein; 2023). A study in the Journal of Physical Activity and Health found that physical activity performed outside was associated with “better stress management, outlook and health perceptions” (Puett et al., 2014).

Many Americans don’t meet the recommended criteria for fitness. According to a study by the Office of Disease Prevention and Health Promotion only 19% of women and 26% of men meet aerobic and muscle-strengthening guidelines in the United States (U.S. Department of Health and Human Services, 2018). All this is to say that parks aren’t just something nice to have, they have a vital role to play in creating a healthier society. Mountain Biking provides excellent cardiovascular and strength exercise as well as balance and stability practice. In fact, research suggests that complex activities that require good proprioception may be extra beneficial for those with neurodegenerative disorders (Patel et al., 2023). Various levels of difficulty mean that many ages individuals at different and levels of fitness can participate.

North Carolina (NC) has 100 counties, Wake County alone has over 400 thousand individual land parcels. With finite resources available to allocate toward the task of park creation an efficient method to narrow the search for new locations is needed.

Organizations like the North Carolina Natural Heritage Program offer comprehensive data sets on the ecological importance of land (https://www.ncnhp.org/data) and simply querying state government GIS data may be sufficient to find owners of desired parcels (https://www.nconemap.gov/pages/parcels). However, finding land that is well suited to a given activity currently relies on firsthand knowledge of the land in question.

A data driven approach to classify land use represents an incredible opportunity to quickly narrow the search for suitable land and better allocate time and money to creating more public space. A machine learning model will be developed to help identify parcels of land that are well suited to a given activity. Specifically, this analysis will look at identifying parcels of land that would make for desirable mountain bike trails in NC.

## Data Sources

### NC Digital Elevation Model

This dataset represents elevation for land in NC in 20-foot increments for the entire state. Elevation values for each county are stored in individual ASCII format raster files.

### North Carolina State and County Boundary Polygons

The state of NC makes shape files for the boundary of each NC County available via the NC OneMap data platform. This data set played an important role creating a unified dataset on which to train the models. The data pulled down from OSM did not have information denoting the enclosing county and therefore no way to map to the corresponding raster elevation. The county boundaries could be used to map the correct county to each OSM object.

### OpenStreetMap (OSM)

OpenStreetMap (OSM) (https://www.openstreetmap.org) is an open geographic database. Almost anybody can contribute information to the database. Consequently, it has extremely broad coverage in terms of how much of the earth is represented. I used Overpass Turbo (https://overpass-turbo.eu/) to query the OSM database for areas that allowed mountain biking. Overpass is an entire query language unto itself. Given that I have limited the scope of this analysis to NC, I used the Overpass Turbo Query Wizard with the following queries 

```
(bicycle=yes or bicycle=designated) and highway=path and (surface=unpaved or surface=ground)
(bicycle=yes or bicycle=designated) and highway=path and (surface=dirt)
```

#### OSM Copyright Notice

>OpenStreetMap® is open data, licensed under the Open Data Commons Open Database License (ODbL) by the OpenStreetMap Foundation (OSMF).
>
>You are free to copy, distribute, transmit and adapt our data, as long as you credit OpenStreetMap and its contributors. If you alter or build upon our data, you may distribute the result only under the same licence. The full legal code explains your rights and responsibilities.
>
>Our documentation is licensed under the Creative Commons Attribution-ShareAlike 2.0 license (CC BY-SA 2.0). 

## References

- Foderaro, L., Klein, W. (2023, May 24). The Health Superpowers of Parks. Trust for Public Land. https://www.tpl.org/parks-promote-health-report
- Puett, R., Teas, J., España-Romero, V., Artero, E. G., Lee, D.-c., Baruth, M., Sui, X., Montresor-López, J., & Blair, S. N. (2014). Physical activity: does environment make a difference for tension, stress, emotional outlook, and perceptions of health status? Journal of Physical Activity & Health, 11(8), 1503–1511. https://doi.org/10.1123/jpah.2012-0375
- U.S. Department of Health and Human Services. (2018). Physical Activity Guidelines for Americans, 2nd edition. https://health.gov/paguidelines/second-edition/pdf/Physical_Activity_Guidelines_2nd_edition.pdf
- Patel, R. A., Blasucci, L., & Mahajan, A. (2023). A pilot study of a 12-week community-based boxing program for Parkinson’s disease. Journal of Clinical Neuroscience : Official Journal of the Neurosurgical Society of Australasia, 107, 64–67. https://doi.org/10.1016/j.jocn.2022.12.006

