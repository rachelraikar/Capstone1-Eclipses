# Capstone1-Eclipses
Analysis of the trends of solar and lunar eclipses.

## Table of Contents

* [Files in Repository](#files-in-repository)
* [Project Outline](#project-outline)
* [Data Wrangling](#data-wrangling)
* [Data Analysis](#data-analysis)
* [Statistical Analysis](#statistical-analysis)
* [Machine Learning Predictions](#machine-learning-analysis)

## Files in Repository

* Report Separate Sections Folder - folder containing sections of final report as separate pdf files:
    * Data Wrangling, Data Storytelling, Statistical Analysis, Machine Learning Analysis
* Capstone 1: Milestone Report - pdf containing full report of project details
* Solar and Lunar Eclipse Milestone Report.pptx - Powerpoint summary of project 
* solar.csv & lunar.csv - data used for analysis in project
* Solar-and-Lunar-Eclipse-Capstone.ipynb - python notebook of code

## Project Outline

#### Problem Definition
* Study the frequency of occurrence of eclipses and determine which eclipses are more common.
* Study the correlation between time of year and occurrence of eclipses.
#### Client Base and Motivation
Astronomers to statistically confirm their theories about the occurrences of eclipses.
    
#### Data Overview
* Acquired from NASA public dataset domain.
* Two separate CSV files with data pertaining to solar and lunar eclipses respectively.
    
## Data Wrangling
* Imported CSV files as PANDAS dataframes and reindexed the rows with the column ‘Catalog number’.
* Filtered the data frames to contain only relevant columns:
   * Solar Eclipses Data Frame
      'Calendar Date', 'Eclipse Time', 'Delta T (s)', 'Eclipse Type','Eclipse Magnitude', 'Latitude', 'Longitude', 'Sun Altitude',    'Sun Azimuth',  'Path Width (km)', 'Central Duration'
   *  Lunar Eclipses Data Frame
        'Calendar Date', 'Eclipse Time', 'Delta T (s)','Eclipse Type', 'Latitude', 'Longitude',  'Penumbral Eclipse Duration (m)', 
        'Partial Eclipse Duration (m)','Total Eclipse Duration (m)'
* Reorganized data by calendar date in Chronological order
* Converted the dates into a list of [year, month, day] for easier analysis of trends.
* Note: The years have negative values because the data is during the five millennium period -1999 to +3000 (2000 BCE to 3000 CE).

* Missing values appearing as ‘-’ were replaced with NAN values.


## Data Story

#### Which type of eclipse is more common?
    There seem to be 166 more lunar eclipses than solar eclipses over a 5000 year period

#### How many solar/lunar eclipses per year on average?
    Solar: ~2.3796/yr
    Lunar: ~2.4128/yr
   
## Data Analysis

#### Is there a trend in eclipses vs. month?

    Solar and lunar eclipses seem to have relatively the same trend with every month
    The slight variation in frequency is due to lengths of the months

#### Trends in Total Eclipses

    Total solar eclipses seem to veer off this trend greatly. They seem to be more common during the second 
    half of the year during the seasons Fall and Winter (September - January). 
![TotalLunarCount](https://user-images.githubusercontent.com/40244616/66281728-6bdb6680-e871-11e9-9446-77fda9bf57fd.png)
![TotalSolarCount](https://user-images.githubusercontent.com/40244616/66281729-6f6eed80-e871-11e9-8289-fe947a866b35.png)

## Statistical Analysis
    Group 1: September - February (Fall - Winter according to US seasons)
    Group 2: March - August (Spring - Summer according to US season)

#### HYPOTHESIS TEST 
    To test the hypothesis that total eclipse is not directly correlated to the months in the year
    𝐻𝑜  : The probability of total eclipse occurring is the same for Group 1 and Group 2. (𝑝1=𝑝2)
    𝐻𝑎  : The probability of total eclipse occurring is not the same for Group 1 and Group 2. (𝑝1≠𝑝2)

#### Statistical Analysis of Total Solar Eclipse
     Confidence Interval: [-0.01568  0.01568]
     Observed Difference: -0.06719
     
     Therefore rejecting null hypothesis and showing that total solar eclipses might be correlated to the
     months in the year

<img width="628" alt="Screen Shot 2019-10-06 at 7 45 26 PM" src="https://user-images.githubusercontent.com/40244616/66281823-e1dfcd80-e871-11e9-9576-2e24755e55e5.png">


#### Statistical Analysis of Total Lunar Eclipse
    Confidence Interval: [-0.01149  0.01149]
    Observed Difference: -0.00560
    
    Therefore accepting null hypothesis and showing that total lunar eclipses are not directly correlated to 
    the months in the year

<img width="618" alt="Screen Shot 2019-10-06 at 7 45 16 PM" src="https://user-images.githubusercontent.com/40244616/66281827-e3a99100-e871-11e9-8c68-cc574797461d.png">

## Machine Learning Analysis

#### Goal :  
    Identify supervised learning techniques to predict the date of future total solar and lunar eclipses.

#### Hypothesis:
    It is possible to predict the time and date of the solar and lunar eclipses from the given data 
    leveraging machine learning regression algorithms. 

### Regression Models Tested

#### Linear Regression
* Model that uses ordinary least squares to minimize the sum of square differences from prediction from true value.
* The data was split into ordered train and test sets to keep the dates of the data in order.
   * Train = 0.75 Test = 0.25
* Fitted the training data to linear regression model and predicted the model on testing data. 

#### Ridge Regression
* Model similar to linear regression but with a normalization term to reduce overfitting. 
* The data was split into ordered train and test sets to keep the dates of the data in order.
   * Train = 0.75 Test = 0.25
* Performed GridSearchCV to find the best alpha parameter for the model and cross validation of 5.
* Plotted the alphas vs the cross validation of 10 scores for each alpha for visual analysis.
* Fitted the training data to ridge regression model and predicted the model on testing data. 

#### Lasso Regression
* Model similar to ridge regression but uses absolute values instead of squares to penalize regression coefficients 
from becoming too large. 
* The data was split into ordered train and test sets to keep the dates of the data in order.
   * Train = 0.75 Test = 0.25
* Performed GridSearchCV to find the best alpha parameter for the model and cross validation of 5.
* Plotted the alphas vs the cross validation of 10 scores for each alpha for visual analysis.
* Fitted the training data to lasso regression model and predicted the model on testing data. 

#### Polynomial Linear Regression
* Model similar to linear regression but y is modelled using an nth degree polynomial for x instead.
* The data was split into ordered train and test sets to keep the dates of the data in order.
   * Train = 0.75 Test = 0.25
* Performed a manual gridsearch to test for the best degree parameter for the Polynomial Features. Best degree = 4
* Fitted the training data to polynomial regression model and predicted the model on testing data. 

#### Bayesian Linear Regression
* Model similar to linear regression but the model is made with probabilities rather than point estimates.
* Performed GridSearchCV to find the best alpha and lambda parameters for the model with cross validation of 5.
* Fitted the training data to bayesian regression model and predicted the model on testing data. 


### Results for the Models

  Below are the Root Mean Square Errors (RMSE) computed for total solar and total lunar eclipses for each model.

| Model|Total Solar (yrs)|Total Lunar (yrs)|
| ------------- | :-------------: | :-------------: | 
|Linear Regression     |        4.8          |         5.4         |
|Lasso Regression      |        4.8          |         5.3         | 
|Ridge Regression      |        4.9          |         5.3         |
|Polynomial Regression |        4.6          |         4.4         |
|Bayesian Regression   |        4.8          |         5.4         |


