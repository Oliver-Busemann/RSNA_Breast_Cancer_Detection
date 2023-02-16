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
#### 3) Training [RSNA_Notebook_3_Training.ipynb]
  -> For training a cv-setup was created: each fold should contain roughly the same number of cancer targets<br>
  -> The scans are augmented based on recommendation in paper<br>
  -> The other additional features are preprocessed with a pipeline and added to the scans after they ran through a pretrained net<br>
  -> Dataset was created that returns a scan and the additional piped information plus the target<br>
  -> A WeightedRandomSampler was tried to upsample cancer cases; Did not give the desired output to the loss of cancer cases was increased by a weight-factor<br>
  -> A pretrained EfficientNet_xl was used for the scans; The output was fed into another network and concatenated with the additional features<br>
  -> For that to work another mombined model was build<br>
  -> The parameters of the pretrained net were not trained in the following<br>
  -> Train fucntions & validation functions were created; Loss was individually adjusted based on current batch<br>
  -> Training- & validation-folds were created based on the scan_ids defined above<br>
  -> It was checked the no valid_scan_id was in the corresponding training fold<br>
  -> Dataloader were created<br>
  -> For each train-/valid-dataloader a model was created (correct: random initial weights loaded) and trained/evaluated for 13 epochs<br>
  -> The learning rate was reduced if valid_loss didnt decrease for 3 epochs<br>
  -> After training of each model (1 for each cv-setup) the weights were saved & the metrics from evaluation were added to a df & written to a csv<br>
  -> When each model was trained, the results were plotted<br>
  -> They showed a reduction in loss & pF1 but they could be trained longer (didnt fully converge yet)<br>
  -> Mean pF1-score was really low because it is 0 for a batch when there is no cancer case<br>
  -> Cancer cases only appear every ~46 time and the batch size is was 32<br>
