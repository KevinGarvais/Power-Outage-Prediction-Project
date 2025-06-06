# Predicting Power Outage Durations
Data Science Project for DSC80 at UCSD
by Adam Walters and Kevin Garvais


# Introduction
In this project, we examined a dataset compiling major power outages in the continental U.S. dating from January 2000 - July 2016. The outages in the dataset were compiled by the Department of Energy and were known to impact at least 50,000 customers or caused an unplanned energy demand loss amounting to at least 300 MegaWatts of power. We accessed this dataset from Purdue University’s Laboratory for Advancing Sustainable Critical Infrastructure. Link to the dataset: https://engineering.purdue.edu/LASCI/research-data/outages.

The dataset records a plethora of information about the power outages in question. This data includes geographical, climatic, urban/rural land-use attributes, and electricity consumption and economic characteristics of the state involved.

In this project, we will first clean our dataset and come to understand it through exploratory data analysis. Then, we will analyze missingness in the dataset and missingness dependency among columns. 

This will set us up to answer our research question: What characteristics of a power outage contribute most to its duration? Continuing with this question, we will build a prediction model and will take in information about a power outage and predict its duration. This type of model would be very important for first responders and people affected by the outage so they can effectively prepare for an accurate duration of power loss.

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
|`'OUTAGE.RESTORATION.DATE'`                |Day of the year when power was restored to all the customers|
|`'OUTAGE.RESTORATION.TIME'`                |Time of the day when power was restored to all the customers|
|`'CAUSE.CATEGORY'`                |Categories of all the events causing the major power outages|
|`'OUTAGE.DURATION'`                |Duration of outage events|
|`'CUSTOMERS.AFFECTED'`                |Number of customers affected by the power outage event|
|`'POPPCT_URBAN'`                |Percentage of the total population of the U.S. state represented by the urban population (in %)|
|`'POPDEN_URBAN'`                |Population density of the urban areas (persons per square mile)|
|`'AREAPCT_URBAN'`                |Percentage of the land area of the U.S. state represented by the land area of the urban areas (in %)|


# Data Cleaning and Exploratory Data Analysis
Before going any further, let's ensure our data is clean and ready to use for our analysis.

## Data Cleaning




# Assessment of Missingness



# Hypothesis Testing



# Framing a Prediction Problem



# Baseline Model



# Final Model



# Fairness Analysis
