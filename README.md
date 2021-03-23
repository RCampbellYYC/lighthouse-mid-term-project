# **Lighthouse Labs Midterm Project 1**
## Predicting flight delays
  
<br />



**Group**

[Ryan Campbell](https://github.com/RCampbellYYC) <br>
[Renee Hall](https://github.com/rlwhall)<br>
[Tim Lau](https://github.com/lolwooops)<br>

**Description**<br>
GitHub repo for Lighthouse Labs midterm project.

**Goal** <br>
Predict arrival delays of commercial flights.

**Data** <br>
* **flights:** The departure and arrival information about flights in US in years 2018 and 2019.
* **fuel_comsumption:** The fuel comsumption of different airlines from years 2015-2019 aggregated per month.
* **passengers:** The passenger totals on different routes from years 2015-2019 aggregated per month.
* **flights_test:** The departure and arrival information about flights in US in January2020.

<br />

**Directories**
* **Final-files:** Copies of the final project files.
* **Working-copies-files:** Working file copies for each group member.

<br />

### Project Overview

**Data Selection**
* The ~15MM row flights data table was too large to handle on desktop PC’s
* Subsamples were taken for analysis and modelling
* Subsamples were randomly selected for flights with delays and no delays to ensure a balanced dataset.
* An **arr_delay** cutoff of zero was used for delay and no delay.
* Two sub samples were used:
  * **Subsample #1:** 600,000 samples used for initial modelling
  * **Subsample #2:** 50,000 samples used for subsequent modelling

<br />

**Data Exploration Tasks**
* Tasks were divided between team members
* There are a couple of notebooks for the exploratory tasks.

<br />


**Weather Data**
* World Weather API was used with Python API wrapper library
* 2018-2019 weather data was pulled for all airports and combined with flights and flights_test data.
<br />

**Data Exploration**
* There are a few different data exploration notebooks for each team members exploration
* The approach was to generally look at the whole dataset and the data tables were divided amongst team member to be looked into.
<br />

**Data Cleaning** 
* The samples taken from the flights data table and the other data tables were checked for missing values, duplicates, nan’s.
* Columns that would not be known for predictions, in terms of the flights_test dataset the team had to predict off of, were dropped.
* Where appropriate missing values were filled with a mean value.
<br />

**Feature Engineering and Selection**
* Many new features were created and tested. 
* Features were added and removed from the models in an iterative process to narrow in on the most important features.
* Feature importance with XGB and RF was used to rank features and help with feature selection.
* PCA was explored as a dimensionality reduction option.
* Both label encoding and dummy variable creation (one-hot encoding) were explored for categorical variables.
<br />

**Modelling – Classifier**
* Initially tried base regressor models, but encountered poor performance with noisy target variable arr_delay.
* Change direction and moved to classifier models.
* Created a number of different base classifier models.
* Base classifier results were poor.
* Iterated to improve base classifier model performance adding engineered features and other features from the data tables.
* Improved classifier model performance to a point, but then the models became unbalanced adding new engineered features (Ex: would overpredict delays).
* The team found the XGBoost model to have the best balance of performance and computational efficiency and therefore this was the main model used in the model runs.
* For the final classifier, the team circled back to an earlier classifier model that was balanced.
<br />

**Modelling – Regressor**
* Base regressor models were created
* Engineered features were added based on the results from the feature importance and selection work.
* A rolling 30-day **arr_delay** average was used to try to smooth the noisy target variable to improve the regressor performance.
* The final R^2 value was ~0.6, although it should be noted that the regressor predicts a rolling average value.
<br />

**Predicting on flights_test Dataset**
* A final classifier model was used to predict delay and no delay based on the flights_test dataset. It was found to be a marginal classifier and the results from it were not directly used. A cutoff of zero was used to define delay and no delay.
* A final regressor model using a rolling average approach was used to predict the delays that were submitted.
