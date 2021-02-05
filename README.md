# Multi-lable-classification
Multi-lable-classificationis a project for toxic comment classification.(Take kaggle toxic-comment-classification-challenge as our dataset)


## Data Resource
* [Toxic comment](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/overview)
* [GloVe word embedding](https://nlp.stanford.edu/projects/glove/)
```
wget http://nlp.stanford.edu/data/glove.6B.zip
unzip glove.6B.zip
```

## What's New

4.0 Model with revised cost funcstion (in the process)

3.0 Model with multiple output layers
3.1 Establish & tuning `LSTM` model.

2.0 Model with single output layer but have multiple neurons 
2.1 Establish & tuning `LSTM` model.

1.0 Restruct training / testing data
1.1 Observation/anlysis the dataset before diving in



## Data Restructure
- Training set - all data from train.csv
- Testing set - all data from test.csv except the data with value of -1, which which means it was not used for scoring

## Model strucutre
- Model 2.0
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/structure1.png" alt="Editor" width="700">
</div>

- Model 3.0
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/structure2.png" alt="Editor" width="700">
</div>



## Observation
- Generate descriptive statistics
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/categories.png" alt="Editor" width="700">
</div>

- What does the data look like?
<div align="center">
	<img src="https://github.com/HaoWeiHe/multi-lable-classification/blob/main/Img/data_sample.png" alt="Editor" width="700">
</div>


- Total comment counts for different labels
<div align="center">
	<img src="https://github.com/HaoWeiHe/multi-lable-classification/blob/main/Img/commentCounts.png" alt="Editor" width="500">
</div>
A quick calculation : sum(label_counts)/num_of_sample = 35098/159571 = 0.219, which indicate that the lower bound(accurancy metric) is around 78.1%


- Count numbers of different categories (Training set)
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/mulit-label-count.png" alt="Editor" width="700">
</div>

- Count numbers of different categories (Testing set before data restructure)
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/test_ori.png" alt="Editor" width="700">
</div>


- Count numbers of different categories (Testing set after data constructure)
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/test.png" alt="Editor" width="700">
</div>


- Word Length distribution
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/word_frequency_distribution.png" alt="Editor" width="700">
</div>
As per the mean and standard diviation from this data observation, we can set our embedding length to 255 and it can contain around 95% words in a text

- Word colud
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/wordCloud.png" alt="Editor" width="700">
</div>
A glimsp of our high frequency words

- Accurancy trend (Model 2.0)
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/acc.png" alt="Editor" width="700">
</div>

- Loss trend (Model 2.0)
<div align="center">
	<img src="https://github.com/HaoWeiHe/Multi-lable-classification/blob/main/Img/trend.png" alt="Editor" width="700">
</div>




## Evaluation metrics

### Model 2.0

Using LSTM with dropout. Accuarncy got 99.7% (The result is over optimism, for we use argmax to evaluate)

```
2000/2000 [==============================] - 15s 8ms/step - loss: 0.0780 - acc: 0.9970
Loss: 0.0780174732208252
Test Accuracy: 0.997014582157135
```
Confusion matrix. (To look into each categories)
```
>> training set 

               precision    recall  f1-score   support

        toxic       0.88      0.78      0.82     15294
 severe_toxic       0.58      0.37      0.45      1595
      obscene       0.88      0.74      0.81      8449
       threat       0.25      0.00      0.00       478
       insult       0.77      0.64      0.70      7877
identity_hate       0.67      0.00      0.01      1405

    micro avg       0.84      0.68      0.75     35098
    macro avg       0.67      0.42      0.47     35098
 weighted avg       0.82      0.68      0.73     35098
  samples avg       0.07      0.06      0.06     35098
  >> testing set 

               precision    recall  f1-score   support

        toxic       0.55      0.82      0.66      6090
 severe_toxic       0.39      0.42      0.40       367
      obscene       0.70      0.69      0.69      3691
       threat       0.00      0.00      0.00       211
       insult       0.62      0.58      0.60      3427
identity_hate       0.40      0.00      0.01       712

    micro avg       0.59      0.67      0.63     14498
    macro avg       0.44      0.42      0.39     14498
 weighted avg       0.58      0.67      0.60     14498
  samples avg       0.07      0.06      0.06     14498
  
```

### Model 3.0

Using LSTM with dropout. Accuarncy got only 18.4% (Over fitting)

```
Test Score: 0.4628007411956787
Test Accuracy: 0.1841709166765213

```
