# MGE303 DataMining Term Project 

**Topic : House Price of King County Regions**

Name : 김소랑(Kim Solang)

Student ID : 20181041

Contact : solangii@unist.ac.kr

---



## Problem Definition

Hello, I am Solang Kim. I will exploring **the House Price of Kimg County Regions** by term project of MGE303 Data Mining class. Actually, This is a problem of **regression**. We **want to know the house price in the King County area**. So, Our goal is **to more accurately predict house price for a house that meets the conditions i want by using the given data**.



## Hypothesis Construction (by EDA)

1. The relationship between **Price** and **Area**

![img1](./img/img1.png)

Compared to the `AR_PL`, `AR_BASE`, and `AR_AR_PL_NEAR` variables discussed earlier, there seems to be **no linear relationship** with PRICE. Although `AR_BASE`shows a little linear relationship, certain values show an **outlier** that does not change the price even if the base area increases.

The relationship between `PRICE` and area variables is likely to have a major impact on variables `AR_LIV`, `AR_RFTP` and `AVG_LIV_NEAR`.



2. The relationship between **PRICE** and **the number of room and floor(internal facilities)**

The boxplot was drawn to find out the relationship between **PRICE**, the number of **bedrooms**, and the number of **bathrooms** (not the exact number, but the larger the number, the categorical variables), and the number of **floors**.

Looking at each case, the **higher** `NUM_BD` **and** `BTH_STAT_2`**, the higher the tendency for** `PRICE`. However, it does not seem to have much to do with `NUM_FLR`.



3. The relationship between Price and Climate change

Looking at the graph above, despite the increase in each variable, price does not show a constant change. Therefore Price, PRECIPITATION, Summer_HIGH, and Winter_Low are not related.



4. The relationship between Price and Near_RIV

5. The relationship between Price and Crime

6. The relationship between Price and house position(latitude, longitude)

 If there is water near the house, the price is high. Therefore, **NEAR_RIV affects PRICE**. 

Price, violent_crime, and Property_crime are not related.

Price, Longitude, and Latitude are not related.



7.  The relationship between price and Appearance and Facilities

   Results show that the distribution of condition had too many values at 3 to determine the exact relationship between outlook and condition. Therefore, the distribution is too biased to identify a particular relationship, so `CONDITION` would be better not to consider it.

   As I said earlier, **the outlook and price seem to be related**, and the condition was so focused on a particular value that it was difficult to find the relationship. 

   Also, the price change depending on 'is_renovated' is not significant at less than 500,000. 

   **Therefore, price and IS_RENOVATED seem irrelevant.** And there seems to be **no change in PRICE according to YR_PAST**.



And if you look at this Pearson correlation matrix, you can see that the relationships that we thought of earlier are roughly right. For example, in the following graph, there is a correlation between AV_LIV, AR_RFTP, and AVG_AR_LIV_NEAR, and as NUM_BED increases, the number of BATHROOMs increases somewhat.



## Data Munging and Data Preprocessing

There was no missing value in our data. And encoding for BTH_STAT feature was done.

The type of BTH_STAT is categorical and BTH_STAT means number of bathrooms. Also, It has 4 category that <2, 2=<ROOMS<=4, 4<ROOMS<=6, and >6. I converted the values corresponding to each category into 1,2,3,4 using map.



## Modeling & Evaluation

I used Multiple Linear Regression, Decision Tree, and Random Forest like this.

Of the three models, The Random Forest’s RMSE values are the smallest, and Score value is the largest. So random forest is the most suitable model. 



## Post-Analysis

We already know that random forests have emerged to address the main drawback of decision trees, the tendency to overfit. Therefore, we know that random forests are better models than decision trees.
 In addition, linear regression would have been overqualified due to the correlation between independent variables. Therefore, I think the best of the three models is random forest because they would have solved the most overfitting problem.

 

The conversion pipeline was not performed. I made so many mistakes and errors that I deleted from my code and going analysis as simple. The results came out pretty well. But I think it is wrong. This is because essential conversion pipelines were not performed in feature engineering, and the ranges for each variable would have been weighted at a specific value, and the correlation by variable was not considered either. Perhaps a lot of problems have occurred.