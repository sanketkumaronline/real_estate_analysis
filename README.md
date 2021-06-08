# Real Estate Analysis

We are going to be using data from the 2020 -2021 Toronto Real Estate sold house listings.  We want to answer questions whether the sold listings could predict future house prices based on the house's features (number of washrooms, bedrooms, etc), location.  

## Presentation
![download (2)](https://user-images.githubusercontent.com/64053195/120941363-642c2f00-c6f0-11eb-95a9-020c6e3dd940.gif)

### Overview
Our chosen project examines house prices in the Greater Toronto Area in the years 2020 and 2021.

Google Presentation: 
[Link To Presentation](https://docs.google.com/presentation/d/e/2PACX-1vRuwZSA81H4OhSnRKrtkMcpR9kmHeZdXy7A9sMxC_RHTJ8gHoP2ZCp5lsE7Z8z5Z1nAENPosdT-gUwe/pub?start=false&loop=false&delayms=3000)

Heroku Web App: https://homepricegta.herokuapp.com

## Data:
The data are pdf files which show 26 rows.
The pdf files are converted into Excel files, cleaned up then saved as csv.  
Multiple Linear Regression model will be used to predict the future price of the house based on the house features listed above.
We are using SQLite for the Database.  

### Data Content 
1. "#" - The row number. 
2. LSC - The listing displays its contract status at the Last Status Change (LSC) field
3. EC - Describes whether the property has received the Encumbrance Certificate: certificate of assurance that the property is free from any legal or monetary liability
4. St# - The Street number 
5. Street name - The name of the street.
6. Abbr - Abbreviation of Street type. 
7. Dir - Direction (North, South, East and West). 
8. Municipality - The name of the city in which the property resides in. 
9. Community - The name of the locality on which the property resides within a given municipality.
10. List Price - The price of the property at the time of listing.
11. Sold Price - The price that the property was sold for. 
12. Type - Describes the type of the property (semi-detached, detached or attached).
13. Style - Number of storeys in the listed property contains.
14. Br - The number of bedrooms in the listed property contains.
15. "+" - Any other additional rooms in the listed property. 
16. Wr - The number of washrooms in the listed property.
17. Fam - Indicates if there is a family room in the listed property.
18. Kit - Number of kitchens in the listed property.
19. Garage type - The type of the garage.
20. A/C - The type of A/C (Centralized or non-centralized).
21. Heat - The type of Furnace.
22. Contract Date - The date the contract was signed.
23. Sold Date - The date the property was sold on.
24. List Brokerage - Name of brokerage that the listed property was under.
25. Co op Brokerage - Buyer's brokerage.
26. MLS # - A unique number assigned to a real estate listing. 

We were able to gather our data from a licensed realtor who has access to the most recent listing information about house sales in Brampton for last six months. <br/>
[Directs you to the profile of the realtor](https://soldbysingh.ca/)

### Questions that we hope to answer: 
1. Do unique features of the house (Washroom, bedroom, area, semidetached, attached) play an integral role with determining the sold price?<br/>
2. Does the location, type, style, listing date and listing price play a factor of the sold price?<br/>
3. When was it listed and how fast was it sold?<br/> 
4. Does location dictate how long a house is listed in the market and if there are any patterns?<br/>
5. Does the location showcase a pattern in the over asking prices?<br/>
6. What will be the Sold Price of a house based on different features mentioned in the dataset? 

## Machine Learning Model

We have created machine learning model to predict "Sold Price" of a house based on style, type, bedrooms, washrooms, and list price of a house. This can help a prospective buyer to decide how much to bid for the house. We have used Multiple Linear Regression model for this purpose. 

### Preliminary Feature Selection for Machine Learning Model

1. The preliminary feature selection was done using exhaustive feature selection method which is one of the **Wrapper Methods**. We trained machine learning model multiple times using different feature sets and comparing the results.
2. Since we are trying to predict the "Sold Price" of the house based on a number of input features, it was taken as the **target variable**. The features had to be selected from remaining 25 columns
3. Few non-beneficial columns such as “Municipality”, “MLS#”, “#”, “LSC”, “EC”,”Dir” were removed in the first iteration because either they had same values, or just used as unique row identifiers. The results were evaluated.
4.	In the subsequent iterations, the remaining columns were tested as features and the performance of machine learning model was evaluated. Additional 8 columns were dropped to improve the accuracy of the model.
5.	The remaining 10 columns were selected as **input features** : 
`"List Price", "Type", "Style", "Br"(bedrooms),	"Additional"(additional rooms), "Wr"(washrooms), "Fam", "Kit"(kitchen), "Garage Type", "Contract Date", "Sold Date"`

### Data Processing for Machine Learning Model
1.	Data is pulled from SQLite database into a DataFrame. The data is in tabular format with a total of 26 Columns and 1193 rows in the database with string (object) and numeric datatypes (int64, float64). 
2.	Out of the 26 columns, 14 are dropped as they are non-beneficial or decrease the performance of the machine learning model. The 12 columns remaining are: 
`"List Price", "Sold Price", "Type”, “Style", "Br", "+", "Wr", "Fam", "Kit", "Garage Type", "Contract Date", "Sold Date".`
3.	The following columns are converted into Integer data type from the Object type: "List Price", "Sold Price", "Contract Date", and "Sold Date".
4.	The four columns with Object datatype ("Type", "Style", "Fam", "Garage Type") are encoded into numerical values using **OneHotEncoder**. All these have less than or equal to 10 unique values. Binning was performed on "Style" which had 10 unique values, but it imporved the accuracy slightly.

### Splitting into Training and Testing Datasets

1.	The dataset is split into training and testing datasets using **train_test_split()** function. The training datasets are created for features (X_train, X_test) and targets (y_train, y_test)	
2.	The **random_state** parameter has been passed as an integer (5), which means the results are reproducible.  
3.	We passed **train_size** parameters the value 0.8 and **test_size** the value 0.2. It means 70% of original dataset will be used in the training dataset and remaining 30% as test dataset.

### Selection of Machine Learning Model

Since we are trying to predict a continuous numerical output (i.e. “Sold Price” of homes) based on a number of input variables, we have selected **Multiple Linear Regression** as a machine learning model.  It will take an input of a set of factors (or test dataset), learn patterns and find relationships between datapoints to predict the value of dependent variable.  The 11 columns mentioned above are taken as feature or input variables.

We also tested *XGBRegressor* from the XGBoost library and *Support Vector Regression (SVM)* from sklearn as alternative machine learning models. However, the perfromance was dropped significantly. Therefore, Linear Regression regression was chosen as best option out of the tested models. More details about testing above mentioned alternative models can be found in *ml_models_comparison.ipynb* file. 

### Changes Made After Segment 2

* After initially testing the model and doing some initial analysis based on 11 features, the "Sold Date" was also dropped as ultimate goal was to predict Sold Price of house in market to help prospective buyers. So now we have 10 input features. 
* The scaling of input data with StandardScaler() is no longer done. As mentioned in previous segment, it did not improve the model accuracy. Therefore, it was removed to reduce coding complexity and execution time.
* Binning for the values in "Style" column was removed.

These changes had very little impact on the model performance. The R2 score dropped by 0.07%, MAE by 0.2%, and RMSE by 0.75%.  

### Model Training

There are a total of 1193 records/rows in the dataset. The train_size and test_size was initially set at 0.8 and 0.2 respectively. However, this has been changed to 0.9 and 0.1 to include some more data in the training part. It means the linear regression model is now trained on about 1075 rows with 10 feature variables and 1 target variable. 


### Model Performance

The performance or accuracy of the model has been evaluated based on 3 most commonly used evaluation metrics used for linear regression models.

**Coefficient of Determination (R2) :** It explains to what extent the variance of one variable explains the variance of the second variable. It usually has a value of 0 to 1. The closer the value is to 1, better the fit. The R2 value for this model comes out to be 0.9412. It means about 95% of the observed variation can be explained by the model’s inputs.

**Mean Absolute Error (MAE) :** It is an arithmetic average of the absolute errors. It has same unit as original data. The lower the MAE value, more accurate the model is. The MAE for this model is 50207.32. 

**Root Mean Squared Error (RMSE) :** It is the mean of the squared errors. The lower the RMSE value, more accurate the model is. The RMSE value for the model is 66918.91. 

To measure the significance of the errors, the The MAE is 4.98% of Average of y_test values and the RMSE is 6.63% of Average of y_test values.

*Actual Vs Predicted Output Graph*

![Actual vs Predicted graph](./Images/graph.png)

*Actual Vs Predicted Output Comparison*

![Actual vs Predicted comparison](./Images/output_comparison.PNG)

*Machine Learning User Interface*

![Machine Learning User Interface](./Images/mlinput.PNG)

---
### Entity Relationship Diagram

![sold_homes_ERD](https://github.com/AndrewTymkiv/real_estate_analysis/blob/main/Images/sold_homes_ERD.png)


---


### Blueprint for the dashboard
[Link to Storyboard](https://docs.google.com/presentation/d/1_tKWkIlpeKGwXy4Q99mPNuYnnJdzkXBzRgX7FtQBHkM/edit?usp=sharing)


### Tableau 
Images from the initial analysis

This bar graph shows the different house types( Att/Row/Tw, Detached, Link, Semi-Detac) with the average house price (blue bar graph), it also shows the difference in price from the  ([Sold Price]-[List Price]) (orange line)
![](Images/PriceDiffType.PNG) 


This bar graph shows the different house styles(Bungaloft, Sidesplit, Bungalow, Bungalow-R, 1 1/2 Storey, 2 Storey, 2 1/2 Storey, 3 Storey) with the average house price (blue bar graph), it also shows the difference in price from the  ([Sold Price]-[List Price]) (orange line)
![](Images/PriceDiffStyle.PNG)



This treemap shows the number of bedrooms and the number of washrooms with the average sold price 
![](Images/BedWashAvgPrice.PNG)



This pie chart displays the 5 different communities this data represents.  Each community displays the number of sold properities and the average sold house price.  
![](Images/Communities.PNG)


This bar graph shows the top ten real estate brokerage firms and their number of sold properties
![](Images/TopTen.PNG)


This box-whiskers-plot shows the data distrbution for the sold price according to the bedrooms, washrooms or kitchen which can be selected from a drop down menu. 
![](Images/WhiskersPlot.PNG)


This area charts displays the average number of days a property was listed for (Contract Date Signed - the Sold Date) according to diffent months
![](Images/AvgDays.PNG)

### Link to Tableau Dashboard

Dashboard 1 

By selecting one of the pie chart slices, a specific area of the city is selected, which then the treemap displays the average sold house price according to bedrooms and washrooms.  The area chart displays the average days a property lasted on the market.  
* [Link to Dashboard 1](https://public.tableau.com/shared/K8Y47Z48K?:display_count=n&:origin=viz_share_link)

Dashboard 2 

By selecting one of the pie chart slices, a specific area of the city is selected, which then the bar graphs displays the average sold price (according to house type, and house style) and the  difference in price from the ([Sold Price]-[List Price]) (orange line)
* [Link to Dashboard 2](https://public.tableau.com/views/Final1_16229308570450/DashboardAvgDiff?:language=en-US&:display_count=n&:origin=viz_share_link)

Dashboard 3

By selecting one of the pie chart slices, a specific area of the city is selected, and the top ten real estate brokerage firms with the most sold properties are displayed in the bar graph. The box-whiskers-plot displays the data distribution for the sold price by bedrooms, bathrooms, and kitchens, which can be selected from a drop-down menu.

* [Link to Dashboard 3](https://public.tableau.com/views/Final1_16229308570450/DashboardRealtorWhiskerPlot?:language=en-US&:display_count=n&:origin=viz_share_link)

