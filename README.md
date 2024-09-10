# newyork-taxi-analysis
This is my first data project on GitHub which I got help from a tutorial.

**Data Source:** [New York City Govement Website](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
Easy Access to [Taxi Data CSV](https://drive.google.com/file/d/1hOVPegNwSAlPs87M0jIx2vWI1l_Fgvoa/view?usp=sharing)

## Problem Definition
This project aims to predict the average money spent on taxi rides for each region of New York per given day and hour. This problem is a supervised regression problem. 

## Data Problems I Fixed

![indir (1)](https://github.com/user-attachments/assets/79abe373-bcea-48cb-a7d3-321c621cb139)

During data preprocessing, the following cleaning steps were performed to ensure data quality:

- **Negative `total_amount` Values**: Removed these entries as negative values are not logically possible and indicate potential errors in the data.
  
- **Zero `total_amount` Values**: Removed these entries because zero values were misleading and did not contribute to the project objectives.

- **Excessively High `total_amount` Values**: Filtered out values higher than $200. Given that the average `total_amount` was approximately $15, values exceeding $200 were deemed unrealistic. A total of 1,166 data points with `total_amount` above $200 were removed. This removal was deemed acceptable due to the relatively small proportion of these data points in a dataset of 7,696,617 points.

## Original Features
List of features that can be used for model development that came with the original data. 
PULocationID, transaction_date, transaction_month, transaction_day, transaction_hour, trip_distance,
total_amount, count_of_transactions

## Feature Engineering
I have added 3 sets of new features to the model. First set is time based feature which are holiday and boolean.

Second is location based information. We have location IDs per region but there is a higher level abstraction for regions called Boroughs. This information came from [taxi_zone_lookup](taxi_zone_lookup.csv)

After feature engineering, the new feature list has become like:
PULocationID, transaction_month, transaction_day, transaction_hour, transaction_week_day, weekend, is_holiday, Borough, total_amount

## The Algorithms 
I tried Decision Tree, Random Forest and Gradient Boosting. The benchmark model is a decision tree. In the benchmark model, I only included the original features. On the normal models, I used original features plus newly created ones.

Here are the performance metrics for various algorithms before any tuning was applied:

| Algorithm           | MAE   | RMSE  | R2    |
|---------------------|-------|-------|-------|
| Benchmark Model     | 9.778 | 14.739| 0.225 |
| Decision Tree       | 8.534 | 14.011| 0.308 |
| Random Forest       | 7.426 | 13.212| 0.385 |
| Gradient Boosting   | 8.388 | 13.378| 0.369 |


The Random Forest model has been tuned to achieve better performance. Here are the best parameter values found:

- **n_estimators**: 500
- **min_samples_split**: 2
- **min_samples_leaf**: 2
- **max_features**: 'sqrt'
- **max_depth**: 10
- **bootstrap**: True


Below is a comparison of different algorithms based on key performance metrics:

| Algorithm           | MAE  | RMSE | R2    |
|---------------------|------|------|-------|
| Benchmark Model     | 9.778| 14.739 | 0.225 |
| Decision Tree       | 8.534| 14.011 | 0.308 |
| Random Forest       | 7.426| 13.212 | 0.385 |
| Gradient Boosting   | 8.388| 13.378 | 0.369 |
| Tuned Random Forest | 9.877| 14.423 | 0.281 |

Here is True vs Predicted value plot for the tuned random forest model. X axis is the true value and y axis is the predicted value. 


