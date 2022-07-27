# Bayesian occupancy modeling with the spOccupancy R package  <a href='https://www.jeffdoser.com/files/spoccupancy-web/'><img src="https://github.com/doserjef/spOccupancy/blob/main/man/figures/logo.png" align="right" height="139" width="120"/></a>

### [Jeffrey W. Doser](https://www.jeffdoser.com/)

#### Department of Integrative Biology, Michigan State University

## About

Occupancy modeling is a common approach to assess species distribution patterns across space and/or time while explicitly accounting for false absences in detection-nondetection data. Numerous extensions of the basic single-species occupancy model exist to model multiple species, spatial autocorrelation, and to integrate multiple data types. This presentation discusses [spOccupancy](https://www.jeffdoser.com/files/spoccupancy-web/), an R package designed to fit a variety of Bayesian single-species and multi-species occupancy models. I first give a brief introduction of occupancy modeling as a robust form of species distribution model as well as spatial autocorrelation and how it arises in detection-nondetection data. I then introduce the `spOccupancy` package and detail how to fit single-species spatial and non-spatial occupancy models. In this repository, I provide examples of three additional forms of occupancy models fit by spOccupancy: (1) multi-species models, (2) integrated occupancy models, and (3) multi-season (spatio-temporal) occupancy models. The repository contains the presentation slides, the example data sets, and the R scripts for the four examples. 

## Installing spOccupancy

spOccupancy can be installed from CRAN using `install.packages("spOccupancy")`. 

## Installing additional R packages

In the examples, we will use three additional packages for summarizing our results: [coda](https://cran.r-project.org/web/packages/coda/index.html), [MCMCvis](https://github.com/caseyyoungflesh/MCMCvis), and [ggplot2](https://ggplot2.tidyverse.org/index.html). These packages can be installed from CRAN as follows: 

```{r}
install.packages(c("coda", "MCMCvis", "ggplot2"))
```

## Repository structure 

### code

+ `single-species-example.R`: example code that fits a spatial and non-spatial occupancy model to assess how occupancy of an amphibian species (*Crossodactylus caramaschii*) varies across a gradient of landscape characteristics in Brazil.
+ `multi-species-example.R`: example code that fits multi-species occupancy models to assess how occupancy patterns of 36 amphibian species in Brazil varies across a gradient of landscape characteristics.
+ `multi-season-example.R`: example code that fits a multi-season occupancy model to assess occurrence trends from 2006-2019 of the Eastern Wood Pewee (*Contopus virens*) in a National Historic Park in Vermont, USA. 
+ `integrated-occupancy-model-example.R`: example code that fits an integrated occupancy model using two data sets to assess occupancy of the common bottlenose dolphin (*Tursiops truncatus*) in the northwestern Mediterranean Sea. 

### data

+ `ribeiroJr2018EcoApps.rda`: data from a single species (*Crossodactylus caramaschii*) in Brazil. This data set comes from [Ribeiro et al. 2018](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/eap.1741). The data set was obtained from the [Zipkin Lab Code Archive](https://github.com/zipkinlab/Ribeiro_etal_2018_EcoApps). The full data set used detection-nondetection data from human surveys as well as from autonomous acoustic recording units, and here we will only use the acoustic data. The R data object `ribeiroJrEtAl2018Data.rda` contains the data from the study formatted for use in `spOccupancy`. 
+ `multiSpeciesRiberioJr2018EcoApps.rda`: data from all 36 amphibian species analyzed in [Ribeiro et al. 2018](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/eap.1741). The data set was obtained from the [Zipkin Lab Code Archive](https://github.com/zipkinlab/Ribeiro_etal_2018_EcoApps).
+ `doser2021EcoApps.rda`: detection-nondetection data of the Eastern Wood Pewee (*Contopus virens*) in Marsh-Billings-Rockefeller National Historic Park in Vermont, USA from 2006-2019. These data were simplified from abundance data that were analyzed in [Doser et al. 2021](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/eap.2377).
+ `lauret202Ecology.rda`: detection-nondetection data of the common bottlenose dolphin (*Tursiops truncatus*) in the northwestern Mediterranean Sea. These data come from [Lauret et al. 2021](https://esajournals.onlinelibrary.wiley.com/doi/abs/10.1002/ecy.3535) and was obtained via the open data posted on [Zenodo](https://zenodo.org/record/5084385#.YuA1dDXMKXI). 

## Additional details on examples

### Single-species and multi-species examples on tropical amphibians

The goal for these examples is to assess how amphibian species occupancy patterns relate to a variety of landscape characteristics around 50 headwater streams in Brazil. Specifically, we will assess the effect of the following variables on amphibian species occupancy: 

+ `forest`: amount of forest land within surrounding landscape.
+ `agriculture`: amount of agricultural land within surrounding landscape.
+ `catchment`: catchment area, which is defined as the complete surface area that contributes to the stream channel in the downstream point from each sampling site.
+ `density`: stream density.
+ `slope`: slope of surrounding land in the landscape.

To accommodate variation in detection probability, we include the following covariates on detection: 

+ `date`: the day of sampling. We estimate both a linear and quadratic effect. 
+ `rain`: the amount of daily precipitation for the given sampling day. 

### Integrated occupancy model

The goal for this example is to assess how common bottlenose dolphin occupancy varies across the northewestern Mediterranean Sea. We include two covariates on dolphin occurrence: 

+ `BATHY`: the bathymetry, or information on the depth of the ocean at the given site. 
+ `SST`: sea surface temperature

We include multiple covarates on detection probability in order to accommodate variation in detection probability: 

+ `eff.samm` and `eff.gd`: the amount of survey effort for the two data sets, respectively
+ `ind.*.*`: an indicator variable accounting for different detection probability across the multiple repeat visits at each site for each data set. The first * corresponds to the dataset and the second * corresponds to the specific repeat visit. 

### Multi-season occupancy model

The goal for this example is to assess how Eastern wood-pewee occurrence has shifted over time from 2006-2019 in a historical national park. We include the following covariates: 

+ `regen`: the average forest regeneration at each site across the time period.
+ `basalArea`: the average basal area at each site across the time period. Note that we include both a linear and quadratic effect of basal area. 
+ `forestCover`: the average forest cover at each site across the time period.
+ `site.index`: an indexing variable that denotes the specific site each data point corresponds to. Can be specified as a random effect using `lme4` syntax (Bates et al. 2015). 
+ `year`: the year. 

We include the following covariates on detection`

+ `basalArea`: the average basal area at each site across the time period.
+ `year`: the year.  

## Additional Resources

+ [Introductory open-source spOccupancy manuscript](https://besjournals.onlinelibrary.wiley.com/doi/full/10.1111/2041-210X.13897)
+ [spOccupancy website](https://www.jeffdoser.com/files/spoccupancy-web/index.html)
+ [spOccupancy vignettes](https://www.jeffdoser.com/files/spoccupancy-web/articles/index.html)
+ Package updates are posted on [my twitter account](https://twitter.com/jeffdoser18)

