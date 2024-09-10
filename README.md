# newyork-taxi-analysis
This is my first data project on GitHub which I got help from a tutorial.

**Data Source: [New York City Govement Website](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
Easy Access to [Taxi Data CSV](https://drive.google.com/file/d/1hOVPegNwSAlPs87M0jIx2vWI1l_Fgvoa/view?usp=sharing)

## Problem Definition
This project aims to predict the average money spent on taxi rides for each region of New York per given day and hour. This problem is a supervised regression problem. 

## Data Problems I Fixed

![indir (1)](https://github.com/user-attachments/assets/79abe373-bcea-48cb-a7d3-321c621cb139)

**Negative total_amount values:** removed them because negative pays are not logically possible showing a fault
**Zero total_amount values: ** removed them because they also mislead project
** Too high total_amount values: ** some values were too high to be true. The average total_amount was circa $15. 
That's why, I filtered out total_amount higher than $200. There were 1166 data points having higher than $200 as total_amount. It was okay to remove because it did not much space considering a dataset of 7696617 points.

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

Here are the performance results before tuning.

           Algorithm    MAE    RMSE     R2
0    Benchmark model  9.778  14.739  0.225
1      Decision tree  8.534  14.011  0.308
2      Random forest  7.426  13.212  0.385
3  Gradient boosting  8.388  13.378  0.369


The randomm forest is selected to be tuned. Here are the best parameter values.
n_estimators=500
min_samples_split= 2
min_samples_leaf= 2
max_features= 'sqrt'
max_depth= 10
bootstrap= True


The Performance compared to previous models
Algorithm	MAE	RMSE	R2
Benchmark model	9.778	14.739	0.225
Decision tree	8.534	14.011	0.308
Random forest	7.426	13.212	0.385
Gradient boosting	8.388	13.378	0.369
Tuned Random Forest	9.877	14.423	0.281

Here is True vs Predicted value plot for the tuned random forest model. X axis is the true value and y axis is the predicted value. 


