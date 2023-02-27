# PVOD Regression

This repository is based on a photovoltaic dataset called [PVOD](https://github.com/yaotc/PVODataset) which contains
PV power output and some weather conditions data. 

The detailed process can be viewed by checking my blog here.
[PVOD Regression - Photovoltaic power output prediction based on weather data](https://smallsquare.github.io/PVOD-regression/)

## Brief introduction

Several classical models are used in this repository.
(Random forest, Gradient boosting machine and Multi-layer perceptron)

First, checking the information of the metadata. The entire dataset is formed by data from 10 stations, but they're
separate in terms of files. So I will use `station03` as an example.

Then, some basic observation of dataset are made.

Correlation analysis:

![Correlation](img/correlation.png)

Target feature distribution:

![Distribution](img/distribution.png)

Also, feature engineering and feature selection are needed. The correlation of selected features is like following:

![Correlation2](img/correlation2.png)

Well, we are finally ready to model. And here is the performance comparison of models with default hyper-parameters.

| Model |  MAE   |  MSE   |  RMSE  | R-square |
|:-----:|:------:|:------:|:------:|:--------:|
|  RF   | 0.5162 | 1.1332 | 1.0646 |  0.9524  |          
|  GBM  | 0.5841 | 1.1142 | 1.0556 |  0.9532  |          
|  MLP  | 1.1181 | 3.7166 | 1.9278 |  0.8440  |          

(The performance below is for reference only, as we have not looked carefully for hyper-parameters.)

Since GBM has the best performance, we can see how close the prediction of GBM made is to the ground truth.

![Prediction](img/prediction.png)

The RF and GBM can tell the importance of features:

```
- RF Feature Importance -
lmd_temperature 
 > 9.6774 %
lmd_pressure 
 > 3.6530 %
lmd_winddirection 
 > 1.0908 %
lmd_windspeed 
 > 1.1318 %
time_sin 
 > 53.0341 %
time_cos 
 > 24.2303 %
date_sin 
 > 2.8041 %
date_cos 
 > 4.3784 %
```
```
- GBM Feature Importance -
lmd_temperature 
 > 9.3780 %
lmd_pressure 
 > 3.5278 %
lmd_winddirection 
 > 0.7219 %
lmd_windspeed 
 > 0.6464 %
time_sin 
 > 53.9076 %
time_cos 
 > 23.7690 %
date_sin 
 > 2.8473 %
date_cos 
 > 5.2021 %
```