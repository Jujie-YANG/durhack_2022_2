# The second Durhack in 2022

- Files Explanation
- Data Augment:

  - Baseline: ("RET_1")("mean") ["Date","Sector"]

    - baseline_RF.jpynb - 51.43%
    - baseline_log.jpynb - 50.88%
  - Questions to see which features
  -
  - Questions to ask sponsors:

    - Can we drop original features("RET_1 etc.") according to the feature importance
  - GroupBy: ("mean","std") - Considering adding 80 more features?

    - ["Date","Sector","Industry"] - baseline_RF_gbdsi - Jacky - 50.97%
    - ["Date","Sector"] - baseline_RF_gbds.ipynb - Andy - **Choose mean or std**
    - ["Date","Sector","Industry"] - baseline_log_gbdsi - Jacky
    - ["Date","Industry"] - baseline_RF_gbdi.ipynb - Ruisheng
    - ["Sector","Industry"] - baseline_RF_gbsi.ipynb - Tianshu
  - Conclusion:

    - 'mean' has less noise than 'std' (Therefore, choose mean only - (baseline_RF_gbds.ipynb - Andy))
    - Could add min and max
    - Change shift
    - Choose best splits
    - we can drop original features according to the feature importance
  - dot product - similarity (stock)



- ## Feature/Parameters Selection:
  - ### Final selected features
    - RET (1-20) _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean"
    - RET_1, RET_2, RET_3, RET_7, RET_14, RET_17

    - VOLUME 1,13 _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean"
    - VOLUME_1

    - RET (1-20) _ groupby (STOCK) _ "mean"
    - VOLUME (1-20) _ groupby (STOCK) _ "mean"
    

    - First 6 individual ones
    - Groupby first 6 individual ones separately


  - ### Optimized Parameters
    - Random Forest
      - K-fold = 4 
    - Lightgmb
      - K-fold = 8?
    
- ## Observation:
  - ### Feature Engineering
    - Group by # of features (2 < 3 < 4 > 5 > 6)
    - The feature importance of (RET_1, RET_2, RET_3, RET_7, RET_14, RET_17) are significantly higher than other individual ones
    - VOLUME 1,13 _ group by (STOCK, SECTOR, INDUSTRY, DATE) _ "mean" -- (51.82%, 1.17) higher than using all VOLUME GROUP BY the same features_mean -- 51.77%, 1.33 (Acc slightly higher , std slightly slower, as well higher feature importance)

  - ### Parameters comparison:
    - Random Forest:
      - K-fold = 4 (acc 4 > 6 > 8, std 4 lightly smaller than 6, 8 is the worst)
    - LightGBM:
      - K-fold = 8 (8: acc 51.42%, std 1.14; 6: acc 51.37%, std 0.74)
      - Other params(e.g. learning rate?)


- ## TODO list:
  - [X] Feature Engineering
  - [X] Feature Selection
  - [X] Compare different models:

    - [X] Random Forest
    - [ ] Logistic
    - [ ] LightGBM
    - [ ] Xgboost
    - [ ] Neural Networks

    Use tables to compare the Accuracy:


    |        | RF | Logistic |
    | -------- | ---- | ---------- |
    | Acc(%) |    |          |
    
- ## Model Performance Comparisons:
- Instruction:

  - For every team member:
    - please remember to ```git pull``` first before uploading your work!
    - Or you can upload your work directly via GitHub website
- MS word

  - [Final Report](https://durhamuniversity-my.sharepoint.com/:w:/g/personal/gldt31_durham_ac_uk/EZX_mdaJ90tJkijEf698WyEBxNfcG5HGmSEaMVDhSvJoSQ?e=7X5nkX)
  - [Ideas](https://durhamuniversity-my.sharepoint.com/:w:/g/personal/gldt31_durham_ac_uk/Ebx6isRb32dGq3DOFPWKx_0BC4BJwWFr7otds2pextGVxg?e=Id591G)
- Useful Links

  - [DEVPOST: DurHack2022](https://durhack-2022-2.devpost.com/?ref_feature=challenge&ref_medium=discover): This Durhack
  - [DEVPOST: DurHack2021](https://durhack2022.devpost.com/?ref_feature=challenge&ref_medium=discover): Last Durhack
  - [Durhack 2022 Discord](durhack.com/discord)
  - [Durhack Facebook](https://www.facebook.com/DurHackEvent)
  - [Durhack Website](https://durhack.com/): Look for the event schedule
- Sponsors

  - [MLH](https://hack.mlh.io/software)
