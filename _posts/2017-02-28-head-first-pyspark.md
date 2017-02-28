---
layout: post
title:  "head first pyspark"
image: ''
date:   2017-02-28 11:20:00
tags:
- pyspark, spark
description: ''
categories:
- spark
serie: spark
---
<p class="music-read"><a href="https://y.qq.com/n/yqq/song/434676_num.html?ADTAG=h5_playsong&no_redirect=1">Music for reading</a></p>

<img src="/land-ml/assets/img/spark/header-head-first-pyspark.png">


## 一、配置 PySpark

1. <a href="http://spark.apache.org/downloads.html" target="_blank">Download Apache Spark™</a>
2. <a href="http://blog.csdn.net/sinat_26599509/article/details/51204594" target="_blank">在 Mac OSX 上配置 PySpark</a>
3. <a href="http://spark.apache.org/docs/latest/index.html" target="_blank">Spark Docs</a>


## 执行模式
Spark 提供了两种 执行模式。

1. 交互式执行
spark 提供了各种语言的 shell。对于 python，只需要执行 `./bin/pyspark` 即可。交互模式可以很方便测试 API。

2. 执行代码
pyspark 的 demo 位于`/examples/src/main/python/`。

    ./bin/spark-submit ../examples/src/main/python/pi.py 10

## Spark 基本概念

### RDD

    Spark’s primary abstraction is a distributed collection of items called a Resilient Distributed Dataset (RDD). RDDs can be created from Hadoop InputFormats (such as HDFS files) or by transforming other RDDs. Let’s make a new RDD from the text of the pi.py file in the Spark source directory:    

**Create RDD**

{% highlight python %}

textFile = sc.textFile('pi.py')
textFile.count()
textFile.first()

{% endhighlight %}

**Transforming RDD**

{% highlight python %}

lineWithRandom = textFile.filter(lambda line: "random" in line)
lineWithRandom.count()
lineWithRandom.first()

{% endhighlight %}

### MapReduce
Demo: 

{% highlight python %}

textFile.map(lambda line: len(line.split())).reduce(lambda a, b: a if (a > b) else b)

{% endhighlight %}

`.map()` 将行与单词数关联，并且产生新的 `RDD`。 `.reduce` 作用于此 `RDD`, 最终算出最大单词数。 

`MapReduce` 是一种常见的数据流模式(Data Flow Pattern), Spark 可以很容易实现 `MapReudce`。

{% highlight python %}

wordCounts = textFile.flatMap(lambda line: line.split()).map(lambda word: (word, 1)).reduceByKey(lambda a, b: a+b)

wordCounts.collect()

{% endhighlight %}


### Caching 

    Spark also supports pulling data sets into a cluster-wide in-memory cache. This is very useful when data is accessed repeatedly, such as when querying a small “hot” dataset or when running an iterative algorithm like PageRank. As a simple example, let’s mark our linesWithSpark dataset to be cached:

