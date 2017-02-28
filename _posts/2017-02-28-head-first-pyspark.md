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
    ./bin/pyspark

### 执行代码
pyspark 的 demo 位于`/examples/src/main/python/`。

    ./bin/spark-submit ../examples/src/main/python/pi.py 10
