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

```scala
val rdd = sc.parallelize(0 to 999,8)
val sample = rdd.takeSample(false, 4)
```
rdd will not be evaluated until the second line, since the value that is assigned to it is not needed until then.

**Now, onto the questions**

Q: Why did Spark fire off eight different tasks?
A: We split the data into 8 parts when the `sc.parallelize(0 to 999,8)` function was used, hence we get a task per partition.

Q: Why would Spark create two jobs to take the sample?
A: I cannot say that I fully understand the reason for this, but from what I read, I believe that unless one is very specific, Spark decides its own execution plan includding the level of parallelism, caching and so on.

Q: Explain why there are multiple result files.
A: I am not sure whether this reffers to the "duplicate files", one of them having a .crc extention, or to the fact that there is a part 0 and a part 1 to the output. In regards to the multiple parts of the output, I believe this might be due to its size. I believe that the .crc (Cyclic Redundancy Check) files are there for exactly the reason you would think - redundancy checks!; now, I do not know why Spark does this and Hadoop does not (if that was even a question).

Q: What does [^a-z] mean? What about the $ sign at the end?
A: Now, I will be  honest and tell you all that I found a very useful [tool](https://regexr.com/) online that evaluates the regular expressions that you type in. As such, I found out that [^a-z] is a negated set, meaning that it matches any character that is not a lower case letter in the English alphabet and $ matches the end of the string.

Q: Why are the counts different (and, why are they higher than before, and not lower)?
A: Well, two big things happened: all letters were set to lower case, and this already brings up the number by a bit since the mapping is case sensitive; secondly, all non-letter characters were removed so now "bone" and "bone." match as well, bringing the number a lot higher.

These are the questions that appeared in part A. In part B there were not that many (serious) questions, and those that were I was honestly not very able to answer. As compensation, here is the code I wrote in part A to find how many chars the longest line has!

```scala
%spark
// Empty cell for the exercise
println("The longest line in the text has " 
            + lines.reduce((a,b)=>a+b).split("\\.").map(x => x.length).
            reduce((a,b)=> a max b) + " characters.")
```
Output: The longest line in the text has 2808 characters.

### Conclusion
---
The overall experience with Spark and Scala was surprisingly pleasant. It was definetly nicer to work in a notepad compared to vim, so that might have played a big part in the "enjoyment" of the assignment. As it can be seen, I have understood a bit about Spark and Scala but not everything, but I think this is a good beginning.
