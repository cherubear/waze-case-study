# Waze Case Study
A capstone project for Google Advanced Data Analytics Certificate program

![waze logo](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/xCm_NX3ARhGby5yNHxROZg_2a48fa4727ec4aaf9bd7e063838687f1_image.png?expiry=1734220800000&hmac=r4m5ThWUxUCukD3KMsbUTUpPK9-88YTDRkB_lC0TxfI)

## Executive Summary
![Waze - Executive summary](https://github.com/user-attachments/assets/a64b0898-49c0-4f20-a5a8-aea36d851636)

## Introduction

### Background on the Waze scenario

Waze’s free navigation app makes it easier for drivers around the world to get to where they want to go. Waze’s community of map editors, beta testers, translators, partners, and users helps make each drive better and safer. Waze partners with cities, transportation authorities, broadcasters, businesses, and first responders to help as many people as possible travel more efficiently and safely. 

You’ll collaborate with your Waze teammates to analyze and interpret data, generate valuable insights, and help leadership make informed business decisions. Your team is about to start a new project to help prevent user churn on the Waze app. Churn quantifies the number of users who have uninstalled the Waze app or stopped using the app. This project focuses on **monthly user churn**. 

This project is part of a larger effort at Waze to increase growth. Typically, high retention rates indicate satisfied users who repeatedly use the Waze app over time. Developing a churn prediction model will help prevent churn, improve user retention, and grow Waze’s business. An accurate model can also help identify specific factors that contribute to churn and answer questions such as: 

* Who are the users most likely to churn?
* Why do users churn?
* When do users churn? 

For example, if Waze can identify a segment of users who are at high risk of churning, Waze can proactively engage these users with special offers to try and retain them. Otherwise, Waze may lose these users without knowing why. 

Your insights will help Waze leadership optimize the company’s retention strategy, enhance user experience, and make data-driven decisions about product development.

#### Project background

Waze’s data team is in the earliest stages of the churn project. The following tasks are needed before the team can begin the data analysis process:

* Build a dataframe for the churn dataset
* Examine data type of each column
* Gather descriptive statistics

#### Your assignment
You will build a dataframe for the churn data. After the dataframe is complete, you will organize the data for the process of exploratory data analysis, and update the team on your progress and insights.

#### Team members at Waze

**Data team roles**

* Harriet Hadzic - Director of Data Analysis
* May Santner - Data Analysis Manager
* Chidi Ga - Senior Data Analyst
* Sylvester Esperanza - Senior Project Manager 

Data team members have technical experience with data analysis and data science. However, you should always be sure to keep summaries and messages to these team members concise and to the point. 

**Cross-functional team members**
* Emrick Larson - Finance and Administration Department Head
* Ursula Sayo - Operations Manager

Your Waze team includes several managers overseeing operations. It is important to adapt your communication to their roles since their responsibilities are less technical.

*Note: The story, all names, characters, and incidents portrayed in this project are fictitious. No identification with actual persons (living or deceased) is intended or should be inferred. And, the data shared in this project has been created for pedagogical purposes.*

#### Specific project deliverables

* Complete the questions in the Course 2 PACE strategy document
* Answer the questions in the Jupyter notebook project file
* Complete coding prep work on project’s Jupyter notebook
* Summarize the column Dtypes
* Communicate important findings in the form of an executive summary

## PACE Strategy Document

**Project goal:**

Waze leadership has asked your data team to develop a machine learning model to predict user churn. Churn quantifies the number of users who have uninstalled the Waze app or stopped using the app. This project focuses on monthly user churn. An accurate model will help prevent churn, improve user retention, and grow Waze’s business.

[Waze project proposal](https://docs.google.com/document/d/13C4UKfe1pz7J7cJ676XgvSOfHNxpxfR1WS4h1mVQ_bg/edit?usp=sharing)
[PACE document](https://docs.google.com/document/d/1GZYAOKtrH-bYPePVMDWLViRaO5uQxDfr0YSpumFZME8/edit?usp=sharing)

**Tasks:**
* Plan
* Analyze
    * Import data
    * Create a dataframe
    * Inspect data
    * Identify outliers
    * Create a data visualization
    * Share an executive summary with the Waze data team
* Construct
* Execute

## Data Description

The dataset contains: 14,999 rows – each row represents one unique user, and 13 columns.

| Column name | Type | Description |
| ... | ... | ... |
| ID | int | A sequential numbered index |
| label | obj | Binary target variable (“retained” vs “churned”) for if a user has churned anytime during the course of the month |
| sessions | int | The number of occurrence of a user opening the app during the month |
| drives | int | An occurrence of driving at least 1 km during the month |
| device | obj | The type of device a user starts a session with |
| total_sessions | float | A model estimate of the total number of sessions since a user has onboarded |
| n_days_after_onboarding | int | The number of days since a user signed up for the app |
| total_navigations_fav1 | int | Total navigations since onboarding to the user’s favorite place 1 |
| total_navigations_fav2 | int | Total navigations since onboarding to the user’s favorite place 2 |
| driven_km_drives | float | Total kilometers driven during the month |
| duration_minutes_drives | float | Total duration driven in minutes during the month |
| activity_days | int | Number of days the user opens the app during the month |
| driving_days | int | Number of days the user drives (at least 1 km) during the month |

## Data Preparation

* Libraries were imported and data loaded.
* Ran `head()` and `info()` methods to inspect data shape, type, and missing values. The 'label' variable (whether or not a user has churned) is missing 700 entries, but all the other variables are complete.
    * The subgroup with missing labels does not appear to be discernibly different from the full dataset in terms of all numerical data and the distribution of iPhone vs. Android users, therefore, we may proceed exploration by omitting these entries.
* Summary statistics were run with `describe()`
    * The summary statistics also show that there are variables that are right-skewed, such as `driven_km_drives`. Therefore, it is better if we use median instead of mean to summarize data.
* To identify differences between churned and retained users, we tried a few things with `groupby()` and `agg()`
    * It is found that users who churned averaged ~3 more drives in the last month than retained users, but retained users used the app on over twice as many days as churned users in the same time period. The median churned user drove ~200 more kilometers and 2.5 more hours during the last month than the median retained user. In other words, churned users are more likely to be serious drivers who drive more often and for longer distance.
    * After we calculate the distance per drive, and drives per driving day, it became more apparent that churned users drive more on days when they drive at all. The median user who churned drove 698 kilometers each day they drove last month, which is almost ~240% the per-drive-day distance of retained users. The median churned user had a similarly disproporionate number of drives per drive day compared to retained users.
    * The ratio of iPhone users and Android users is consistent between the churned group and the retained group, and those ratios are both consistent with the ratio found in the overall dataset.
 
## Preliminary Findings

1. There are 700 entries where "label" (whether or not a user has churned) was missing. All the other variables are complete. Fortunately, there does not seem to be any pattern associated with the missing data. Summary statistics for this subgroup do not appear to be very different from the full dataset.
2. Using median instead of mean reduces the impact of outliers. In our case, total distance driven is a right-skewed variable. The mean is 4,404 km, whereas the median is 2,500 km.
3. Users who churned averaged ~3 more drives in the last month than retained users, and the median churned user drove ~200 more kilometers and 2.5 more hours during the last month than the median retained user. These seem like marginal difference, but considering distance per drive and drives per driving day, the churned users appear to have driven more often and for longer distance on a day when they drive at all. It is likely that they are someone who drives for a living, such as long-haul truck drivers.
4. About 63% are iPhone users and 36% are Android users. There does not appear to be an appreciable difference in churn rate between iPhone users and Android users, since the ratio remains the same when we grouped data by hurned and retained users. Device compatibility is unlikely to be a factor.
5. We've preliminarily established that a typical churned users may be someone who drives for a living. I would like to further investigate which features within Waze app is well liked, and which ones are not, and what may be the churned users' needs.
