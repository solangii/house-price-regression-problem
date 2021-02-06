# House Price of King County Regions

```
Course project of MGE303 DataMining, UNIST
```

**Implement**  : [link](https://github.com/solangii/house-price-regression-problem/blob/master/main.ipynb)

**report** : [link](https://github.com/solangii/house-price-regression-problem/tree/master/report)

I will exploring **the House Price of Kimg County Regions** by term project of MGE303 DataMining class(2020, spring). Actually, This is a problem of **regression**. We **want to know the house price in the King County area**. So, **Our goal is to more accurately predict house price for a house that meets the conditions i want by using the given data**(Problem Definition).

---

## 1. Data Munging

1. Data Load
2. Data Handle
3. Encoding
4. Histogram



## 2. EDA (Hypothesis Construction)

1. The relationship between PRICE and AREA

   **Hypothesis 1**:The relationship between `PRICE` and area variables is likely to have a major impact on variables `AR_LIV`, `AR_RFTP` and `AVG_LIV_NEAR`.

2. The relationship between PRICE and the number of room and floor(internal facilities)

   **Hypothesis 2** : Looking at each case, the **higher `NUM_BD` and `BTH_STAT_2`, the higher the tendency for `PRICE`**. However, it does not seem to have much to do with `NUM_FLR`.

3. The relationship between Price and Climate change

   **Hypothesis 3**: `Price`, `PRECIPITATION`, `Summer_HIGH`, and `Winter_Low` are not related.

4. The relationship between Price and Near_RIV

   **Hypothesis 4**: If there is water near the house, the price is high. Therefore, **`NEAR_RIV` affects `PRICE`**.

5. The relationship between Price and Crime

   **Hypothesis 5**: `Price`, `violent_crime`, and `Property_crime` are not related.

6. The relationship between Price and house position(latitude, longitude)

   **Hypothesis 6**: `Price`, `Longitude`, and `Latitude` are not related.

7. The relationship between price and Appearance and Facilities

   **Hypothesis 7**: As I said earlier, **the `outlook` and `price` seem to be related**, and the `condition` was so focused on a particular value that it was difficult to find the relationship.  Also, the price change depending on 'is_renovated' is not significant at less than 500,000. **Therefore, `price` and `IS_RENOVATED` seem irrelevant.** And there seems to be **no change in `PRICE` according to `YR_PAST`**.

 **Conclustion of Hypothesis** : 

- **have relationship** with `PRICE` : `AR_LIV`, `AR_RFTP`,`AVG_AR_LIV_NEAR`,`NUM_BD`,`BTH_STAT_2`,`NEAR_RIV`,`OUTLOOK`

- don't have relationship with `PRICE` : `AR_PL`, `AR_BASE`, `AVG_AR_PL_NEAR`, `NUM_FLR`, `PRECEPITATION`, `SUMMER_HIGH`, `WINTER_LOW`,`VIOLENT_CRIME`,`PROPERTY_CRIME`, `LAT`, `LONG`, `CONDITION`, `IS_RENOVATED`, `YR_PAST`

Construct correlation matrix



## 3. Modeling & Evaluate

- Multiple Linear Regression

  ```python
  mlr = LinearRegression()
  mlr.fit(X_train,y_train)
  mlr_score = mlr.score(X_test,y_test)
  pred_mlr = mlr.predict(X_test)
  expl_mlr = explained_variance_score(pred_mlr,y_test)
  mse_mlr = mean_squared_error(pred_mlr,y_test)
  rmse_mlr = np.sqrt(mse_mlr)
  cv_mlr = cross_val_score(mlr,X_train,y_train, cv=10).mean()
  ```

- Decision Tree

  ```python
  tr_regressor = DecisionTreeRegressor(random_state=0)
  tr_regressor.fit(X_train,y_train)
  tr_regressor.score(X_test,y_test)
  pred_tr = tr_regressor.predict(X_test)
  decision_score=tr_regressor.score(X_test,y_test)
  expl_tr = explained_variance_score(pred_tr,y_test)
  mse_tr = mean_squared_error(pred_tr,y_test)
  rmse_tr = np.sqrt(mse_tr)
  cv_tr = cross_val_score(tr_regressor,X_train,y_train, cv=10).mean()
  ```

- Random Forest Regression Model

  ```python
  rf_regressor = RandomForestRegressor(n_estimators=28,random_state=0)
  rf_regressor.fit(X_train,y_train)
  rf_regressor.score(X_test,y_test)
  rf_pred =rf_regressor.predict(X_test)
  rf_score=rf_regressor.score(X_test,y_test)
  expl_rf = explained_variance_score(rf_pred,y_test)
  mse_rf = mean_squared_error(rf_pred,y_test)
  rmse_rf = np.sqrt(mse_rf)
  cv_rf = cross_val_score(rf_regressor,X_train,y_train, cv=10).mean()
  ```

  

**Calculate Score**

```python
print("Multiple Linear Regression Model Score is ",round(mlr.score(X_test,y_test)*100))
print("Decision tree  Regression Model Score is ",round(tr_regressor.score(X_test,y_test)*100))
print("Random Forest Regression Model Score is ",round(rf_regressor.score(X_test,y_test)*100))
>> Multiple Linear Regression Model Score is  70.0
>> Decision tree  Regression Model Score is  76.0
>> Random Forest Regression Model Score is  88.0
```



## 4. Conclusion

```python
models_score =pd.DataFrame({'Model':['Multiple Linear Regression','Decision Tree','Random forest Regression'],
                            'Score':[mlr_score,decision_score,rf_score],
                            'Explained Variance Score':[expl_mlr,expl_tr,expl_rf],
                            'RMSE':[rmse_mlr,rmse_tr,rmse_rf],
                            '10-CV':[cv_mlr,cv_tr,cv_rf]
                           })
models_score.sort_values(by='10-CV',ascending=False)
```

Of the three models, RMSE values are the smallest, and 10-CV and Score think the largest random forest is the most suitable model.

---

