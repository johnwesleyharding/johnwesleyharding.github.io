---
layout: post
title: The safest speed to drive in Chicago is 0mph
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

The goal is to determine which of these features are most often present in collisions with fatal injuries.  Using a dummy classifier, I identified a baseline for recall of the 'Fatal' label of . 

**Models**

I selected a Logistic Regression as a linear classification model, Random Forest Classifier as a tree model, and used Random Search CV for validation and modest hyperparameter tuning in both models.  To best work toward the goal, the validation metric is recall score for the 'Non-incapacitating Injury', 'Incapacitating Injury', and 'Fatal'.  The best cross validation score for Logistic Regression is 0.28, while the tree model yielded a score of ####.  

![permutation](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/crashpermutation.png){: .center-block :}

Permutation importance from the tree model produced only 'Posted Speed Limit' as relevant feature in terms of weight for the best model.  Despite re-sampling for balance in the train data, the reality of those same distributions in the test data still warps many of of the prediction results.

**Random Forrest Test Results**

![confusion](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/image.png){: .center-block :}

| most severe injury | predicted | precision | recall | actual |
| :------ | :--- | :--- | :--- | :--- |
| FATAL | 3796 | 0.01 | 0.67 | 63 |
| INCAPACITATING INJURY | 3755 | 0.09 | 0.29 | 1103 |
| NO INDICATION OF INJURY | 55354 | 1.00 | 0.88 | 62929 |
| NONINCAPACITATING INJURY | 3557 | 0.28 | 0.22 | 4649 |
| REPORTED, NOT EVIDENT | 5112 | 0.27 | 0.48 | 2830 |

**Conclusion**

Ultimately I'm not sure if this is a case where the outcome is simply not strongly related to the sample features or if an errant path in the wilderness of data science left me lost with no trail of breadcrumbs.
