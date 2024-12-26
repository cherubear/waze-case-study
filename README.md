# Waze Case Study
A capstone project for Google Advanced Data Analytics Certificate program

![Waze logo](https://github.com/user-attachments/assets/3b8be2fa-6df1-4a17-b1d5-4f1281066f46)


## Executive Summary

**Preliminary Data Summary:**

![Preliminary - Executive summary](https://github.com/user-attachments/assets/a64b0898-49c0-4f20-a5a8-aea36d851636)

**Exploratory Data Analysis:**

![Waze Project EDA_ Executive summary](https://github.com/user-attachments/assets/578b0d06-50c3-4e80-a568-fd93317006bb)

**Hypothesis Testing:**

![Waze project_ hypothesis testing executive summaries](https://github.com/user-attachments/assets/ccc6f38f-24eb-451e-a661-2cbb694f664e)

**Regression Analysis:**

![Waze Project_ Logistic Regression Model Executive summaries](https://github.com/user-attachments/assets/dae32208-0035-469c-b07b-cfc7caca849b)


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

## Preliminary Data Summary

### Project goal

Waze leadership has asked your data team to develop a machine learning model to predict user churn. Churn quantifies the number of users who have uninstalled the Waze app or stopped using the app. This project focuses on monthly user churn. An accurate model will help prevent churn, improve user retention, and grow Waze’s business.

[Waze project proposal](https://docs.google.com/document/d/13C4UKfe1pz7J7cJ676XgvSOfHNxpxfR1WS4h1mVQ_bg/edit?usp=sharing)

[PACE document](https://docs.google.com/document/d/1GZYAOKtrH-bYPePVMDWLViRaO5uQxDfr0YSpumFZME8/edit?usp=sharing)

### Tasks
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

### Data description

The dataset contains: 14,999 rows – each row represents one unique user, and 13 columns.

| Column name             | Type  | Description                                                                                                        |
|-------------------------|-------|--------------------------------------------------------------------------------------------------------------------|
| label                   | obj   | Binary target variable (“retained” vs “churned”) for if a user has churned anytime during the course of the month  |
| sessions                | int   | The number of occurrence of a user opening the app during the month                                                |
| drives                  | int   | An occurrence of driving at least 1 km during the month                                                            |
| device                  | obj   | The type of device a user starts a session with                                                                    |
| total_sessions          | float | A model estimate of the total number of sessions since a user has onboarded                                        |
| n_days_after_onboarding | int   | The number of days since a user signed up for the app                                                              |
| total_navigations_fav1  | int   | Total navigations since onboarding to the user’s favorite place 1                                                  |
| total_navigations_fav2  | int   | Total navigations since onboarding to the user’s favorite place 2                                                  |
| driven_km_drives        | float | Total kilometers driven during the month                                                                           |
| duration_minutes_drives | float | Total duration driven in minutes during the month                                                                  |
| activity_days           | int   | Number of days the user opens the app during the month                                                             |
| driving_days            | int   | Number of days the user drives (at least 1 km) during the month                                                    |


### Data preparation

* Libraries were imported and data loaded.
* Ran `head()` and `info()` methods to inspect data shape, type, and missing values. The 'label' variable (whether or not a user has churned) is missing 700 entries, but all the other variables are complete.
    * The subgroup with missing labels does not appear to be discernibly different from the full dataset in terms of all numerical data and the distribution of iPhone vs. Android users, therefore, we may proceed exploration by omitting these entries.
* Summary statistics were run with `describe()`
    * The summary statistics also show that there are variables that are right-skewed, such as `driven_km_drives`. Therefore, it is better if we use median instead of mean to summarize data.
* To identify differences between churned and retained users, we tried a few things with `groupby()` and `agg()`
    * It is found that users who churned averaged ~3 more drives in the last month than retained users, but retained users used the app on over twice as many days as churned users in the same time period. The median churned user drove ~200 more kilometers and 2.5 more hours during the last month than the median retained user. In other words, churned users are more likely to be serious drivers who drive more often and for longer distance.
    * After we calculate the distance per drive, and drives per driving day, it became more apparent that churned users drive more on days when they drive at all. The median user who churned drove 698 kilometers each day they drove last month, which is almost ~240% the per-drive-day distance of retained users. The median churned user had a similarly disproporionate number of drives per drive day compared to retained users.
    * The ratio of iPhone users and Android users is consistent between the churned group and the retained group, and those ratios are both consistent with the ratio found in the overall dataset.
 
### Preliminary findings

1. There are 700 entries where "label" (whether or not a user has churned) was missing. All the other variables are complete. Fortunately, there does not seem to be any pattern associated with the missing data. Summary statistics for this subgroup do not appear to be very different from the full dataset.
2. Using median instead of mean reduces the impact of outliers. In our case, total distance driven is a right-skewed variable. The mean is 4,404 km, whereas the median is 2,500 km.
3. Users who churned averaged ~3 more drives in the last month than retained users, and the median churned user drove ~200 more kilometers and 2.5 more hours during the last month than the median retained user. These seem like marginal difference, but considering distance per drive and drives per driving day, the churned users appear to have driven more often and for longer distance on a day when they drive at all. It is likely that they are someone who drives for a living, such as long-haul truck drivers.
4. About 63% are iPhone users and 36% are Android users. There does not appear to be an appreciable difference in churn rate between iPhone users and Android users, since the ratio remains the same when we grouped data by hurned and retained users. Device compatibility is unlikely to be a factor.
5. We've preliminarily established that a typical churned users may be someone who drives for a living. I would like to further investigate which features within Waze app is well liked, and which ones are not, and what may be the churned users' needs.

## Exploratory Data Analysis

### Project goal
The Waze data team is currently developing a data analytics project aimed at increasing overall growth by preventing monthly user churn on the Waze app. Thorough exploratory data analysis (EDA) enables Waze to make better decisions about how to proactively target users likely to churn, thereby improving retention and overall customer satisfaction.

[PACE document](https://docs.google.com/document/d/15Q9XGQK4GPk5dQZD3hKgbwbNHB9nsVeLxDSF6OrqFA0/edit?usp=sharing)

### Tasks

* Perform Exploratory Data Analysis (EDA)
* Create data visualizations
    * Create a scatterplot to enhance the visualization created with Python
* Provide a summary of the results of your exploratory data analysis (EDA)

### Summary of EDA and recommendations

* There is 700 of missing values in the user churn label, so we might need further clarification why that may be the case from Waze. Fortunately, we found that the missing values do not seem to be associated with device type.
    * **Recommendation**: Understanding the root case of missing values is a critical step. Imagine that all those missing values are in fact churned user, that could change how our data look quite a bit.
* There are many outliers for drives, sessions, distance, and duration, and some of which seems physically impossible. During data cleaning, I imputed outliers with 95% percentile. It is worth investigating with Waze how the outliers emerged, as there could be a software bug with double counting trips, or failing to stop a trip.
    * **Recommendation**: Understanding the outliers may help Waze identify and fix bugs, but is less urgent for our data exploration than the missing values, because the outliers have been addressed, and is less likely to impact our data greatly.
* The number of drives and the number of sessions are both strongly correlated, so they might provide redundant information when we incorporate both in a model.
    * **Recommendation**: When building a model, choose one from sessions and drives, and/or one from activity days and driving days, because they are highly correlated.
* Excluding the users who did not drive at all, the churned users drove less frequent, but drive longer distance when they do.
    * **Recommendation**: Find out more demographic information, especially of the churned users. Do they share a common profile and/or driving habit? What are they looking for in a navigation app, and what do they like and not like about Waze?
* Users appear to be very active in the observed month. The sessions on average accounts for 40% of all app usage since onboarding, even for longtime users who signed up years ago.
    * **Recommendation**: If there had been updates or campaigns last month, they might be effective with boosting app usage, and we may want to explore if they are repeatable and sustainable.

## Hypothesis Testing

### Project goal

The main purpose of this project is to understand if there is meaningful difference in the amount of rides between iPhone users and Android users. With this information, business leaders at Waze can think about strategies to address these differences, such as improving user experience on a specific device.

[PACE document](https://docs.google.com/document/d/1NE-K6zajeFlRFsPUhtKg95We2dlWahkeiAU1S3OvXqc/edit?usp=sharing)

### Tasks

* Explore the project data
* Implement a hypothesis test
* Communicate insights with stakeholders within Waze

### Summary of hypothesis testing

The descriptive statistics show that on average, iPhone users do ~1.5 more drives than Android users over the observed month, but we don’t know if this is due to sampling variability. We completed a two-sample t-test with the following hypothesis:
* Null hypothesis: There is no difference between the average number of drives of iPhone users and Android users.
* Alternative: There is difference between the average number of drives of iPhone users and Android users.

The result is that we fail to reject the null. Since we do not see significant difference in user behavior between iPhone and Android users, at this stage we do not recommend making changes specific to a device type. We recommend looking into other factors that may impact user churn.

## Regression model

### Project goal

The goal of this project to build a statistical model that will help predict if a user will churn or not given the usages information collected in the Waze app.

### Tasks

* Determine the correct modeling approach
* Build a regression model
* Finish checking model assumptions
* Evaluate the model
* Interpret model results and summarize findings for cross-departmental stakeholders within Waze

### Summary of model construction

As we are trying to predict if a user will churn given a series of independent variables, we will build a binomial logistic regression model. We started with looking at multicollinearity between all independent variables, and discovered that sessions and drives are strongly correlated, and driving_days and activity_days are strongly correlated. Therefore, the first model we built is to drop sessions and activity_days, and try all the other variables as independent variables in our model. Below are our findings:

1. driving_days is the variable that has most influenced the model's prediction. It has a negative correlation with user churn, which is not surprising. The more a user uses the app, the less likely they will churn.
2. In the EDA, we found that km_per_driving_day may be positively correlated to churn, but in our regression model, the relationship was negligible.
3. In multivariate model, variables may interact with each other in unexpected ways. Therefore we may see results that we did not expect.
4. When evaluating the model, we find that precision score is mediocre and recall score is extremely low. It does not appear to be an effective model. I would not recommend using this model as is. There are many variables with weak predicting power. I would recommend removing variables that are not useful.
5. I would start with removing variables that are not useful. In the meantime, as we recommended a few times in previous phases of this project, more information needs to be collected about user demographics and drive-level information. Our findings in this model construction phase substantiated this view because our model does not perform very well.
6. It would be helpful to have demographics information, or more details about how users use the app. For example, if there are multiple features in the app, which ones are used during drives.

## Machine learning models

### Project goal

We want to build and test different machine learning models to predict user churn. Our work will help Waze leadership make informed business decisions to prevent user churn, improve user retention, and grow Waze’s business. 

### Tasks

Previously, I built a binomial logistic regression model. However, the predicting power is quite weak. The final step is to build and test different machine learning models for predicting user churn. The step is consist of the following sub-tasks.

* Perform feature engineering
* Build the following machine learning models: random forest and XGBoost
* Evaluate the models
* Share an executive summary with the Waze leadership team

### Model construction

To use existing data to determine whether or not a user will churn (binary outcome), we will start building and testing the following machine learning models: random forest classifier and XGBoost.

#### Considerations before model construction

We are building and testing machine learning models that will help predict user churn with existing data.

First, we must value users privacy. To do so, we ensure no personal identification information can be backed out from our model. Given what I know about the dataset, the risk of privacy infringement in this project is low. Second, We should be wary of any bias that could result from the model, which may also lead to biased treatment to Waze users if any subsequent business decisions were made based on model findings. We are aware the model will not be error-free - a false negative means failing to identify a churning user, denying Waze the opportunity to make an effort to retain the user; while a false positive means unnecessary cost for Waze to retain a user who was not going to churn anyway.

Since Waze is invested in this project to reduce user churn and grow their user base, therefore the benefits of such a model outweigh the potential problems if the model has a reasonably good predicting power. We will aim to build a model that has good recall score, that is, try not to miss users who will likely churn.

**Step-by-step**:
* Import packages and load data
* Feature engineering
   * Calculate the distance traveled per driving day
   * Calculate the amount of sessions each user had during the last month, as a percentage of total sessions since onboarding
   * Create a binary label of professional driver, which is defined as someone who had 60 or more drives and drove on 15+ days in the last month
   * Calculate sessions per day since onboarding
   * Calculate average driving speed of each driver, km per hour
   * Calculate average driving distance per drive, km per drive
   * Calculate the percent of navigations of favorite destinations, as a percentage of total sessions
         * Note: this is a proxy since sessions and drives may not have the same scale. The result is not a true percentage in the range [0, 1].
   * Encode categorical values "device" and "label" as numeric (in this case, both are binary)
* Model construction
   * Split the data into train/validation/test sets (60/20/20)
   * Train a Random Forest Classifier with cross validation within the train dataset, and iterate across these hyperparameters to find an estimator with best recall score:
     * max_features: any or all 18 variables
     * min_sample_split: 2 or 3
     * max_depth: no restriction
     * n_estimators: 100, 200 or 300
     * **Findings:** We got a Random Forest Classifier with recall score of 0.13. It is an improvement from the logistic regression model, but still far from ideal.
   * Train a XGBoost model with cross validation within the train dataset, and iterate across these hyperparameters to find an estimator with best recall score:
     * max_depth: 5, 10
     * min_child_weight: 3 or 5
     * learning_rate: 0.01 or 0.1
     * n_estimators: 300
     * **Findings:**

### Conclusion

1. The Random Forest improved recall of churned user to 12% (compared to 9% with a logistic regression model).
2. The XGBoost model improved recall to 17%, another big improvement from the Random Forest Classifier.
3. Still, a recall rate of 10-12% is far less than ideal. Although not necessarily a model fit for deployment in predicting user churn and inform business decisions, it provides some directional recommendations regarding how we may want to further explore.
4. The engineering features ranked high in importance, such as km per hour, percent of sessions last month. This is very different from the logistic regression model, in which driving_days was the one dominating feature.
5. **Recommendations:**
    * Communicate with Waze to obtain business insights if certain features are intuitive, for example, something is working so that app usage increased last month, and our model shows that this is also associated with lower likelihood of user churn. Looks like an effective business strategy already. Why this happened, and can it be sustainable?
    * Explore drive-level details in order to refine our model, for example, does user use any of the social features in app, like reporting a road condition?
