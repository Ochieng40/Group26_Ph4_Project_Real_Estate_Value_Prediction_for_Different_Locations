# Group26_Ph4_Project_Real_Estate_Value_Prediction_for_Different_Locations
## 1.0 Business Understanding

MDN real estate investment firm is currently looking to expand their horizons and invest in different locations that are predicted to do well in the next few years. The company wants to do their due diligence and have data drive their decisions

Due to their need for data, the company requested us,the data analyst constultants, develop a model that can predict the future of real estate in different states. MDN seeks to gain insight into the best locations to invest in and help advise clients where to buy property.

This project uses Time Series modelling to build predictive models for Real Estate prices in USA. 

The project will utilize Real Estate data from Zillow Research.

### Specific Objectives:
- Identify the top 10 states with well to do real estate
- Identify the top 10 zipcodes with highest value of property
- Develop Time series models that can forecast the future of real estate prices

## 2.0 Data Understanding
* We observe that the data is in wide format.There are 272 columns, of which the first 7 are RegionID, RegionName, City, State, Metro, CountyName and SizeRank. The remaining 265 are the actual Time Series values stored in separate columns.

* There are 14723 rows.
* We also note that the RegionName column denotes Zipcodes.

## 3.0 Data Preparation
* Looking at the states, District of Columbia has the highest average value of property, followed by California and Hawaii.

* The zipcode with the highest average value of property is zipcode 10021 in Newyork. Zipcode 10021 is in the neighbourhood of Lenox Hill|Upper East Side|Uptown|Manhattan (www.unitedstateszipcodes.org)

* The first four highest value zipcodes are all in Newyork.3 zipcodes from Californa also appear in the top 10 zipcodes.


## 4.0 EDA
* It is oserved that, of the top 10 zipcodes, 4 have some missing values of property while 6 don't. It is also noted that for those with missing values, the missing data ranges from years 1996 to 2005.

* **We select zipcode 10128 in Newyork, which is the fourth highest in terms of property value, as it has no missing values and would thus offer more data for modelling.**  
* There are 265 rows i.e. monthly property value for about 22 years between April 1996 to April 2018
### Dickey Fuller test
* From the Dickey Fuller test we observe a p-value of 0.93 which is greater than alpha (0.05)
* We therefore fail to reject the null hypothesis and conclude that the data is not stationary
* We will thus proceed to making the data sationary by removing trends.

## 4.0 Modeling
* We ran 3 model iterations for the zipcode of interest and select the best performing model.The 3 model types chosen are:
    1. Arima model as baseline
    2. Arima model using PMDArima to get best parameters
    3. FB Prophet model
    
### Autocorrelation function (ACF) and partial autocorrelation function (PACF)
* We observed a strong autocorrelation for the first lag and then a weak/declining autocorrelation.
* From inspecting the PACF plot, we can pick 'p' for our ARIMA base model. We observe that the 1st lag is the most significant and can thus set the Auto Regressive(AR) parameter to 1.
* Similarly, from inspecting the ACF plot, we pick 1 as the parameter for the Moving Average(MA).
* Therefore our baseline model is set to the order of 1,0,1

## 5.0 Model Evaluation
### Evaluation metrics:
* We used Root Mean Squared Error (RMSE) and R2 score as evaluation metrics to compare different models performance.

### Model Evaluation Results
* The baseline ARIMA model had an AIC of 6460 and a BIC of 6474. TheR2 score is about 73.6% and the RMSE is about 48,866 
* Predictions have also been made for 24 months beyond the current dataset i.e. from May 2018 to April 2020
* We then proceed to investigate optimal valus of the parameters using PMD ARIMA for the second iterative model.

* The second ARIMA model has an AIC of 6415 and a BIC of 6433. TheR2 score is about 75.6% and the RMSE is about 46,931 
* This is a better performing ARIMA model than the baseline model which had an R2 score of 73.6% and RMSE of 48,866 .
* Predictions have also been made for 24 months beyond the current dataset i.e. from May 2018 to April 2020
* We then proceed to create a third model using FB prophet.

* The third model, an FB prophet model produces an RMSE of 16821 and is therefore the best performing model of the three.
* Predictions have also been made for 24 months beyond the current dataset i.e. from May 2018 to April 2020

## 6.0 Findings
* We used the zillow real estate data to find the top 10 zipcodes in terms of property value. Zipcode 10128 in Newyork is used to build 3 iterative models to predict the future housing prices. This zipcode is used as a prototype to build the models, and the model can be scaled to any other zipcode of interest.

* The 3 models created are a baseline ARIMA model, an ARIMA model with parameters from pmdarima and a final model using FBProphet. 

* The three models have been evaluated for the Zipcode 10128 in Newyork using RMSE as the metric of evaluation. The resultant RMSEs are:

    * 48,866(baseline ARIMA Model of orde 1,0,1),
    * 46,931 (Second Arima Model of order 2,1,2)
    * 16,821 (the final model usingFB prophet)
    
* From the foregoing results, the FB prophet model performs best in predicting future real estate prices of the Zipcode 10128 in New York.

## 7.0 Conclusions
* The top 10 states with highest average value of property are: 
    1. District of Columbia (DC)
    2. California (CA)
    3. Hawaii (HI)
    4. New Jersey (NJ)
    5. Massachusetts (MA)
    6. Maryland (MD)
    7. New York (NY)
    8. Connecticut (CT)
    9. Colorado (CO)
    10. Washington (WA)
    
* The top 10 zip codes with highest value of property are:
    1. 10021 in New York
    2. 10011 in New York
    3. 10014 in New York
    4. 10128 in New York
    5. 94027 in California
    6. 81611 in Colorado
    7. 90210 in California
    8. 33480in florida
    9. 94123 in California
    10. 31561 in Georgia
    
* Three models are created for predicting value of property abase Arima model using parametrs from PACF and ACF plots; A second Arima model using parameters PMD Auto Arima and a third model using FB prophet. The best performing model of the three  is the third model using FB Prophet algorithm, for the zipcode 10128 in NewYork.

* Based on the predictions made for property values for the next 2 years, we are able to observe a flactuation(rise and fall) in property values for zipcode 10128 in New York, but in the end we are able to observe an increase in price. Investing in this property values carries its risks for investors aiming to buy and later sell.


## 7.0 Recommendations
* We would advise the client, MDN real estate investment firm to focus on the top 10 highest value states and top 10 zipcodes in assessing the areas with a higher future value of property.

* We would further advise the client to mitigate against risk, by not investing in one area only. For example, the top 4 zipcodes with highest value of property are all in New York. We would advise spreading of risk by looking into other zipcodes and states within the top 10.

* We also advise MDN consultants to make use of the FB Prophet model in predicting the future value of property as it performed best. Nonetheless, each different zipcode should be assessed independently on the three models.

* More data is needed to improve model performance.

* Other research may also be needed eg PESTEL analysis to complement the model findings.

## 7.0 Next Steps
* Though this project focused on one zipcode for model building, we propose further work in creating and running predictive models for all the top 10 zipcodes to compare and assess which zipcodes are likely to have best performance in the future based on the predictive models.  
 






  
