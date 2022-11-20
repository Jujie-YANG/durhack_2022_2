# The second Durhack in 2022 (Theme: DATA AUGMENT)

  - Questions to ask sponsors:
    - [ ]why before predicting X_test, we need to fit? Does it pre-train the test data!!??
    - [ ]dot product - similarity (stock)??

- ## To-Do List:
  - [X] Fill missing data value with 0
  - [X] Feature Engineering

    - [X] min & max
    - [X] GroupBy individual feature
    - [X] GroupBy 2 features
    - [X] GroupBy 3 features
    - [X] GroupBy 4 features
    - [X] GroupBy 5 features
    - [X] GroupBy 6 features
  - [X] 1st round Feature Selection (110 columns in total)
  - [ ] Deal with Volumn outliers (Normal Distribution)
  - [X] 2nd round Feature Selection
  - [X] 3rd round Feature Selection
  - [X] Fine Tune Params
    - [X]n_splits(K-fold)
    - [X]shifts
  - [X] Compare different models:
    - [X] Random Forest
    - [X] Logistic
    - [X] LightGBM
    - [X] Xgboost
    - [ ] Neural Networks

- ## Feature Engineering:
  - ### Observation
    - 'mean' has less noise than 'std'
    - Group by # of features (2 < 3 < 4 > 5 > 6)
    - The feature importance of (RET_1, RET_2, RET_3, RET_7, RET_14, RET_17) are significantly higher than other individual ones
    - VOLUME 1,13 _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean" -- (51.82%, 1.17) higher than using all VOLUME GROUP BY the same features_mean -- 51.77%, 1.33 (Acc slightly higher , std slightly slower, as well higher feature importance)
    - Regarding first 6 individual features, DATE is significantly high
    - Regarding Groupby first 6 individual features separately, DATE is quite important
  
  - ### Results
    - GROUP BY (STOCK, SECTOR, INDUSTRY, DATE)
    - RET of specific days

- ## Feature Selection: (Based on Feature Importance of Random Forest model)


  - ### 1st round Feature Selection (110 columns in total)


    | Features                                                        | # of columns |
    | :---------------------------------------------------------------- | -------------- |
    | RET (1-20) _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean"  | 20           |
    | RET_1, RET_2, RET_3, RET_7, RET_14, RET_17                      | 6            |
    | VOLUME 1,13 _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean" | 2            |
    | VOLUME_1                                                        | 1            |
    | RET (1-20) _ groupby (STOCK) _ "mean"                           | 20           |
    | VOLUME (1-20) _ groupby (STOCK) _ "mean"                        | 20           |
    | DATE                                                            | 1            |
    | RET (1-20) _ group by (DATE) _ "mean"                           | 20           |
    | VOLUME (1-20) _ group by (DATE) _ "mean"                        | 20           |
  - ### 2nd round Feature Selection (29 columns in total)


    | Features                                                        | # of columns |
    | :---------------------------------------------------------------- | -------------- |
    | RET (1-20) _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean"  | 20           |
    | RET_1, RET_2, RET_3, RET_7, RET_14, RET_17                      | 6            |
    | VOLUME 1,13 _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean" | 2            |
    | VOLUME_1                                                        | 1            |
  - ### 3rd round Feature Selection (6 columns in total)


    | Features (>0.015)                        | # of columns |
    | ------------------------------------------ | -------------- |
    | RET_1                                    | 1            |
    | RET_17                                   | 1            |
    | RET_1_STOCK_SECTOR_INDUSTRY_DATE_mean    | 1            |
    | RET_4_STOCK_SECTOR_INDUSTRY_DATE_mean    | 1            |
    | RET_17_STOCK_SECTOR_INDUSTRY_DATE_mean   | 1            |
    | VOLUME_1_STOCK_SECTOR_INDUSTRY_DATE_mean | 1            |


