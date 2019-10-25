---
layout: post
title: Data Wrangling and Storytelling
subtitle: Unit 1 Data Science project
gh-repo: daattali/beautiful-jekyll 
comments: false
---

**Do counties with large GDP also have a higher economic growth rate than counties with low GDP?**

One potential effect of America's demographic shift toward cities from the country is changing GDP in both the urban and rural counties across the United States.  For this project, I looked at data from all 3113 county-equivalent economic areas in the United States from 2012 to 2015.  The values in the data use chained dollar amounts to account for inflation.

**Distribution of Counties by 2015 GDP:**

![GDP](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/growthswarm.png){: .center-block :}

Just over half of all counties fit within the GDP range of $100 million to $1 billion dollars, and another 35% are within the $1 billion to $10 billion range.  Among these highly populated GDP ranges, the three year median growth rate does show a higher average percentage increase in the counties with larger GDPs, and that trend continues for counties with an economy of more than $10 billion and more than $100 billion.

| GDP Range | Number of Counties | Mean growth 2012-2015 |
| :------ |:--- | :--- |
| < $10M | 1 | 19.27% |
| 10M - 100M  | 165 | 2.52 |
| 100M - 1B | 1558 | 1.58 |
| 1B - 10B | 1102 | 1.86 |
| 10B - 100B | 265 | 2.32 | 
| > 100B | 22 | 3.24 |

**Counties with a low GDP can't be as easily defined in terms of growth**

It seems that higher rates of growth occur in counties with both large and small shares of GDP.  Loving, Texas is the only county with less than 10 million in GDP for 2016, but it's also in the top 1% of the top 1% in growth.  Here's the distribution of counties by GDP:

All of the outliers in growth rate occur in counties in the lower buckets of GDP size.  This makes sense as the impact made by any new development as a percentage of GDP is buffered by the scale of existing economic activity.

![Choropleth](https://github.com/johnwesleyharding/johnwesleyharding.github.io/raw/master/img/growthmap.png)

We can see the outlier counties in economic growth rate tend to be rural areas.  Many in Texas are likely related to the oil and gas boom spurred by fracking during the middle of the decade.  
