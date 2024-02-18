# Practical-Application-Assignment-11.1

By: Mick Gram

Notebook: https://github.com/mickgram/Practical-Application-Assignment-11.1/blob/main/Practical-Application-Assignment-11.1.ipynb

ZIP file, extracted in root: https://mo-pcco.s3.us-east-1.amazonaws.com/BH-PCMLAI/module_11/practical_application_II_starter.zip

**What Drives the Price of a Car?**

**Objetive:** 
In this application, I will explore a dataset from kaggle. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing.  My goal is to understand what factors make a car more or less expensive.

**Method:** 
I used the CRISP-DM method, and the high level steps had the following findings:

**Business Understanding:**

- The dealership today sets prices based on their experience, rather than having a market based approach to understand what the price should be.
- In the car industry having a large inventory of cars is capital expensive so turn-around time is critical. To high a price will keep the car sitting on the lot to long. To low a price means that the dealership left room for additional profit.
- When customers try to negotiate for prices then understanding the true market price, will give the dealership more leverage.
- Knowledge about how especially different features impact the price can be valuable also.

**Data Understanding:**

Large dataset: The 426k dataset is assumed to be randomly picked from the original 3m dataset.
Offered or actual: According to Statistica(1) 38..6 million cars was sold in 2022. My first thought was if this was car put for sale, and hence the price would not reflect a true price of what it was sold for, but I will assume it is the actual sales price.

Private or Dealership: There is not a feature in the dataset saying if these prices were private sales or dealership sales. According to Kelly Blue Book theres is a significant difference, so for the sake of simplicity, then I will assume it is dealership prices.

History: There is not a feature identifying the time of the price (the sale), so it may historic price that could be impacted by changes in inflation, supply/demand and other market factors.
Freedom: The dataset is still very large at 426k which affords us to cut out a lot of records due to missing values, rather than approximating value of features for records not available. As I proceed I will of course keep an eye on this.

US vs Foreign: The dataset has a wide range of US and foreign based manufacturers, as well as electric and combustion engine cars, and for this I will focus on combustion. It also has a very wide range of ages of cars. I assume that this dealership focuses at cars maybe max 20-30 years old. I will look into that also.

**Cleaning / Filtering:**

- Removing columns id and VIN as they don't make sense for regression

- It's a large dataset so will remove records with null values and still have a considerable dataset.

- I assume that car dealership only sell the following:

- American cars (no Tesla or Harley-Davidson)

- Cars with Odometer < 100,000,

- Cars from 2000 until today

- Cars at prices below < 50,000

- I will create a new features called "manufacturer_type" and see if it has any correlation.

**Correlation:**

The heatmap used found the following features to be most relevant for modeling: 
- year, cylinders, odometer, fuel, type, manufacturer, size, condition

**Data Preparation:**

Data was hot-encoded and scaled peoperly.


**Modeling:**

I tried multi regression, pipeline with SFS and regression, Ridge and Lasso and GridSearchCV.

All models were close in result but GridSearchCV gave the best fit with these metrics:

- Fitting 5 folds for each of 9 candidates, totalling 45 fits
- Best parameters found: {'alpha': 100}
- MSE: 55,602,801
- R^2: 0.6404

**The unscaled features were  the following: (top 20 impact, rest can be found in notebook)**

![image](https://github.com/mickgram/Practical-Application-Assignment-11.1/assets/153389917/4982d4b4-4229-4d20-98d0-063c13707502)



**The actual vs Predicted:**

I did the following plot of actual vs predicted based on the chosen model:

![image](https://github.com/mickgram/Practical-Application-Assignment-11.1/assets/153389917/8e8f431e-83a6-405c-81ec-e5a4646bea97)

Prediction appears to have a good overlap with actuals, but of course areas that could be better explained.
Especially the negative values are of concern, and the model also doesn't do well at the top price point.

**Reflections**

Raw data:
I wished time of sale would have been made available in the raw data. That could have played in as car prices especially around 2021 increased a lot for used cars.

Correlations:
It would have been interesting to work a bit more with categorizations to see if I could have maybe done something with manufacturer, type and model.

Models:
I wondered why the simple multi regression was so close to the other models and why I didn't see much of a difference. I would love to learn more and dig into that.
