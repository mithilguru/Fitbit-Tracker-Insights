# Fitbit Tracker Insights
## Project Overview



## Intro

Fitbit is a fitness technology company that produces wearables to monitor daily health and activity data, such as heart rate, steps, sleep-quality, etc. There is a tremendous amount of data collected by these wearable devices daily that can be harnessed to benefit the consumer and the company. I am exploring the Fitbit fitness tracker data Kaggle dataset (https://www.kaggle.com/arashnic/fitbit) to find trends in usage and provide recommendations for product strategy. 

**OBJECTIVES**

**1. Discover trends in usage**

**2. Generate recommendations for product strategy**

The data description indicates it is generated from respondents to a survey in 2016. It includes consented data from the personal trackers of thirty users.

**DATA - Assessment**

The data source is not ideal, as the sample size is only 30, the survey was conducted and compiled by a third-party organization, and the data may be slighlty inconsistent - due to the source including data from different trackers - and outdated as current trackers have improved capabilities. Additionally, there is a possibility of voluntary response bias due to the participants consenting to take place in the study, which may have influenced their habits during the course of the study. There is also no extra information provided about the participants, so the sample may not be truly representative of the general population.

Despite the limitations, the dataset is chosen for analysis since it is one of the few publicly available sources with Fitbit tracker data - most tracker data is locked for user privacy. The only alternative for reliable data would be to self-analyze Fitbit data with the use of the Fitbit API, but this limits study to one subject. 

**DATA - Summary**

The data includes 18 total datasets (CSV files) representing data collected by the trackers. A quick search through the files revealed that most of the data was collected and compiled in the dailyActivity.csv dataset, and the remaining files contain specific intervals or variations of the quantitative data. Most of the data is explained in the dailyActivity file, and the sleepDay file provides additional information for analysis. The hourlySteps and hourlyIntensities datasets also supplement the daily activity data. The remaining datasets can be condensed. 

**DATA - Features** 

All variables are quantitative.

**Steps** - total steps per day

**Intensity** - sorted by level (Sedentary, Lightly Active, Fairly Active, Very Active) for distance and time

Levels of activity intensity (source: fitbit.com) - 
0 = sedentary time - time spent immobile/seated (i.e. sitting at work/school).
1 = lightly active time - time spent walking throughout the day (i.e. walking around home, to and from work, etc.).
2, 3 = fairly active, very active time - time spent for specific workout/exercise activity (i.e. running, lifting, sports, etc.).

**Calories** - total calories burned per day

**Sleep** - total sleep sessions per day, minutes asleep, time in bed

## Methods 

Utilizing SQL (BigQuery database) to perform the initial data preparation and R (dplyr) for additional data transformation and visualizations, as well as a Tableau dashbaord for supplemental visuals.

The data was processed in SQL to - 
* Check for distinct users
* Merge tables
* Remove missing values and duplicates
* Identify mistyped data
* Adjust columns (date/time transformations)

## Analysis

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Usage-DoW.png?raw=true "Total Logs by Day of Week")

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Distributions-1.png?raw=true "Daily Activity Distributions")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Distributions-2.png?raw=true "Remaining Daily Distributions")

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Steps-Wk.png?raw=true "Average Steps during Week")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Activity-Intensity-Wk.png?raw=true "Activity Intensity during Week")

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Intense-Activity-G.png?raw=true "Daily Intense Activity by Group")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Inactivity-G.png?raw=true "Daily Inactivity by Group")

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Corrplot.png?raw=true "Correlation Plot")

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Steps-V-Cals.png?raw=true "Daily Steps vs Calories")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Steps-V-Sleep.png?raw=true "Daily Steps vs Sleep")


## Discussion
