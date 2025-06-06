# Predicting Power Outage Durations
Data Science Project for DSC80 at UCSD
by Adam Walters and Kevin Garvais


# Introduction
In this project, we examined a dataset compiling major power outages in the U.S. dating from January 2000 - July 2016. The outages in the dataset were compiled by the Department of Energy and were known to impact at least 50,000 customers or caused an unplanned energy demand loss amounting to at least 300 MegaWatts of power. We accessed this dataset from Purdue University’s Laboratory for Advancing Sustainable Critical Infrastructure. Link to the dataset: https://engineering.purdue.edu/LASCI/research-data/outages.

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

## Exploratory Data Analysis

### Univariate Analysis

We began with univariate analysis of total outages across different variables.

First, we examined how many outages each `'CAUSE.CATEGORY'` had:


<iframe
  src="assets/univariate_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The plot shows that severe weather and intentional attacks account for the majority of outages in our data.


Then, we looked at the total outages by U.S. region:

<iframe
  src="assets/univariate2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The plot indicates a fairly even distribution of outages apart from the Northeast and West North Central regions. The Northeast has far more outages and the West North Central, far fewer outages.


### Bivariate Analysis

Next, we wanted to look at how two variables interacted with each other inside our data.

First, we examined which U.S. states had the most yearly outages:

<iframe
  src="assets/bivariate_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The map indicates that California and Texas have the most yearly outages by far, while other states with lower populations tend to have less outages.

Next, we looked at the median outage duration for each state:

<iframe
  src="assets/bivariate_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The map indicates that many western states experience far shorter power outages than eastern states.

Lastly, we took a look at the median outage duration for each outage cause:

<iframe
  src="assets/bivariate_3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The bar graph indicates that fuel supply emergencies and severe weather often result in far longer outage durations as opposed to other causes.

### Interesting Aggregates

We grouped outage causes together and put them into a pivot table alongside the year in which the outages occurred. This pivot table would allow us to examine how the median duration of an outage of a certain cause may change over time. 

| CAUSE.CATEGORY                |     2000 |      2001 |     2002 |     2003 |     2004 |     2005 |    2006 |      2007 |      2008 |      2009 |      2010 |
|:------------------------------|---------:|----------:|---------:|---------:|---------:|---------:|--------:|----------:|----------:|----------:|----------:|
| equipment failure             |  0       |   8.23333 |  0       |  2.59167 |  3.68333 |  2.48333 |  2.65   |  3.43333  |   4.48333 |  15.45    |   4.91667 |
| fuel supply emergency         |  0       |   0       |  0       |  0       |  0       |  0       |  0      | 27.9333   | 396       | 109.5     | 168       |
| intentional attack            |  0       |   0       |  0       | 22.1583  |  0       |  0       |  0      |  0        |   0       |   0       |   0       |
| islanding                     |  0       |   0       |  0       |  0       |  0       |  0       |  0      |  0.783333 |   3.725   |   4.84167 |   2.03333 |
| public appeal                 |  0       |   2.33333 |  0       | 25.8     | 72       |  0       |  5.95   | 40.5083   | 100.958   |   5       |   8.53333 |
| severe weather                | 41.5     | 169       | 86       | 62.2333  | 34.5     | 73.5     | 45.5417 | 25.5      |  53       |  45.1667  |  48.875   |
| system operability disruption |  6.25833 |   4.01667 |  3.83333 | 44.9     |  1.58333 |  4.11667 |  3.95   |  6.91667  |   3.24167 |   1.775   |   3.31667 |


# Assessment of Missingness

## NMAR Analysis

One column that stands out in our dataset as potentially NMAR (Not missing at random) is `'CUSTOMERS.AFFECTED'`. We believe this could be the case because if the number of customers affected isn't listed, it could mean that not very many people were affected by the outage and thus the companies did not go through the effort to count affected customers. 

If we had additional data indicating the land-area that was affected by the outage, we could perhaps explain the absence of customers affected as MAR.

## Testing Missingness Dependency

The subject of our missingness dependency test will be the `'OUTAGE.DURATION'` which is missing in 58 of the power outages. We will be testing to see the missingness of outage duration is dependent on `'CLIMATE.REGION` or `'CAUSE.CATEGORY'`.

### Testing dependency on Climate Region

Lets start by testing if the outage duration's missingness is dependent on the climate region of the outage.

**Null Hypothesis:** The distribution of an outage duration's missingness is not different depending on the climate region.

**Alternate Hypothesis:** The distribution of an outage duration's missingness is different depending on the climate region.

To test these hypotheses, we will be taking the difference in maximum missingness proportion and minimum missingness proportion between each climate region.

<iframe
  src="assets/CLIMATE.REGION_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


I found an observed difference in proportions of 0.054 which had a p-value of 0.238 so we failed to reject the null hypothesis. So, we assume that the climate region has no impact on the missingness of the outage duration.

<iframe
  src="assets/CLIMATE.REGION_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Testing dependency on Cause Category

Next, lets  test if the outage duration's missingness is dependent on the cause of the outage.

**Null Hypothesis:** The distribution of an outage duration's missingness is not different depending on the outage cause.

**Alternate Hypothesis:** The distribution of an outage duration's missingness is different depending on the outage cause.

To test these hypotheses, we will be taking the difference in maximum missingness proportion and minimum missingness proportion between each outage cause.


<iframe
  src="assets/CAUSE.CATEGORY_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


I found an observed difference in proportions of 0.255 which had a p-value of 0.0 so we reject the null hypothesis. So, we can assume that the missingness of an outage duration does depend on the cause of the outage.

<iframe
  src="assets/CAUSE.CATEGORY_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



# Hypothesis Testing

**For our hypothesis test, we will be testing if "warm" climate category has a significant impact on increasing the duration of a power outage.**

Our null hypothesis is: Warm climate does not increase the duration of a power outage.

Our alternate hypothesis is: Warm climate does increase the duration of a power outage.

Our test statistic is the difference of means. Specifically, the difference in means of the average outage duration overall vs. the average outage duration for warm climates.

For our significance level, we will choose a p-value of 0.05.

We performed a permutation test with 1,000 simulations that shuffled the climate categories of each outage. In these 1,000 simulations we stored the difference in means and compared it to our observed test statistic.

Our observed test statistic was 3 days 13 minutes and 18 seconds and when comparing it to our 1,000 simulations we got a p-value of 0.279 meaning we fail to reject the null hypothesis. So, we assume that climate category has no impact on the duration of a power outage. This is useful information because we now know that climate category is not a good indicator of power outage duration.

# Framing a Prediction Problem

We will create a model that aims to predict the duration of a power outage. This will be a regression model since the duration of an outage is a continuous variable and not a categorical one.



# Baseline Model



# Final Model



# Fairness Analysis
