# Telecom-Churn-Case-Study-Upgrad
## Problem Statement

## Business Problem Overview

In the telecom industry, customers are able to choose from multiple service providers and actively switch from one operator to another. In this highly competitive market, the telecommunications industry experiences an average of 15-25% annual churn rate. Given the fact that it costs 5-10 times more to acquire a new customer than to retain an existing one, customer retention has now become even more important than customer acquisition.

For many incumbent operators, retaining high profitable customers is the number one business goal.

To reduce customer churn, telecom companies need to predict which customers are at high risk of churn.

In this project, we will analyse customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn and identify the main indicators of churn.

## Understanding and Defining Churn

In the telecom sector, there are two primary payment models: prepaid (where users pay a set amount in advance and then use the services) and postpaid (where users pay a monthly or annual cost after using the services).

In the postpaid model, users typically notify the current operator to stop services when they wish to switch to a different provider, and we can immediately identify this as a case of churn.

It is difficult to determine whether a customer has churned or is just not using the services temporarily (for example, they may be traveling overseas for a month or two and then plan to resume using the services again). Additionally, under the prepaid model, customers who wish to switch to another network can simply stop using the services without any notice.

Because of this, predicting churn is typically more important (and difficult) for prepaid consumers, therefore the word "churn" needs to be used carefully.  Additionally, postpaid plans are more prevalent in Europe and North America, but prepaid plans are more frequent in India and Southeast Asia.

The Indian and Southeast Asian markets are the foundation of this endeavor.


## Definitions of Churn 

Churn can be defined in a number of ways, including:

**Revenue-based Churn:** Clients who, for a specified amount of time, have not used any revenue-generating services, like SMS, outbound calls, or mobile internet. Aggregate metrics like "customers who have generated less than INR 4 per month in total/average/median revenue" are another option.

The primary flaw in this definition is that some clients utilize the services but don't produce any income; they are merely recipients of calls or SMSs from their wage-earning colleagues. For instance, a lot of users in rural areas only get calls from their metropolitan siblings who earn a living.

**Usage-based churn:** Clients who have not used any services over a given period of time, including calls, internet, or other outbound communications.

This definition may have a drawback in that it might be too late to take corrective measures to keep the client after they have ceased utilizing the services for some time. For example, if we define churn as a "two-month zero usage" period, then it may be impossible to estimate turnover because the customer would have already moved to a different provider by then.

In this project, churn will be defined using the **usage-based** concept.

## High-value Churn

About 80% of revenue in the Indian and Southeast Asian markets originates from the top 20% of consumers, or so-called high-value clients. Therefore, we will be able to reduce large income leakage if we can lower the churn rate of high-value consumers.

In this project, we will identify high-value clients using a particular metric (explained below) and we will exclusively forecast churn for high-value clients.

## Understanding the Business Objective and the Data

Customer-level data for the months of June, July, August, and September is included in the dataset. The corresponding months' codes are 6, 7, 8, and 9. 

Using the data (features) from the first three months, the business goal is to forecast the churn in the last (i.e., ninth) month. It will be useful to comprehend the normal consumer behavior during churn in order to perform this activity effectively.

## Understanding Customer Behaviour During Churn

Consumers typically decide to move to a rival over time rather than all at once (this is especially true for high-value clients). We make the following assumptions about the customer lifecycle phases when predicting churn:
1. **The positive phase": During this stage, the client is satisfied with the service and acts normally.

2. **The stage of "action":** During this phase, the customer experience begins to suffer; for example, he or she receives an alluring offer from a rival, is subjected to unfair charges, is dissatisfied with the quality of the service, etc. The client typically behaves differently during this time than during the "good" months. Additionally, since remedial measures (such matching the competitor's price or enhancing the quality of the service, among other things) can be implemented at this time, it is critical to identify high-churn-risk clients during this period.
   
3. **The period of "churn":** The consumer is considered to have churned at this time. On the basis of this stage, we define churn. It's also crucial to remember that we were unable to forecast this data at the time of the prediction (i.e., the action months). We therefore discard all of the data associated with this phase after classifying churn as 1/0 based on this phase.

Since we are working over a four-month period in this instance, the first two months are considered the "good" phase, the third month is considered the "action" phase, and the fourth month is considered the "churn" phase.

## Data Preparation

The following data preparation steps are crucial for this problem:

1. **Derive new features**
This is among the most crucial aspects of data preparation since high-quality features frequently set good models apart from subpar ones. Using our knowledge of business, we will identify characteristics that we believe may be significant churn indicators.

2. **Filter high-value customers**
As previously said, we only need to forecast attrition for high-value clients. High-value clients should be defined as follows: Individuals who have refilled with a quantity greater than or equal to X, where X represents the 70th percentile of the mean amount refilled over the first two months (the favorable phase).

3. **Tag churners and remove attributes of the churn phase**
Next, categorize the customers who have churned (if churn=1, otherwise 0) according to the fourth month. Individuals who have not placed or received any calls during the churn phase, as well as those who have never used mobile internet. To identify churners, we must use the following attributes:

- total_ic_mou_9
- total_og_mou_9
- vol_2g_mb_9
- vol_3g_mb_9

After tagging churners, we need to remove all the attributes corresponding to the churn phase (all attributes having ‘ _9’, etc. in their names).

## Modelling

Create models to forecast attrition. There will be two uses for the prediction model we develop:

1. It will be utilized to forecast the likelihood of a high-value customer leaving in the near future (i.e., the churn phase). Knowing this allows the business to take appropriate action, like offering exclusive programs or low-cost recharges.

2. It will be applied to determine significant variables that have high churn prediction power. These factors might also reveal the reasons behind users' decisions to move to different networks.

In certain instances, a single machine learning model can accomplish both of the aforementioned objectives. However, because there are a lot of features in this case, we should consider dimensionality reduction techniques like PCA before developing a predictive model. We can apply any classification model after PCA.

Additionally, we will attempt utilizing strategies to address class imbalance because the rate of churn is normally low (around 5–10%; this is known as class-imbalance). 

To construct the model, we might consider the following suggested actions:
1. Preprocess the data (manage missing values, format columns appropriately, etc.).
2. Use relevant exploratory analysis to glean insights that can be applied to future modeling or feature engineering projects, or directly to business needs.
3. Create fresh characteristics.
4. Use PCA to lower the number of variables.
5. Utilizing appropriate methodologies, train a range of models and adjust model hyperparameters (manage class imbalance).
6. Apply the proper evaluation metrics to the models' assessment. Keep in mind that accurately identifying churners is more crucial than precisely identifying non-churners; use an evaluation tool that aligns with this business objective.
7. Lastly, select a model using a metric for evaluation.

Only one of the two objectives can be met by the aforementioned model: it can only identify which consumers are likely to leave. The aforementioned approach is insufficient for identifying the critical churn traits. This is because PCA typically yields components that are difficult to understand.

As a result, the primary goal of the second model we develop will be to pinpoint significant predictor features that aid in the understanding of churn indicators by the company. A tree family model or a logistic regression model are acceptable options for determining significant variables. We shall take steps to address multi-collinearity in the event of logistic regression.

Once significant predictors have been identified, visually represent them using plots, summary tables, or other techniques that best illustrate the significance of the features, in our opinion.

Lastly, based on our observations, suggest customer churn management tactics.
