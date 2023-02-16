# RSNA_Breast_Cancer_Detection

https://www.kaggle.com/competitions/rsna-breast-cancer-detection

## GOAL: Detect Breast Cancer in mammography scans

### Notebooks:

#### 1) Data Exploration [RSNA_Notebook_1_Data_Exploration.ipynb]
  -> Analyse & visualize the provided scans<br>
  -> Analyse & visualize the additional information available<br>
#### 2) Preprocessing [RSNA_Notebook_2_Preprocessing.ipynb]
  -> There was a huge bottleneck with loading the data to the gpu (gpu util only ~3%)<br>
  -> The big scans are preprocessed to a much smaller size (512x512) and saved using pickle<br>
####
