---
layout: post
title: The safest speed to drive in Chicago is 0mph
subtitle: Unit 2 Data Science project
gh-repo: daattali/beautiful-jekyll 
comments: false
---

**Can we determine what conditions lead to vehicle collisions that result in serious injury or death?**

The Chicago collisions datasets for people, vehicles, and crashes have almost 800 thousand samples that can be used to determine the conditions likely to result in serious injuries to drivers, passengers or pedestrians.  Like when a car hits a person - that's not good at all.  I selected 'Injury Classification' as the target feature because it says 'classification' right there in its name, ezpz.  The majority of five target classes is 'No indication of injury' at ~92.5% frequency, and the class of principle interest is 'Fatal' occurring in only 0.04% of cases.  Because of the extreme weights of the multi-class target, preprocessing to ?stratify? the proportion of samples is necessary, but I haven't yet figured out how to go about this.  [critical failure: 1]

I am currently using all features other than the target for modeling.  I will select features more carefully after determining if I can merge in additional data.  Until then many features are irrelevant and potential leakage exists from at least four features (airbag, ejection, ems, hospital). [critical failure: 2]

I selected a Logistic Regression as a linear classification model, Random Forest Classifier as a tree model, and recall score for the 'Fatal' and 'Incapacitating Injury' as the evaluation metric.  I use Random Search CV for model validation and hyperparameter selection in the tree model.  I don't know what hyperparameters to set for Logistic Regression yet.  [critical failure: 3]  The best validation score in the tree model is .02, which seems terrible but maybe it is at least an indication that I succeeded in setting up the score correctly in RandomSearchCV.  [potential awesomeness: 1]  The score could also improve with a better fit - currently very limited do to processing time (6 fits in 10 minutes with very small hyperranges).  Logistic Regression yielded a validation score of [forgot to record, cleared output already to rerun for the model for which I can set hyperparameters.

I still need to look into how to get feature importances from the best estimator, since that's kind of the whole point of the project. [critical failure: 4]

Because of the aforementioned weight imbalance, the metric was unable to register a single desired fatality prediction in the test data and said: "Precision and F-score are ill-defined".  [critical failure: 5]  Majority class recall is real good though, 0.99!

![confusion](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/image.png){: .center-block :}

| label | predicted | precision | recall | actual |
| :------ |:--- | :--- | :--- | :--- |
| FATAL | 3796 | 0.01 | 0.67 | 63 |
| INCAPACITATING INJURY | 3755 | 0.09 | 0.29 | 1103 |
| NO INDICATION OF INJURY | 55354 | 1.00 | 0.88 | 62929 |
| NONINCAPACITATING INJURY | 3557 | 0.28 | 0.22 | 4649 |
| REPORTED, NOT EVIDENT | 5112 | 0.27 | 0.48 | 2830 |

![confusion](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/crashpermutation.png){: .center-block :}

**Conclusion**

Ultimately I'm not sure if this is a case where the outcome is simply not strongly related to the sample features or if an errant path in the wilderness of data science left me lost with no trail of breadcrumbs.
