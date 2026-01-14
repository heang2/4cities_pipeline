# 4cites_pipeline
[![Project Page](https://img.shields.io/badge/Project-Page-blue)](https://heang2.github.io/4cites_project_page/)
[![arXiv](https://img.shields.io/badge/arVix-2000.12345-red)](https://remaintobeseen)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[**Forcasting four representative cities of their future traffic conditions**](https://remaintobeseen)

Author1,Author2,Author3,Author4,Author5

[Journal](https://remaintobeseen)


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
If the installation is missing, please install.
Direct installation is likely to fail, you can also install it separately or use [Google Colab](https://colab.research.google.com/).The alternative solution is to [install using Docker](./docs/Cites_docker_setup.md).

## 1.LODES raw data processing
We are using using the data from the [LODES](https://lehd.ces.census.gov/data/lodes/)  dataset provided by the U.S. Census Bureau.The LODES dataset includes commuting data for the workforce in all states across the United States over multiple years, which have been widely used in existing studies.

OD_process folder: ‘main.py’ is the main entrance of code. To run this code:

First, please define the state/city/download file path according to your need.

Second, prepare the raw 'od' and 'xwalk' files from LODES dataset. For raw 'od' file, please rename 'state_xwalk.csv' to 'xwalk.csv' ; for raw 'xwalk' file, please rename 'state_od_main_JT00_2019.csv' to 'od2019.csv'. Put these two raw files in your download file path.

Then, run this code. You can get the network data ('cityname_link.csv' and 'cityname_node.csv') and the corresponding tract level OD data ('cityname_od.csv'). The given code is for downloading LODES version 7 of 2019, you can also adjust the code for downloading version 8 and other years.

00_Download_LODES.py: code for downloading LODES dataset.

01_Check_corruption_or_loss: code for checking the corruption or loss of the downloaded LODES dataset.

This step will output the OD martix of the state/city,by processing historical data,we can get data in different year of the same city.Then,using OD martix,we can move on to the next step:Time series model prediction of OD flow data.

## 2.Time series model prediction of OD flow data
We are using a time series model, so you need enough years of time series data to input into the model.So we suggest that you have as much historical OD data as possible to avoid ARIMA oscillatory.

OD_predict_pr_and_analysis folder:‘main.py’ is the main entrance of code. To run this code:

First,please fill in the historical year od data of the city you need in od_historical data one folder for one year.

Second,define start_historical_year、end_historical_year、start_forecast_year、end_forecast_year,it represent the input od data and the future od data will be forecasted.

Then,run this code(Default is parallel).You can obtain the OD probability matrix for future years.We need real OD traffic flow as traffic assignment, so we calibrate it with SSP data.Use the code generate_od_from_pr.py,define the SSP_BY_YEAR and run the code,then you can get od_matrix,using transformation_csv.py to convert the entire OD matrix into the forms of O_ID, D_ID, and number,then We can move to the next step.


## 3.Traffic assignment
We have already used a relatively sophisticated traffic assignment method in our previous work, so we can directly use the [Colab code](https://colab.research.google.com/drive/19iGXJAHx5_vvoZMbOmbBXdTwxzVogB2V?usp=sharing) and [github code](https://github.com/xuxiaotong/A_unified_and_validated_traffic_dataset_for_20_U.S._cities) for this step.
After running the above code, it is necessary to save the result data output by Traffic assignment, such as assignment_desult.csv and network.csv, for the next step.


## 4.ArcGIS cities congestion visualization and accessibility analysis
### 4.1 ArcGIS cities congestion visualization
We use arcgis to visualize VOC images of cities.You can also refer to this [GitHub repo](https://github.com/xuxiaotong/A_unified_and_validated_traffic_dataset_for_20_U.S._cities).In the step3,the output file including assignment_result.csv and network.csv,network.csv can be used to visualize the road network of cities' road network and assignment_result.csv including road network speed data and congestion level, we can put it into ArcGIS to output VOC maps.


### 4.2 accessibility analysis
In this section,We use [matplotlib.pyplot (plt)](https://matplotlib.org/stable/index.html)、[LineCollection](https://matplotlib.org/stable/api/collections_api.html#matplotlib.collections.LineCollection)、[Normalize](https://matplotlib.org/stable/api/_as_gen/matplotlib.colors.Normalize.html) to visualize the accessibility of different income area(e.g.10mins).

<p align="center">
 <img width="1014" height="506" alt="c300abd2d0a943f7bd1a02485aa8ef6a" src="https://github.com/user-attachments/assets/c51ebe16-b852-4f46-8acb-713d6ed7cfc8" />
<p>

Please fill in your city and year under ./accessibility_analyses, run the code.

 
## More features
The code below can be used to help you analyze the OD you predict in step 2.

./OD_predict_pr_and_analysis/origin_desination_profiles.py:This script turns each OD matrix into a few easy-to-read profiles

./OD_predict_pr_and_analysis/year_to_year_change.py:This script compares OD flow matrices between two years (A -> B)

./OD_predict_pr_and_analysis/pr_distribution_diagonostics.py:Computes distribution/concentration stats (sparsity, entropy, Gini, top-k mass shares, quantiles)


## Basic information on 4 representative U.S. cities we select as e.g.

<p align="center">
 <img width="949" height="548" alt="image" src="https://github.com/user-attachments/assets/e9e6e36d-50e8-4cfa-bbc2-e7a1f08a01c9" />
<p>

 
| No. | City          | State        | Time Zone    | Census 2020 | Land Area (km²) | Population Density | Congestion Ranking |
|---:|---------------|--------------|--------------|------------:|----------------:|-------------------:|-------------------:|
| 1  | San Francisco | California   | Pacific Time | 873,965     | 121.5           | 7,195              | 3                  |
| 2  | Seattle       | Washington   | Pacific Time | 737,015     | 217.0           | 3,396              | 7                  |
| 3  | Portland      | Oregon       | Pacific Time | 652,503     | 345.8           | 1,887              | 16                 |
| 4  | Pittsburgh    | Pennsylvania | Eastern Time | 302,971     | 143.5           | 2,112              | 9                  |


## License

MIT License
