# In-Demand Real Estate Development in Ames, IA


### Table of Contents

- [Problem Statement](#Problem-Statement)
- [Data & Resources](#Data-&-Resources)
- [EDA & Analysis](#EDA-&-Analysis)
- [Conclusion & Recommendations](#Conclusion-&-Recommendations)
- [Next Steps](#Next-Steps)
- [Acknowledgements](#Acknowledgements)

-------------------------

### Problem Statement

Ames, IA is an agriculturally-rich town in located in central Iowa. It is the eighth largest city in Iowa and home to Iowa State University. It was ranked ninth on CNNMoney's "[Best Places to Live](#https://money.cnn.com/magazines/moneymag/bplive/2010/)" list in 2010. 

The city has expanded considerably in the past two decades, with the total population expanding 30% from 50,731 residents in 2000 to 66,258 in 2019. Ames added over 5000 housing units in the years between 2000 and 2010, and while the 2020 census information has not been tabulated, the city's growth suggests that the total number of housing units also grew in the last decade. 

The municipality's steady growth means that builders are looking to construct homes that meet the needs of modern invididuals and families. To that end, the analysis detailed below is looking at what key construction features make the house the most appealing to home buyers and thereby garner a higher sale price. 

The analysis investigates the relationship between the sale price of a house and any bonus auxiliary structures -- i.e. basements, garages, and any other space adjacent to the main living area that could be used as storage or be used as alternative/additonal living or activity places while being separate from the main space in the house. My analysis focused on basements and garages, but a project of a larger scope could look at sheds, cover patios, attached dwelling units, and other enclosed areas. The data shows that including at least one of these features will increase the home price considerably, so this is an important item for housing developers to consider.  

### Data & Resources 

+ The Ames, IA real estate data comes from the Ames Assessor's office and contains records from individual property sales in the municipality from 2006 to 2010. It has been used to compute assessed values for residential properties. 
    - Reference URL: [Data Description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)
    - [Data Dictionary](https://www.kaggle.com/c/dsir-1116-ames-regression-challenge/data)
    
+ The Ames, IA population counts and other census data came from the [Ames' Wikipedia page](https://en.wikipedia.org/wiki/Ames,_Iowa#2010_census).

### EDA & Analysis 

Once I read in the Ames, IA real estate training set, I performed preprocessing that included handling null values and checking for sensible values. I then created basic exploratory visualization, including heatmaps and pairplots, to investigate more obvious trends. 

I used the clean data to build a series of models. For each model, I selected a set of features as my X, set the SalePrice column as my target variable y, performed a train-test split, scaled the training data, instantiated the model, fit it on the training data, scored it using both train and test sets, and then made predictions for the Ames Housing test real estate data which is separate from the test data I split off from my training set. 

The sets of features I used for the models can essentially be described as the following subsets: 
1. Numeric columns that required no dummifying or engineering (except for dealing with nulls and outliers). 
2. The numeric columns in No. 1 as well a selection of columns describing the house's garage or lack thereof.
3. The numeric and garage-related variable in Nos. 1 and 2 as well as a selection of columns describing the house's basement or lack thereof. The selection of which garage- and basement-related columns to dummify and use were based in those that seemed to have the strongest correlation according to the correlation table and heat map, and I also paid attention to multicollinearity when selecting these features.  

I ran a linear regression, ridge regression, and cross-validated lasso regression. The ridge regression model fit on the numeric, garage, and basement-related columns (the third subset detailed above) performed the best at predictin the sale prices for the Ames Housing test set, with a test RMSE score of 28034.2. 

In addition to making the sale price predictions, I did some analysis on the training set to look for the relationship between the garage and basement features and the sale price-- i.e. which features and categories contributed to higher sale prices. 

### Conclusion and Recommendations 

The latter part of my analysis shows that both garages and basements can have a significant effect on home prices. 

In the ridge regressor model that yielded the most accurate predictions, several basement and garage features proved to have the largest coefficients, indicating a powerful correlation. The coefficient for the total basement square feet was 28444, meaning that the house price increases by $28,444 for every unit increase of basement square footage when all other variables are held constant. Other variables with the highest or lowest coefficients (indicating postive or negative correlation) were: Garage Cars (how many cars the garage is made to fit), basement quality, garage size, basement exposure, garage condition, and the binary of whether or not a house has a garage.

A groupby analysis on the Ames housing data also showed that the basements with higher ceilings had much higher mean sale price than those with lower ceilings. Additionally, the size of the basement has a linear relationship with the sale price. Finally, the type of garage seemed to be a significant factor, as houses with garages that are adjacent to the main house (built-in, attached, and basement garages) had mean sale prices above $150,000, while house with detached garages or car port garnered prices below $150,000. 

Based on this analysis, I would recommend to any real estate developer that they strongly consider including either a finished basement or adjacent garage in their development plans. The data tells us that this is a basic way to increase the value of a home. 

### Next Steps 

Further analysis is needed to understand the interaction between the garage, the basement, and the rest of the house. While these are independently strongly-correlated variables, an important next step would be to see how they interact with and/or compound one another (through Polynomial feature engineering) and how they are impacted by other variables. From there, common sense and domain knowledge can help us know whether one or the other - a garage or basemenet - is better suited to a given property or house.

Also important to look at our how these features relate to the topography and other land features. I would also want to look at hose these features are related to the neighborhood the house is in. 

### Acknowledgements

Thank you to Charlie Rice, John Hazard, and Prasoon Karmacharya for their invaluable support in putting this project together! 

