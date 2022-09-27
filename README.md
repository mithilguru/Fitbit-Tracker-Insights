# Fitbit Tracker Insights
## Project Overview



## Intro

Fitbit is a fitness technology company that produces wearables to monitor daily health and activity data, such as heart rate, steps, sleep-quality, etc. There is a tremendous amount of data collected by these devices daily that can be harnessed to benefit the consumer and the company. I am exploring the Fitbit fitness tracker data Kaggle dataset (https://www.kaggle.com/arashnic/fitbit) to find trends in usage and provide recommendations for product strategy. 

**OBJECTIVES**

**1. Discover trends in usage**

**2. Generate recommendations for product strategy**

The data description indicates it is generated from respondents to a survey in 2016. It includes consented data from the personal trackers of thirty users.

**DATA - Assessment**

Assessing the data source shows - the sample size is 30, the survey was conducted and compiled by a third-party organization, and the data may be slightly inconsistent, due to the source including data from different trackers, and outdated as current trackers have improved capabilities. Additionally, there is a possibility of voluntary response bias due to the participants consenting to take place in the study, which may have influenced their habits during the course of the study. There is also no extra information provided about the participants, so the sample may not be truly representative of the general population.

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

Used SQL (BigQuery database) to perform the initial data preparation and R (dplyr) for additional data transformation and visualizations, as well as a Tableau dashbaord for supplemental visuals.

The data was processed in SQL to - 
* Check for distinct users
* Merge tables
* Remove missing values and duplicates
* Identify mistyped data
* Adjust columns (date/time transformations)

## Analysis

**Usage**

Initial exploratory analysis involved understanding usage patterns. The study spanned exactly one month (31 days), and ideally the majority of users logged data every day. The data revealed that the majority of users did meet this criteria. 

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Usage-DoW.png?raw=true "Total Logs by Day of Week")

Viewing usage specific to the date / day of week shows that the total number of logs are generally higher during the mid-week (Tuesday, Wednesday, Thursday) by a small margin. 

**Activity**

Data summaries suggest most users are generally active (median 7439 steps a day). The vast majority of time is spent being sedentary (expected), and the median time spent in intense activity is only 11 minutes (4 very active minutes, 7 fairly active minutes). The mean intense activity values are much higher for both (21 very active minutes, 13 fairly active minutes) hinting at a skewed distribution likely due to only a small portion of users having a regular workout routine. Users average around ~7 hours of sleep a night on average. These distributions are shown below.

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Distributions-1.png?raw=true "Daily Activity Distributions")

The histograms of the activity variables are in-line with the initial observations: active entries are right-skewed (biased by a select few active users) as shown by the skewed distributions of total distance, total steps, very active minutes, and fairly active minutes. The sedentary minutes distribution contrasts this, as expected, since it is left skewed (predominantly high sedentary values, a few active (low minutes) entries) and also bi-modal (two peaks). Now checking sleep and calorie variables next.

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Distributions-2.png?raw=true "Remaining Daily Distributions")

Viewing the calorie burn distribution, it is slightly right-skewed (aligns with activity data) and centered around ~2000 calories. The time asleep distribution is mostly symmetrical with no obvious outliers. 

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Steps-Wk.png?raw=true "Average Steps during Week")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Activity-Intensity-Wk.png?raw=true "Activity Intensity during Week")

Viewing the step data, users are typically most active around midday on the weekends and late afternoon / early evening on weekdays. Intensity data essentially mirrors the step data, suggesting the users' intense exercise is typically step-based (i.e. running). Now grouping users based on activity level.

Users were categorized into three different activity groups: Average (<5000 steps), Active (5000-9999 steps), and Very Active (10000+ steps) based on daily average step totals. 

Over half of the users fall into the 'Active' category (18 users), and an even amount of 'Average' and 'Very Active' users make up the rest of the sample (8 average users, 7 very active users). Viewing activity trends between groups, as well as relationships between other variables below.

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-IntenseActivity-G.png?raw=true "Daily Intense Activity by Group")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Inactivity-G.png?raw=true "Daily Inactivity by Group")

