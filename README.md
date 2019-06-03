# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Data Science Capstone Project - Picture of Health
## Using Census Data to Map and Model Health in England and Wales. 

This repository contains notebooks for my Capstone Project completed during General Assembly's Data Science Immersive.
### Introduction and Aims: 
The UK census is carried out once every 10 years, and a wealth of information from it is made available for public study. This project seeks to use data from the most recent 2011 Census for England and Wales to map and model areas of poor health across England and Wales. A model will be successful if it can be used to accurately predict levels of poor health based off predictor features, and return information about how these predictor features contribute towards the model.

The model is designed to be of interest to any institution looking at public health policies. It can be used to both find features that have the highest impact on wellbeing, as well as given changes in these features, make predictions of population health. 

Due to the focus on policy, I chose to use census aggregate data, rather than individual level census data (which is made available in anonymised micro-data samples, containing about 5% of overall responses, from the [UK Data Service.](https://census.ukdataservice.ac.uk/get-data/microdata.aspx)) The reasoning behind this is that policy is not implemented at an individual level, therefore a model that works with data aggregated per region (MSOA or Local Authority) is more immediately useful. If a Local Authority can gain insights on which characteristics of its population affect its overall health, then this model becomes a practical guide for actioning focussed improvements that will lead to an overall increase in wellbeing. 

In this project I work with the Middle Super Output Area (MSOA), a geographic area designed by the Office for National Statistics to facilitate reporting of small area statistics in England and Wales. There are 7,201 MSOAs in England and Wales, each MSOA is made up of contiguous Lower Super Output Areas, LSOAs, and they are designed to be as homogenous as possible. For a full breakdown of census geography, see the [ONS website](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeography). 

Each row in my data is an MSOA, and the corresponding entry is an aggregate percentage indicating the percentage of the MSOA and exhibits the column variable. This is important to remember when looking at the data and plots. 

A final note on the target variable of health: this is self-reported level, rather than one assigned by a medical practitioner. 

<b>Navigating through the repository: </b>

#### **[Data Dictionary and Source Code](./data_dictionary_and_sources)**

Links to access publicly available census data used in this project, as well as resources for mapping from shapefiles.  

#### **[Joining and preparing data](Joining_and_preparing_data.ipynb)**

This notebook contains all the code to stitch together, clean and transform my data into a useable data resource.


#### **[EDA and Modelling](EDA_and_modelling.ipynb)**

This notebook contains the bulk of my project, including all EDA, mapping, and modelling of my data. 

#### **[Summary and Conclusions](summary_and_conclusions)**

Findings from the project, and possible next steps. 


