## Source Code: Census Data

The data for this project comes from the most recent UK census of 2011. I am working with aggregated data for England and Wales, available for download from the [Office for National Statistics.](https://www.nomisweb.co.uk/census/2011/bulk/r2_2#KeyStatistics)

Geographical boundaries for mapping are available from the [Office for National Statistics geography portal.](https://geoportal.statistics.gov.uk/datasets/census-merged-local-authority-districts-december-2011-super-generalised-clipped-boundaries-in-great-britain)

Lookup tables to associate MSOAs with their Local Authorities are also on the geography portal, [here.](http://geoportal.statistics.gov.uk/datasets/output-area-to-lsoa-to-msoa-to-local-authority-district-december-2017-lookup-with-area-classifications-in-great-britain)

The source code for mapping came from Marcelo Rovai's [blog](https://towardsdatascience.com/mapping-geograph-data-in-python-610a963d2d7f) on Towards Data Science. 

For the bayesian modelling, I gained a lot of insight from Will Koehrsen's excellent [blog](https://towardsdatascience.com/bayesian-linear-regression-in-python-using-machine-learning-to-predict-student-grades-part-2-b72059a8ac7e), as well as the PyMC3 [documentation](https://docs.pymc.io/notebooks/getting_started.html). 


## Data Dictionary

Census data is released in many different formats and at many different levels. There are small samples of anonymised individual reponses, and then data for different aggregated areas: Output Areas (Middle Layer Super Output Area and Lower Layer Super Output Areas), Statistical Wards, Local Authorities, Regions and Countries. 

For this project, I worked with data from Middle Super Output Areas, or MSOAs. The columns for the data are:  


- GeographyCode: unique identifier for each entry 
- Tot_people: total person count (for MSAO) 
- Tot_area_hect: area (hectares) 
- Density: density (number of persons per hectare)
- Male%: percentage males
- Female%: percentage females
- Household_living%: percentage lives in a household
- Communal_living%: percentage lives in a communal area
- Living_1%: percentage living in a couple: Married or in a registered same-sex civil partnership
- Living_2%: % living in a couple: Cohabiting
- Living_3%: % not living in a couple: Single (never married or never registered a same-sex civil partnership)
- Living_4%: % not living in a couple: Married or in a registered same-sex civil partnership
- Living_5%: % not living in a couple: Separated (but still legally married or still legally in a same-sex civil partnership)
- Living_6%: % not living in a couple: Divorced or formerly in a same-sex civil partnership which is now legally dissolved
- Living_7%: % not living in a couple: Widowed or surviving partner from a same-sex civil partnership
- Qual_0: percentage no qualifications
- Qual_1: percentage highest level of qualification: Level 1 qualifications: 1-4 GCSEs or equivalent qualifications
- Qual_2: percentage highest level of qualification: Level 2 qualifications: 5 GCSEs or equivalent qualifications.
- Qual_A: percentage highest level of qualification: Apprenticeship 
- Qual_3: percentage highest level of qualification: Level 3 qualifications: 2 or more A-levels or equivalent qualifications
- Qual_4: percentage highest level of qualification: Level 4 qualifications and above: Bachelors degree or equivalent, and higher qualifications
- Qual_Other: percentage highest level of qualification: Other qualifications including foreign qualifications
- Health_vg:  percentage very good health
- Health_g: percentage good health 
- Health_f:  percentage fair health 
- Health_b:  percentage bad health 
- Health_vb:  percentage very bad health 
    


There are more variables included in the 'key statistics' of the census aggregrate data, but as they are so closely correlated to my target variable of health, I could not include them in this model. 

