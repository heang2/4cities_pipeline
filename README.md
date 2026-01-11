# 4cites_workflow
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


[**Forcasting four representative cities of their future traffic conditions**](https://remaintobeseen)

Author1,Author2,Author3,Author4,Author5

[Journal](https://remaintobeseen)

[Project homepage](https://anghe-mark-intelligence.github.io/Forcasting-4-cites-in-us/)

In this repo, we built a workflow from OD prediction to traffic assignment, and then to urban congestion analysis and accessibility analysis in different [SSP scenario](https://github.com/usutradhar/Population-Trend-Analysis).The workflow can be divided into four stages: 1. LODES raw data processing 2. Time series model prediction of OD flow data 3. Traffic assignment 4. ArcGIS urban congestion visualization and accessibility analysis.


<p align="center">
 <img width="717" height="291" alt="2099e89e5fdde54843437321e6f0216e" src="https://github.com/user-attachments/assets/db9ee9ce-91f2-4d22-bbf9-7470daf6c76f" />
</p>


## Installation
We suggest that you create an conda environment to run this project.The required environment can be configured according to [requirements.txt](https://github.com/Anghe-Mark-intelligence/4cities_workflow/blob/main/requirement.txt).

```
conda create -n us_city_pred python=3.10 -y
conda activate us_city_pred
pip install -r requirements.txt
```

## 1.LODES raw data processing
We are using using the data from the [LODES](https://lehd.ces.census.gov/data/lodes/)  dataset provided by the U.S. Census Bureau.The LODES dataset includes commuting data for the workforce in all states across the United States over multiple years, which have been widely used in existing studies.



## 2.Time series model prediction of OD flow data



## 3.Traffic assignment
We have already used a relatively sophisticated traffic assignment method in our previous work, so we can directly use the [Colab code](https://colab.research.google.com/drive/19iGXJAHx5_vvoZMbOmbBXdTwxzVogB2V?usp=sharing) and [github code](https://github.com/xuxiaotong/A_unified_and_validated_traffic_dataset_for_20_U.S._cities) for this step.


## 4.ArcGIS urban congestion visualization and accessibility analysis


## More features


## License

MIT License
