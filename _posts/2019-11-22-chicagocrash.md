---
layout: post
title: The safest speed to drive in Chicago is 0mph
subtitle: Unit 2 Data Science project
gh-repo: daattali/beautiful-jekyll 
comments: false
---

**Can we determine what conditions lead to vehicle collisions that result in serious injury or death?**













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
