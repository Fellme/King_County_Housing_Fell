# King County Housing Analysis
***************************************
### Author: Morgan Fell

![image](https://user-images.githubusercontent.com/20844445/228355779-0a7b778f-f5a7-473d-a3a0-ac3d4d1d3092.png)

## Overview
Home and Garden Television (HGTV) is interested in filming around the Seattle, WA area. In preparation, we have gathered historical home data for King County, WA to have an understanding of the market. Through our analysis we hope to provide stakeholders with evidence of target home features, renovation return on investment, and overall pricing. Shows on the network range from Home Hunters, where a family explores 3-4 options to buy, to house flipping. In order to front the budget for these shows, our stakeholders need to understand if this area is worth the expense. Our final model highlights that the living space, size of the home's lot, garage and patio sizing, and location contribute to the price of homes in the area. 

*****************************************
## Business Problem
Before filming begins, HGTV completes research to provide scripts, potential investment reality, and budget. We will focus our discovery on the following:
1. How many homes are available for renovation and what is the historical ROI for renovated homes?
2. Should our crews focus more on structural features (living space, bathrooms, bedrooms, etc.) or landscape (views, acres, garage, patio, etc.)
3. Are there other features that increase price such as having a home on the waterfront or a view?

*****************************************
## Data Understanding
Our data set has 30, 155 entries spanning 24 columns. The homes in the list were built between 1975 and 2022. You will find a detailed list of the columns below. Before starting the data provided a warning about outliers being expected in the location, so we will want to ensure the homes we're including in our model are only from King County. 
### Column Names and Descriptions

### Number of Available Homes for Renovations
![image](https://user-images.githubusercontent.com/20844445/228362123-567d2aa4-1d83-4cee-9d21-4bb6f8aba2db.png)

Answering part of our first question, there is a substantial supply of homes that have not been renovated.
### Pricing Differences between Renovated Homes and Non-Renovated Homes
![image](https://user-images.githubusercontent.com/20844445/228362323-98886e71-0fa7-4d5f-87ce-be825c873191.png)

There is a 27% increase in homes that have been renovated. I would recommend sending crews from renovation centered shows and setting aside a budget item for renovations. 

### Trend in Home Price Compared to Age of Home
![image](https://user-images.githubusercontent.com/20844445/228363845-69d99914-f970-4f73-8999-92c9569e88d1.png)

When deciding which homes to renovate, we can visualize how price fluctuates when homes in the area age. Our overall average price for this area is around 1.08 million USD. Prices dip below this average when they're 55 to 85 years old. When scouting homes this could be taken into consideration as ideal investment properties.
****************************************
## Data Preparation
Our target variable for this project is **price**. We need to check our cleaned data for potential colinearity as this could throw off the results of our model. We can also use the Pearson Correlations listed to determine the features who are strongly correlated to our target. This help our teams understand what to focus on when forming a budget and choosing features to highlight in the script
![image](https://user-images.githubusercontent.com/20844445/228365695-fd9a0b40-84d0-4fb4-91cf-90263e6b822b.png)
>Correlation to Price in Highest to Lowest Order
>
>Sqft_living 0.65
>
>Sqft_above 0.58
>
>Bathrooms 0.52
>
>Bedrooms 0.34
>
>sqft_patio 0.31
>

Takeaways:
- The living space (`sqft_living`) has the highest correlation to price. This means we want to prioritize maximizing the actual home versus the increasing the size of the yard. Since bathrooms outranked bedrooms in correlation, I would suggest having crews focus on updating or adding bathrooms to the home if renovating. If they are trying to sell the home or purchase a new one, then I would prioritize highlighting bathrooms 
***************************************
## Modeling
Before running a model I split my data into categorical and numerical. The categorical data included `waterfront`,`condition`,`grade`,`greenbelt`,`nuisance`,`view`,`heat_source`,'sewer_system`,`month`, and  `renovated`. I used the one-hot endcoded technique to provide dummy values for modeling. After running separate Simple Linear Regressions on each variable, I selected those with the highest r-squared values. 

> Highest R-Squared Numerical Features Highest to Lowest
> 
> Sqft_living
> Bathrooms
> Latitude
> Bedrooms
> Sqft_basement

Grade was the only categorical feature of significance. Looking at the boxplots for Grade vs. Price we can see the higher ranking provides a better range of pricing. Moving grades could be achieved by having teams focus on improving the highly ranked numerical features. 

![image](https://user-images.githubusercontent.com/20844445/228371395-22f817d4-90e8-41dc-b046-701e5fa65422.png)


### Final Model



****************************************
## Conclusion and Follow-up



***************************************
For more information email: 
