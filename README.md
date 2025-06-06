# Predicting Power Outage Durations
Data Science Project for DSC80 at UCSD
by Adam Walters and Kevin Garvais


# Introduction
In this project, we examined a dataset compiling major power outages in the continental U.S. dating from January 2000 - July 2016. The outages in the dataset were compiled by the Department of Energy and were known to impact at least 50,000 customers or caused an unplanned energy demand loss amounting to at least 300 MegaWatts of power. We accessed this dataset from Purdue University’s Laboratory for Advancing Sustainable Critical Infrastructure. Link to the dataset: https://engineering.purdue.edu/LASCI/research-data/outages.

The dataset records a plethora of information about the power outages in question. This data includes geographical, climatic, urban/rural land-use attributes, and electricity consumption and economic characteristics of the state involved.

In this project, we will first clean our dataset and come to understand it through exploratory data analysis. Then, we will analyze missingness in the dataset and missingness dependency among columns. 

This will set us up to answer our research question: What characteristics of a power outage contribute most to its duration? Continuing with this question, we will build a prediction model and will take in information about a power outage and predict its duration. This type of model would be very important for first responders and people affected by the outage so they can effectively prepare for an accurate duration of power loss.


# Our Dataset

Our original raw dataset contains 1534 rows and 57 columns, corresponding to unique outages and outage characteristics respectively. Here are the columns most notable for our future analysis.

|Column                |Description|
|---                |---        |
|`'YEAR'`                |Year when outage occurred|
|`'MONTH'`                |Month when outage occurred|
|`'U.S._STATE'`                |State the outage occurred|
|`'POSTAL.CODE'`                |Two-lettter state abbreviations|
|`'CLIMATE.REGION'`                |U.S. Climate regions as specified by National Centers for Environmental Information (9 Regions)|
|`'CLIMATE.CATEGORY'`                |“Warm”, “Cold” or “Normal” episodes of the climate that are based on a threshold of ± 0.5 °C for the Oceanic Niño Index (ONI)|
|`'ANOMALY.LEVEL'`                |Oceanic El Niño/La Niña (ONI) index referring to the cold and warm episodes by season|
|`'OUTAGE.START.DATE'`                |Day of the year when the outage event started|
|`'OUTAGE.START.TIME'`                |Time of the day when the outage event started|
|`'OUTAGE.START.TIME.DATE'`                |Date and time of the day when the outage event started|
|`'OUTAGE.RESTORATION.DATE'`                |Day of the year when power was restored to all the customers|
|`'OUTAGE.RESTORATION.TIME'`                |Time of the day when power was restored to all the customers|
|`'OUTAGE.RESTORATION`                |Date and time of the day when power was restored to all the customers|
|`'CAUSE.CATEGORY'`                |Categories of all the events causing the major power outages|
|`'OUTAGE.DURATION'`                |Duration of outage events|
|`'CUSTOMERS.AFFECTED'`                |Number of customers affected by the power outage event|
|`'POPPCT_URBAN'`                |Percentage of the total population of the U.S. state represented by the urban population (in %)|
|`'POPDEN_URBAN'`                |Population density of the urban areas (persons per square mile)|
|`'AREAPCT_URBAN'`                |Percentage of the land area of the U.S. state represented by the land area of the urban areas (in %)|


# Data Cleaning and Exploratory Data Analysis
Before going any further, let's ensure our data is clean and ready to use for our analysis.

## Data Cleaning
1. We started by dropping the initial rows of the set which served only to explain characteristics of the columns
2. Then, we combined our `'OUTAGE.START.DATE'` & `'OUTAGE.START.TIME'` to create `'OUTAGE.START.TIME.DATE'` a columns of datetime objects which have the exact date and time when the outage occurred. We did a similar process for our restoration columns, creating `'OUTAGE.RESTORATION'` a column of datetime objects that have the exact date and time when the power was restored.
3. Lastly, we created the `'OUTAGE.DURATION'` column which was made by subtracting the restoration time by the start time, leaving us with a datetime object that amounted to the duration of the outage.
4. We named the dataframe that results from this `'clean_included_null_df'` because it includes null values for `'OUTAGE.DURATION'` and then made a new dataframe called `'clean_outages_df'` which drops null values for `'OUTAGE.DURATION'`. Both of these dataframes will be helpful in analysis going forward.

Here is a snippet of our `'clean_outages_df'` dataframe with some key columns:

|   YEAR | OUTAGE.DURATION   | POSTAL.CODE   |   ANOMALY.LEVEL | CLIMATE.CATEGORY   |   CUSTOMERS.AFFECTED |
|-------:|:------------------|:--------------|----------------:|:-------------------|---------------------:|
|   2008 | 14 days 04:16:00  | LA            |            -0.3 | normal             |                50000 |
|   2005 | 1 days 07:05:00   | GA            |            -0.7 | cold               |                52659 |
|   2004 | 0 days 13:30:00   | GA            |             0.3 | normal             |                47165 |
|   2011 | 0 days 17:26:00   | MI            |            -0.9 | cold               |                    0 |
|   2014 | 0 days 00:52:00   | LA            |            -0.2 | normal             |                28000 |



# Assessment of Missingness



# Hypothesis Testing



# Framing a Prediction Problem



# Baseline Model



# Final Model



# Fairness Analysis