- ## Parameter Tuning
  - ### Parameters comparison:

    - Random Forest:
      - K-fold = 4 (acc 4 > 6 > 8, std 4 lightly smaller than 6, 8 is the worst) - 8:51.47%,1.23; 4: 51.57%, 0.76
    - LightGBM:
      - K-fold = 8 (8: acc 51.42%, std 1.14; 6: acc 51.37%, std 0.74)
      - learning_rate = 0.2 (comparing with 0.01, 0.1, 0.2, 0.3, 0.5) - grid search
      - n_estimators = 50 (comparing with 25, 30, 35, 50)
      - num_leaves = 5 (comparing with 5, 30, 50)
  - ### Optimized Parameters

    - Random Forest
      - K-fold = 4
    - Lightgmb
      - K-fold = 8

    
- ## Model Performance Comparisons:


  - ### Model params:

    - RF: (n_estimators = 500, max_depth=6, random_state:0, n_jobs=-1)
    - LightGBM(1): (n_estimators = 50, learning_rate = 0.2, num_leaves = 5)
    - LightGBM(2): (n_estimators = 500, max_depth=6, random_state:0, n_jobs=-1) -- same as RF
  - ### Baseline:

    - GROUP BY ["Date","Sector"] FOR "RET_1" ON "mean"

    |                | RF    | Logistic | LightGBM(1) | LightGBM(2) | xgboost |
    | ---------------- | ------- | :--------- | ------------- | ------------- | --------- |
    | Average Acc(%) | 51.31 | 50.88    | N/A         | N/A         | N/A     |
    | std            | 0.58  | 0.09     | N/A         | N/A         | N/A     |
  - ### 1st round Feature Selection (120 columns in total)


    |                | RF          | Logistic | LightGBM(1) | LightGBM(2) | xgboost    |
    | ---------------- | ------------- | :--------- | ------------- | ------------- | ------------ |
    | Average Acc(%) | ***51.74*** | 50.94    | 51.37       | 51.25       | 51.10      |
    | std            | 0.78        | 0.4      | 1.04        | 0.88        | ***0.23*** |
  - ### 2nd round Feature Selection (29 columns in total)


    |                | RF          | Logistic   | LightGBM(1) | LightGBM(2) | xgboost    |
    | ---------------- | ------------- | :----------- | ------------- | ------------- | ------------ |
    | Average Acc(%) | ***51.92*** | 50.73      | 51.53       | 51.01       | 50.64      |
    | std            | 0.75        | ***0.40*** | 1.14        | 0.74        | ***0.40*** |
  - ### 3rd round Feature Selection (6 columns in total)


    |                | RF          | Logistic | LightGBM(1) | LightGBM(2) | xgboost    |
    | ---------------- | ------------- | :--------- | ------------- | ------------- | ------------ |
    | Average Acc(%) | ***51.60*** | 51.14    | 51.58       | 51.20       | 51.28      |
    | std            | 0.46        | 0.42     | 0.83        | 0.53        | ***0.36*** |

- ## Durhack Related:
  - ### MS word
    - [Final Report](https://durhamuniversity-my.sharepoint.com/:w:/g/personal/gldt31_durham_ac_uk/EZX_mdaJ90tJkijEf698WyEBxNfcG5HGmSEaMVDhSvJoSQ?e=7X5nkX)
    - [Ideas](https://durhamuniversity-my.sharepoint.com/:w:/g/personal/gldt31_durham_ac_uk/Ebx6isRb32dGq3DOFPWKx_0BC4BJwWFr7otds2pextGVxg?e=Id591G)
  - ### Durhack 
    - [DEVPOST: DurHack2022](https://durhack-2022-2.devpost.com/?ref_feature=challenge&ref_medium=discover): This Durhack
    - [DEVPOST: DurHack2021](https://durhack2022.devpost.com/?ref_feature=challenge&ref_medium=discover): Last Durhack
    - [Durhack 2022 Discord](durhack.com/discord)
    - [Durhack Facebook](https://www.facebook.com/DurHackEvent)
    - [Durhack Website](https://durhack.com/): Look for the event schedule
  - ### Sponsors/APIs
    - [MLH](https://hack.mlh.io/software)
