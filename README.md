# Chicago Car Crashes 

**By Yamuna Umapathy & Lotus Baumgarner**

## Business Problem:

This project is about finding the primary contributory causes of car accidents in the most busiest city Chicago for our Stakeholder Insurance Carrier. Sources say Weather conditions, Heavy Traffic in Peak Hours, Vehicle Condition, Other driver's improper driving behaviours, Late night drivings, Texting while driving are some of the factors which causes car crashes. Insurance Carriers implementing Good Driving behaviours through their Telematic programs by offering discounts for Consumer's Auto insurance rates, also an alternate technique to reduce Carrier's Loss ratio by reducing car crashes.

National Highway Traffic Safety Administration source says Drivers are 94% responsible for car crashes.
source: https://crashstats.nhtsa.dot.gov
<p align="center">
  <img src = "https://github.com/YamunaU75/CarCrash_Phase4/blob/main/Data/NH%20table.png  " width="400" height="250"
</p>

## Dataset:

The dataset comes from Chicago Data Portal https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data 
This dataset contains 810K rows and 48 columns excluding consumer's personally identifiable information.

## Data Exploration, Data Cleaning & Feature Engineering:

This dataset contains more categorical columns, and values are more than 8-20 values, this has to be reduced before preprocessing. Or we end up
with more columns after Ordinal or One Hot encoding. Combining liked values within certain columns `TRAFFIC_CONTROL_DEVICE`, `WEATHER_CONDITION` & `FIRST_CRASH_TYPE` and `CRASH_HOUR`. Choosing our TARGET column as `MOST_SEVERE_INJURY` which has 5 categorical values, this will be changed to 3 options: NO_INJURY, NON_INCAP_INJURY and INCAP_INJURY. 

After completing our EDA, visualizing each feature with our Target variable, following columns was dropped. Columns which have 90+% missingness, columns 
not correlated with our Target variable, columns which have repetitive info as others, columns which have similar info as our Target will be dropped. Finally we came up with 16 necessary columns to find our right model.


## Down Sampling Dataset:

Target value has class imbalance, we downsampled our dataset to balance Target classes. Separated datasets was created for each target class, and by setting length of minority class as sample size, and using sample() method to randomize the pulled rows. Finally, we concatenated back into a single balanced dataset 
to find the right model. Balanced dataset contains 44K rows and 16 columns.


## Models Used:

Using Train Test split, and preprocessing using Pipeline and column transformer,

1. Model 1: We ran our baseline model with logistic regression. Accuracy score was 69 for our balanced dataset.


2. Model 2: Random Forest Classifier with tuned hyper parameters, we got accuracy score of 68.


3. Model 3: XGBoost Classifier, received accuracy score of 69, which was similar to our Baseline, and concluded as our final model results.
   Below are XGBoost Classification report and confusion matrix.https://github.com/YamunaU75/CarCrash_Phase4/blob/main/Data/confusion_matrix.png
  <p align="center">
  <img src = "https://github.com/YamunaU75/CarCrash_Phase4/blob/main/Data/XGB_CR.png  " width="400" height="250"
</p>

<p align="center">
  <img src = "https://github.com/YamunaU75/CarCrash_Phase4/blob/main/Data/confusion_matrix.png  " width="400" height="250"
</p>


4. Model 4: We tried our tensorflow model with 2 Hidden layers, activation function as softmax for multi classification target, optimizer Adam, loss as sparse_categorical_crossentropy, metrics accuracy, epochs 30, added regularization and validation size 0.2. We came up with similar accuracy score 68, validation accuracy was doing better than training accuracy score.


## Conclusion:

Downsampled the dataset to have balanced target class for 'No_Injury', 'Non_Incap_Injury' and 'Incap_Injury'. We ran Baseline model with Logistic Regression and got accuracy score of 69. Second model with Random Forest Classifier with tuned hyper parameters resulted in lower accuracy score 68. We tried our final model XGBoost and got same score 69.

Feature Importance graph for XGBoost shows major causes of incidents are RearEnd, Pedestrian/bicyclist, Hitting parked vehicle, Headon, Angle collision & hitting fixed object. Incidents caused by driver's negligence & their physical condition. Regarding lighting factor, most of the incidents happened in Darkness but there was street lighting, this may be due to less Visibility in nights. Vehicle damages results more than $1500.

We also checked Tensorflow model to find if we can get better results by choosing 2 Hidden layers, activation function as softmax for multi classification target, optimizer Adam, loss as sparse_categorical_crossentropy, metrics accuracy, epochs 30, added regularization and validation size 0.2, we came up with better accuracy score 68, validation accuracy was better than training accuracy score.

## Next Steps:

1. We have to work more on hyper parameter tuning and Feature Importance to get better accuracy score
2. Offering better discounts for Drivers with safe driving.
3. Focus on Drivers who live North side of Chicago who has frequent crashes.

## Repository Structure

```
├── Data
├── .gitignore
├── Chicago_CarCrash presentation
├── Chicago_CarCrash.ipynb
└── README.md
```