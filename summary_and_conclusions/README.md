# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Summary and Conclusions

<ul>
  <li><a href="#data">Data, Data, Data</li>
  <li><a href="#eda">EDA</li>
  <li><a href="#modelling">Modelling</li>
  <li><a href="#findings">Findings</li>
  <li><a href="#limitations">Limitations</li>
  <li><a href="#next_steps">Next steps</li>    
</ul>

<a id="data"></a>
### Data, Data, Data 
One of my biggest stumbling blocks at the start of this project was accessing the census data in the correct format. 
Census data is released in many different formats and at many different levels. There are small samples of anonymised individual responses, and then data for different aggregated areas: Output Areas (Middle Layer Super Output Area and Lower Layer Super Output Areas), Statistical Wards, Local Authorities, Regions and Countries. 

Each area is represented by a code, created by the Office for National Statistics to represent a wide range of geographical areas of the UK. The codes are very similar - for instance, E02000003 represents an MSOA in England, and E01000003 represents an LSOA in England. There are also codes that refer to outdated statistical areas, e.g. those used in prior censuses.  

The first dataset I was working with included a mixture of Wards, Region and Country data. I did not immediately notice the mix of output regions as the codes were so similar.  What I really wanted was to model on the MSOAs. I realised my mistake when (a) the entries did not have similar population sizes and (b) the MSOA boundary data that I downloaded to map with did not contain the same geography codes as my dataframe. The mistake was easy to fix, but it really did reinforce the fact that understanding the format of your data is a crucial component of any data science project. I could have created a 'working' model on the incorrect data, but any results would have been misleading. 

<a id="eda"></a>
### EDA

The EDA lead to some interesting insights on how levels of qualifications are distributed in the population. I was surprised to see that the spread of no qualifications and tertiary education was similar - our two end cases so to speak - and that Apprenticeships accounted for such a small part of the population. It will be interesting to see how the Apprenticeship Levy, introduced in 2017, changes this distribution in the next census. 

We discovered the Local Authorities that have the highest density of bad health (Merthyr Tydfil, Blaenau Gwent, Neath Port Talbot, Rhondda Cynon Taf, Blackpool), and those with the lowest (Hart, Wokingham, Isles of Scilly, Elmbridge, Richmond upon Thames). Four out of five of the worst affected LAs are in Wales, four out of five of the LAs least affected by bad health are in or within commuting distance of London. 

It is also interesting to see the areas that have the highest variance in bad health - Liverpool, East Lindsey, Halton, Newcastle upon Tyne, Cardiff, and Kensington and Chelsea.

Finally, we were able to see how poor health is distributed across England and Wales through the use of a plotting function that maps areas to a colorscale (green: good health, red: poor health). There is a strong concentration of green around Greater London and its surrounds, as well as the Yorkshire Dales. 

Areas of poor health are more concentrated at the fringes or edges. Wales looks particularly bad, as does the area around Newcastle, and the Lincolnshire coast. 

<a id="modelling"></a>
### Modelling 
I decided to turn this problem into a regression model, with percentage of bad health per MSOA as my target variable. Even though the distribution of bad health showed that I had many outliers (61 MSOAs with that had a level of bad health more than 3 times the mean value), I kept these outliers in my data. The importance of identifying areas of bad health outweighs the higher accuracy score I may get from dropping the outliers from my training data altogether. 

Here is the list of models I applied, along with their highest cross validated r-squared scores on the training data: 
- Linear regression model with lasso penalty: 0.82084
- Linear regression model with ridge penalty:  0.81938
- Linear regression model with elastic-net penalty: 0.82040
- KNeighborsRegressor: 0.759533
- DecicisionTreeRegressor: 0.723733
- RandomForestRegressor: 0.7971391
- BaggingRegressor (decision tree base estimator): 0.82644

Although the BaggingRegressor had the highest cross validated score, it is a black-box model, making it less useful for interpretation than my second highest performing model (linear regression with lasso). 

Satisfied with the scores on the sklearn model, I decided to implement a Bayesian linear regression, so that I could add credible intervals to the relative importance of each coefficient. I used priors with a Laplace distribution for the betas to simulate the lasso penalty of my best linear regression model.

The Bayesian model confirmed the findings and relative importance of predictor features, returning an r-squared score of 0.8302. 

<a id="findings"></a>
### Findings 

My Linear Regression with lasso penalty and Bayesian models agree on what the most important features are in predicting bad health. 

The feature that contributes most is: 
- % of the MSOA with no qualifications. 

The five features that contribute most <i>negatively</i> to predicting bad health are, in order: 
- % of the MSOA with tertiary education or higher 
- % of the MSOA with 1-4 GCSEs as their highest level of education 
- % of the MSOA with 2 or more A-levels as their highest level of education 
- % of the MSOA living in a couple, includes marriage, civil partnerships, cohabitation
- % of the MSOA with other qualifications

The overall finding of this project is that education levels are strong indicators of the health of a population. 

<a id="limitations"></a>
### Limitations 

- There were a limited number of predictor features available to model on. So many of the statistics released in the census were variations on questions of health and wellbeing, that I could not usefully include these in my model. (For example - if there was a feature about hours of unpaid care provided in the home, you could extrapolate to there being somebody who needs care in the home and who has poor health. This feature would become such an important predictor that the coefficients of more interesting features would be reduced.)  

- Having decided not to remove outliers in my training data (outliers being areas that have very high levels of bad health), I was still not able to successfully predicit the more extreme cases. For a model whose aim is to understand and predict health, being able to find these extreme cases is important. 

<a id="next_steps"></a>
### Next steps 

- Find ways to further validate this model. I could test it on 2011 census data from Scotland and Northern Ireland, or see if the model works as well on different levels of aggregate data. (For instance, my data is for MSOAs. Would the same model work for LSOAs, LAs, or wards?) 

- Find and isolate an area of England or Wales that has focussed on increasing education spend - does health improve? Do healthcare costs go down? Link these findings to costs. Can we track changes in one budget to changes in another?

- Putting the code into a model that could be used by a Local Authority or policy holder to predict changes in overall health based on budgeting decisions. For example: if x amount more is spent on education, what would the overall increase in health look like? This would require further modelling to understand exactly what the effect of increased education budget has on education levels, but we can expect that such research exists that could be used to help create an 'education for better health' budget tracker. This also requires tweaking existing code into a more object-oriented format, and considering a dashboard output or web interface for the model. I would also look into making more of the plots interactive with either plotly or Bokeh, rather than Matplotlib / Seaborn. 

- For making this information interactive at an individual level, I thought it could be fun to insert your postcode into a function, and have key statistics returned about your MSOA or Local Authority, along with a map of the country showing areas of similar levels of health. For this I started creating a [postcode lookup file](../creating_postcode_lookups.ipynb), but I  need to spend more time thinking about how I would deploy this on a website. 