Observing activity distributions between groups via boxplot and ANOVA tests shows that there are significant differences in high intensity activity minutes between groups as expected - 'Very Active' level users are have higher active minutes than 'Average' level users. Similarly, there are significant differences between groups for sedentary minutes as well - 'Average' level users have higher sedentary minutes than 'Very Active' level users.
Interestingly, the median level inactivity in the middle 'Active' group is much lower than the 'Very Active' group (although the range is higher), indicating that there is a select group of users that schedule their day around periods of high-intensity activity while otherwise being generally sedentary.

**Relationships**

Plotting the correlation matrix of the variables gives a quick look into variable relationships at a glance.

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Corrplot.png?raw=true "Correlation Plot")

Looking at the overall linear (Pearson's) correlations between all the variables, the strongest associations are between activity variables (steps, distance, active minutes) as well as calories. Specifically, higher very active and fairly active minutes are strongly related with more steps and distance (r = .67, .68). 

![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Steps-V-Cals.png?raw=true "Daily Steps vs Calories")
![alt text](https://github.com/mithilguru/Fitbit-Tracker-Insights/blob/main/Visuals/Daily-Steps-V-Sleep.png?raw=true "Daily Steps vs Sleep")

Finally, seeing activity (steps) in relation to calories shows that there is a moderate positive correlation between total calories and calories burned (expected). There is no apparent relationship between activity (steps) and time asleep (also expected). Current Fitbit trackers give more detailed insight into sleep time and sleep quality that can be used to better identify sleep habits and relationships with other factors. Additional supplemental visualizations can be viewed on Tableau Public.



## Discussion

**Summary**

Analyzing the activity and sleep data of the sample gives a general idea of the usage of a typical Fitbit tracker. The most immediate observation is that users **do not** log all of the available information from the tracker. Only the daily activity and sleep data meet sample size requirements for statistical analysis (~30 users). 
This is interesting to note, as trackers do have advanced capabilities that can give users more detailed insight on their day-to-day health, yet these features are not being used *in this sample*. This should be investigated further in an official future study.

The available activity data showcases a general trend in usage - activity levels are spread across a spectrum. There is a *highly active* subset of users that regularly perform intense workouts, and there is a *sedentary* subset of users that generally limit activity to light movement. The remaining users are spread in-between the two groups. 
The strongest trend is the correlation between intense activity, steps, and distance. This is also seen with the hourly intense activity aligning with hourly steps data. The typical activity of Fitbit users suggests the intense activity is mostly running.

Sleep data is also provided, but without the in-depth metrics on sleep phases and sleep quality, it is difficult to define any associations between activity patterns and sleep. More importantly, the **lack of** detailed sleep data in the sample suggests that users may not be inclined to track their sleep patterns in detail.

**Recommendations**

Priority for future product strategy must be centered around increasing device usage.
Higher device usage -> greater user fitness/satisfaction -> more device and service sales

**1. Integrate detailed fitness tracking seamlessly**

As noted in the summary, more detailed data utilizing all aspects of the tracker can help the user better understand their health and activity habits. The Fitbit app allows users to view this at a glance, and it should be easy-to-configure and enabled by default. Since a user is likely purchasing this device to improve their fitness, it should be expected that the tracker is used optimally. Notifications can be centered around encouraging *device usage*, to indirectly help motivate forming consistent healthy exercise habits.

**2. Emphasize social fitness goal-setting**

One of the key features of the Fitbit app is the ability to share progress with friends and family. Social motivation is a strong influence in helping people build a fit lifestyle. This should be the focus of the app in addition to the detailed tracking. The combination of tracking and sharing progress leads individuals towards *using* the device and app above all. 

An important aspect to track while implementing these recommendations is to understand user behavior and perceptions towards fitness data tracking. Studies show that while people who would like to maintain a healthy lifestyle are inclined to purchase and use fitness trackers, there is fine line between encouragement and pressure. Notifications and tracking cannot cross the ethical boundaries of overwhelming users with data. Thus, future study should be centered around a stronger sample of both regular and irregular users conducted by first-party researchers to get a better grasp of usage tendencies.

View the R project for the full report and analysis. Thank you!
