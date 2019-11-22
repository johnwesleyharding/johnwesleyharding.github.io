---
layout: post
title: The safest speed to drive in Chicago is 0 miles per hour
subtitle: Unit 2 Data Science project
gh-repo: daattali/beautiful-jekyll 
comments: false
---

**The data**

The Chicago collisions datasets for people, vehicles, and crashes have almost 800 thousand observations from the past five years that can be used to determine the conditions likely to result in serious injuries to drivers, passengers or pedestrians.  I selected 'Most Severe Injury' as the target feature and specifically focused on the ‘Fatal’ and ‘Incapacitating Injury’ labels.  The majority of five target classes is 'No indication of injury' at ~88% frequency, while 'Fatal' occurs in only 0.08% of cases.  Because of the extreme weights of this multi-class target, I randomly undersampled the observations for heavier labels before modeling the training data.

| most severe injury | raw | balanced |
| :------ | :--- | :--- |
| NO INDICATION OF INJURY | 87.9 % | 20.0 % |
| NONINCAPACITATING INJURY | 6.6 | 20.0 |
| REPORTED, NOT EVIDENT | 3.9 | 20.0 |
| INCAPACITATING INJURY | 1.5 | 20.0 |
| FATAL | 0.1 | 20.0 |

**Features**

Selected features from the data include one continuous variable, the posted speed limit, and several ordinally encoded categoricals: weather and lighting conditions, crash type (head-on, rear-end, etc), road defects, month of year, hour of day, and contributing causes.  These features all came from the primary crash dataset, but additional information about the involved persons and vehicles may also be relevant.  A feature that described a post-collision action of 'drive away' was removed to avoid spoiling the target.

The goal is to determine which of these features are most often present in collisions with fatal injuries.  Using a stratified dummy classifier, I identified a baseline for recall of the 'Fatal' label at 0% and and overall model accuracy of 78%. 

**Models**

I selected Logistic Regression as a linear classification model, Random Forest Classifier as a tree model, and used Random Search CV for validation and hyperparameter tuning in both models.  To best work toward the goal, the validation metric is recall score for the 'Non-incapacitating Injury', 'Incapacitating Injury', and 'Fatal' labels.  

```python
scoring = make_scorer(recall_score, 
                      average = 'macro', 
                      labels = ['NONINCAPACITATING INJURY', 
                               'INCAPACITATING INJURY', 'FATAL']),
```

The best cross validation score for Logistic Regression is 0.28, with the tree model evaluating slightly better at 0.33.

**Logistic Regression Test Results**
![conflogr](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/crashconflogr.png){: .center-block :}

| most severe injury | predicted | precision | recall | actual |
| :------ | :--- | :--- | :--- | :--- |
| FATAL | 18977 | 0.00 | 0.49 | 70 |
| INCAPACITATING INJURY | 7058 | 0.02 | 0.14 | 1060 |
| NO INDICATION OF INJURY | 17170 | .91 | 0.25 | 62901 |
| NONINCAPACITATING INJURY | 8437 | 0.08 | 0.15 | 4681 |
| REPORTED, NOT EVIDENT | 19932 | 0.05 | 0.35 | 2862 |

The Logistic Regression model predicted almost 19000 fatalities in the test data, and accurately found fewer than half of the 70 true values.  The test score for 'Fatal' recall is 49% and the overall accuracy of the model is only 25%.

**Random Forest Test Results**

![conftree](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/crashconftree.png){: .center-block :}

| most severe injury | predicted | precision | recall | actual |
| :------ | :--- | :--- | :--- | :--- |
| FATAL | 7523 | 0.01 | 0.67 | 70 |
| INCAPACITATING INJURY | 5453 | 0.05 | 0.25 | 1060 |
| NO INDICATION OF INJURY | 32943 | .95 | 0.50 | 62901 |
| NONINCAPACITATING INJURY | 8479 | 0.12 | 0.22 | 4681 |
| REPORTED, NOT EVIDENT | 17176 | 0.05 | 0.33 | 2862 |

The Random Forest Classifier model predicted just over 7500 fatalities in the test data, and accurately found two-thirds of the true values.  The test score for 'Fatal' recall is .67 and the overall accuracy of the model is 47%.

**Feature Analysis**

Permutation importance from the tree model produced only 'Posted Speed Limit' as relevant feature in terms of weight for the best model.  Despite re-sampling for balance in the train data, the reality of those same distributions in the test data still warps many of of the prediction results.

![permutation](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/crashpermtree.png){: .center-block :}

**Conclusion**

The goal of identifying factors in fatal collision is not achieved by these models.  It's possible that even after balancing the training data, the skew of ground truth toward non-injury prevented meaningful predictions.  Ultimately I'm not sure if this is a case where the outcome is simply not strongly related to the available features or if an errant path in the wilderness of data science left me lost with no trail of bread crumbs.
