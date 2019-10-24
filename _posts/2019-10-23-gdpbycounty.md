---
layout: post
title: Data Wrangling and Storytelling
subtitle: Unit 1 Data Science project
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [test]
comments: false
---

**Do counties with large GDP also have a higher economic growth rate than counties with low GDP?**

One potential effect of Americans increasing move toward cities is a shift in GDP of both the urban and rural counties as those demographics change.  I looked at data from all 3113 county-equivalent economic areas in the United States from 2012 to 2015.  

**Distribution of Counties by 2015 GDP:**

| GDP Range | Number of Counties | Mean growth 2012-2015 |
| :------ |:--- | :--- |
| < $10M | 1 | 19.27% |
| 10M - 100M  | 165 | 2.52 |
| 100M - 1B | 1558 | 1.58 |
| 1B - 10B | 1102 | 1.86 |
| 10B - 100B | 265 | 2.32 | 
| > 100B | 22 | 3.24 |

## This next part has pictures.

It seems that higher rates of growth occur in counties with both large and small gdps.  Loving, Texas is the only county with less than 10 million in GDP for 2016, but it's also in the top 1% of the top 1% in growth.  Here's the distribution of counties by GDP:

![GDP](https://imgur.com/lPd9YV8.jpg)

Nebrask is doing better than Nevada.  Texas has way too many counties!

![Barplot](https://imgur.com/u1uI27l.jpg){: .center-block :}



```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

