
# PHBS_MLF_2019
MLF Team Project

## Team members:
Name                   |     Student ID    |     GitHub ID
-----------------------|-------------------|---------------------------------
Hu Tianrui(胡天锐) | 1901212587 | [PeterHuTHU](https://github.com/PeterHuTHU)
Yu Haiyang(余海洋) | 1901212663 | [Yavin-1018](https://github.com/Yavin-1018)
Zhang Peidong(张培栋) | 1901212671 | [ZhangPeidong-Mack](https://github.com/ZhangPeidong-Mack)
Zhong Lin(钟林) | 1801212992 | [zhong-lin-pku](https://github.com/zhong-lin-pku)

## Project goal
Our goal is to predict trends of stocks and their future prices. We will use classifiers such as SVM, decision tree and random forest to predict trends of stocks and then compare advantages and disadvantages of each algorithm. Then we will use models such as linear regression, SVM, random forest and Multi-Layer Perceptron to predict specific prices, again we will compare advantages and disadvantages of each model. Other skills such as k-fold cross-validation will also be applied.

## Data Description
We use trading data of Shenzhen Stock Exchange and Shanghai Stock Exchange from 2017-01-01 to 2019-12-31. Features include the opening price, closing price, highest price, lowest price, trading volume and turnover. The dataset is too large so we only upload part of it. Click [here](https://pan.baidu.com/s/1aaYOzaOtSxtKzsZU-PMNlg) with extraction code "nspy" if you want to see a complete version of our data.

## Test

## TEST YU
hello


## Factor Introduction
We use some quantification factors: 
![Factor Introduction](image/pic_factors.bmp)
* MACD: Moving Average Convergence/Divergence, measures the separation and aggregation of short-term index moving average and long-term index moving average
* RSI: Relative Strength Index, reflect the prosperity of the market in a certain period of time
* EMA: Exponential Moving Average, a trend index 
* MOM: Momentum, measures the speed of price changes
* ATR: Average True Range, represent market change rate

## Decision Tree
For Decision Tree method, data preprocessing is really simple. We don't need to standardize the data, what we need to do is just generate labels. We also use weekly frequency data, and the tag value is determined by the positive and negative excess return of the next week compared to the whole market. The factors we use in Decision Trees are MACD, RSI, EMA, MOM and ATR. And we looking at the results of the model from two prespectives: 
### Method 1
We study the parameters for each stock seperately, and the most simple method is for each stock, we just divide the 145 samples into the training set and the testing set, and we can get the predicting acurracy.
And the average results for all stocks are listed here: 

training accuracy is:  96.86%
testing accuracy is:  52.13%
### Method 2
Logically speaking, we could not forecast the past with future data, so then we do another test, we use the samples in 2017 and 2018 as the training set, and the samples in 2019 as the testing set. And we are now interested in each week's results in 2019. 

The results are listed below. the average testing accuracy is 52.59%, and each week's results are displayed:
![Decision Tree Method 2](image/pic_decision_tree.bmp)
We can also see the F1 score and the confusion matrix:

accuracy_score is: 0.5259057730590577
precision_score is:  0.4416550979484806
recall_score is:  0.35027678380279537
f1_score is:  0.3906940251411418
![Decision Tree Method 2](image/pic_confusion_matrix.bmp)
We can find out that more than half of the stocks didn't beat the market, one of the reasons is that we use simple averages instead of market capitalization weighted averages, so the accuracy score and precision score are underestimated. 

If we set one parameter of the function, average as "weighted", which means we calculate metrics for each label, and find their average weighted by support, and can account for label imbalance, we find the results here: 
precision_score is:  0.5143724083513994
recall_score is:  0.5259057730590577
