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

## 配置 PySpark

1. 配置步骤：
    <a href="http://blog.csdn.net/sinat_26599509/article/details/51204594" target="_blank">在 Mac OSX上配置 PySpark</a>
2. PySpark Downloads:
    <a href="http://spark.apache.org/downloads.html" target="_blank">Download Apache Spark™</a>
3. Spark Docs：
    <a href="http://spark.apache.org/docs/latest/index.html" target="_blank">Spark Docs</a>


## 执行 Examples

### 交互式执行
spark 提供了各种语言的 shell。对于 python，只需要执行 `./bin/pyspark` 即可。

### 执行代码
pyspark 的 demo 位于`/examples/src/main/python/`。

    ./bin/spark-submit ../examples/src/main/python/pi.py 10

## Spark 基本概念

### RDD

    Spark’s primary abstraction is a distributed collection of items called a Resilient Distributed Dataset (RDD). RDDs can be created from Hadoop InputFormats (such as HDFS files) or by transforming other RDDs. Let’s make a new RDD from the text of the pi.py file in the Spark source directory:    

**Create RDD**
```Python
textFile = sc.textFile('pi.py')
textFile.count()
textFile.first()
```

**Transforming RDD**
```Python
lineWithRandom = textFile.filter(lambda line: "random" in line)
lineWithRandom.count()
lineWithRandom.first()
```

### MapReduce
Demo: 
```Python
textFile.map(lambda line: len(line.split())).reduce(lambda a, b: a if (a > b) else b)
```

`.map()` 将行与单词数关联，并且产生新的 `RDD`。 `.reduce` 作用于此 `RDD`, 最终算出最大单词数。 

`MapReduce` 是一种常见的数据流模式(Data Flow Pattern), Spark 可以很容易实现 `MapReudce`。

```Python
wordCounts = textFile.flatMap(lambda line: line.split()).map(lambda word: (word, 1)).reduceByKey(lambda a, b: a+b)

wordCounts.collect()
```

### Caching 


