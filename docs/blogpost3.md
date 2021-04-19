# Assignment 3
---

# Table of contents:
  * [Introduction](#introduction)
  * [Overall experience](#overall-experience)
  * [Conclusion](#conclusion)




### Introduction
---

My first reaction when opening the notebooks was "Oh thank God!". This is in part because it made me remember the Data Mining course, which I am sure many students following this course also have, and its Jupyter Notebooks. It was a breath of fresh air from the hadoop terminal and vim, to say the least.

While it was hard at first to draw that many connections between Hadoop and Spark, it gradually became pretty clear. RDD's were honestly not hard to work with and Scala was surprisingly much easier to work with compared Java - this is a big thing coming from me, seeing as I have failed Functional Programming two years in a row.

### Overall experience
---

As I am not sure what exactly I am supposed to talk about besides *mY eXpErIeNcE wItH sPaRk*, what I'm gonna do is go through and adress the questions posed throughout the notebooks, presenting the occasional line of code here and there.

But before that - let's talk lazy evaluation. In programming language theory (aka: from the people that make your clicky keyboards write something that actually makes sense) lazy evaluation is a strategy where the value of an expression is only called when it is needed e.g. in the expression "if A and B", expression B would not have to be computed if A was computed to be false, as the whole expression would result to false either way. This is the evaluation strategy Spark uses, maning that in the block of code 

```
val rdd = sc.parallelize(0 to 999,8)
val sample = rdd.takeSample(false, 4)
```



### Conclusion
---