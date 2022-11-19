# The second Durhack in 2022

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
- ## 
- ## Feature Selection:


  - ### Final selected features

    - all features group by "mean"
    - VOLUME_1
    - RET_1
    -
    -
    - max
    - min?
    -

Use tables to compare the Accuracy: (average different models' predictions)


|        | RF | Logistic |
| -------- | ---- | ---------- |
| Acc(%) |    |          |
|        |    |          |

- ## TODO list:


  - [ ] Jacky - logistic feature importance to see whether feature importance is the same as RF
  - [ ] Harrison - errors of feature importance for RF
  - [ ]
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
