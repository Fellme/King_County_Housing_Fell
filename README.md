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
Our data set has 30,155 entries spanning 24 columns. The homes in the list were built between 1900 and 2022. You will find a detailed list of the columns below. Before starting the data provided a warning about outliers being expected in the location, so we will want to ensure the homes we're including in our model are only from King County. 
### Column Names and Descriptions for King County Data Set
   * `id` - Unique identifier for a house ,
   * `date` - Date house was sold ,
   * `price` - Sale price (prediction target) ,
   * `bedrooms` - Number of bedrooms ,
   * `bathrooms` - Number of bathrooms ,
   * `sqft_living` - Square footage of living space in the home ,
   * `sqft_lot` - Square footage of the lot ,
   * `floors` - Number of floors (levels) in house ,
   * `waterfront` - Whether the house is on a waterfront ,
       * Includes Duwamish, Elliott Bay, Puget Sound, Lake Union, Ship Canal, Lake Washington, Lake Sammamish, other lake, and river/slough waterfronts ,
   * `greenbelt` - Whether the house is adjacent to a green belt ,
   * `nuisance` - Whether the house has traffic noise or other recorded nuisances ,
   * `view` - Quality of view from house ,
       * Includes views of Mt. Rainier, Olympics, Cascades, Territorial, Seattle Skyline, Puget Sound, Lake Washington, Lake Sammamish, small lake / river / creek, and other ,
   * `condition` - How good the overall condition of the house is. Related to maintenance of house. ,
      * See the [King County Assessor Website](https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r) for further explanation of each condition code ,
   * `grade` - Overall grade of the house. Related to the construction and design of the house. ,
      * See the [King County Assessor Website](https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r) for further explanation of each building grade code ,
   * `heat_source` - Heat source for the house ,
   * `sewer_system` - Sewer system for the house ,
   * `sqft_above` - Square footage of house apart from basement ,
   * `sqft_basement` - Square footage of the basement ,
   * `sqft_garage` - Square footage of garage space ,
   * `sqft_patio` - Square footage of outdoor porch or deck space ,
   * `yr_built` - Year when house was built ,
   * `yr_renovated` - Year when house was renovated ,
   * `address` - The street address ,
   * `lat` - Latitude coordinate ,
   * `long` - Longitude coordinate ,
    
Most fields were pulled from the [King County Assessor Data Download](https://info.kingcounty.gov/assessor/DataDownload/default.aspx)

### Number of Available Homes for Renovations
![image](https://user-images.githubusercontent.com/20844445/228362123-567d2aa4-1d83-4cee-9d21-4bb6f8aba2db.png)

Answering part of our first question, there is a substantial supply of homes that have not been renovated.
### Pricing Differences between Renovated Homes and Non-Renovated Homes
![image](https://user-images.githubusercontent.com/20844445/228362323-98886e71-0fa7-4d5f-87ce-be825c873191.png)

We can see the mean for each using the green triangle on the boxplot. There is a 27% increase in the median price for homes that have been renovated. I would recommend sending crews from renovation centered shows and setting aside a budget item for renovations. 

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
I split my data into categorical and numerical. The categorical data included `waterfront`,`condition`,`grade`,`greenbelt`,`nuisance`,`view`,`heat_source`,'sewer_system`,`month`, and  `renovated`. I used the one-hot endcoded technique to provide dummy values for modeling. Joint plots were used to view the distribution of data and understand the linear relationships of the numerical features to price. Seperate simple linear regressions were run on each variable, I selected those with the highest r-squared values. 

> Highest R-Squared Numerical Features Highest to Lowest
> 
> Sqft_living
> Bathrooms
> Latitude
> Bedrooms
> Sqft_basement

After adjusting the columns in the categorical data, I applied a similar set of simple linear regressions. Grade was the only categorical feature of significance. Looking at the boxplots for Grade vs. Price we can see the higher ranking provides a better range of pricing. Moving grades could be achieved by having teams focus on improving the highly ranked numerical features. 

![image](https://user-images.githubusercontent.com/20844445/228371395-22f817d4-90e8-41dc-b046-701e5fa65422.png)


### Final Model
There were a total of 4 models attempted after eliminating features based on the simple regressions. 
- Model one can be considered our Basline Model because every high ranking feature was allowed. This returned an r-squared of 0.63; however, two of the features, `floors` and `bedrooms` had high p-values meaning we could not reject the null hypothesis. 
- Model two eliminated those features with minimal changes to the r-squared value. 
- With the third model I introduced log transformation to help normalize the distribution. Again, the changes to r-squared were minimal and still overed around 0.63. I did see some of the other metrics become better, such as Kurtosis and F-Statistic. 
- Finally, I performed a recursive regression to pull out selected features: `lat` and grades '3 Poor','12 Luxuary', `5 Fair`, and `11 Excellent`. The recursive model accounted for the least price variability with an r-squared of 0.26. The fourth model did lower the Kutosis, meaning the data was more normalized. 
- With the addition of error checking MSE and RMSE, I landed on the third model being the best performing. 
![image](https://user-images.githubusercontent.com/20844445/228567002-3657478f-ff36-4137-8daf-18ec2239d3b6.png)

****************************************
## Conclusion and Follow-up

As filming begins, HGTV will want to focus on improving and/or increasing the living space mainly with the bathrooms. Using the coefficients of the grades we can see that the lower a home is graded the more our price decreases. I can see that as soon as we hit a grade of 8 (Good) we drop below a -6 coefficient. Knowing that latitude contributes to the price, I looked back at the descriptive data and found 75% occurred within 47.63 and -122.13 for longitude. This cooresponds to the Redmond area of King County. I would recommend crews start here when looking for properties to showcase.

![image](https://user-images.githubusercontent.com/20844445/228575289-919595db-aeff-4955-8b4d-b0737f8a5663.png)
![image](https://user-images.githubusercontent.com/20844445/228575331-aee843d8-4fe6-4889-809e-b15ae2252c1d.png)

***************************************
## Next Steps

- Looking further into how to transform the data for better distribution metrics would be ideal. 
- I would recommend looking into the location of the homes as they compare to prices further. Using zipcodes, population density, and distance from Seattle city proper could factor into the price increasing
- For any of the renovated homes, it would be nice to see what specifically was changed. We could compare the square footage of the living space before and after the renovation. 


For more information email: Morgan Fell (morgan13.fell@gmail.com)

**Repository Structure**
```
├── King_Country_Linear_Regression.ipynb                      <- Narrative documentation of analysis in Jupyter notebook
├── Map.ipynb                                                 <- Documentation for Map in Jupyter Notebook
├── README.md                                                 <- The README for reviewers of this project
├── Column Headers.md                                         <- Detailed listing of the columns in the CSV file
├── King_county_house.csv                                     <- King County Housing data file
└── presentation.pdf                                          <- PDF version of project presentation
```
