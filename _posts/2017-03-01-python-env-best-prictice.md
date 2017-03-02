---
layout: post
title:  "Python 环境搭建最佳实践"
image: ''
date:   2017-03-01 18:00:00
tags:
- python
description: ''
categories:
- python
serie: python
---

<p class="music-read"><a href="spotify:track:4DAZ8UYNpWVIV46aLkN2Qp">Music for reading(spotify)</a></p>

<img src="http://cdn1.tnwcdn.com/wp-content/blogs.dir/1/files/2016/02/raw.gif">

## 一、重建 macOS python

macOS Sierra 自带的版本是 Python2，通常位于 `/usr/bin/python`, 即便是 root 权限，也无法删除。当然，由于诸多系统软件依赖 Python2，也不建议删除。

python 允许多版本共存，并且目前 python 有众多包管理利器，诸如：celler、pip，aconda 等。

为了更好地管理 python 环境，我们先把其他各个渠道的 python 版本，统统删掉(通常位于 `/usr/local/bin`)。

以 python2.7 为例，具体步骤：

1. 删除 Python 2.7 Framework。

``` shell
➜ where python
/usr/bin/python
/usr/local/bin/python
```

确定删除 `/usr/local/bin/python`。进入 `/usr/local/bin`，确定真身。

{% highlight shell %}
➜ls -al | grep "python"
lrwxr-xr-x  1 root       wheel    35B 12  7 10:28 2to3-2 -> ../Cellar/python/2.7.6_1/bin/2to3-2
lrwxr-xr-x  1 root       wheel    37B 12  7 10:28 2to3-2.7 -> ../Cellar/python/2.7.6_1/bin/2to3-2.7
lrwxr-xr-x  1 root       wheel    41B 12  7 10:28 easy_install -> ../Cellar/python/2.7.6_1/bin/easy_install
lrwxr-xr-x  1 root       wheel    45B 12  7 10:28 easy_install-2.7 -> ../Cellar/python/2.7.6_1/bin/easy_install-2.7
{% endhighlight %}

原来，位于 `../Cellar/python`, 删除之。

{% highlight shell %}
➜sudo rm -rf "../Cellar/python/"
{% endhighlight %}

2. 清除软链接

{% highlight shell %}
➜cd /usr/local/bin/python
➜ls -al | grep "python"
➜sudo rm -rf xxx
{% endhighlight %}

3. 清除 相关 profile files 中的 `PATH` 等环境变量。


## 二、安装 Anaconda

### 1. Anaconda 是什么？

<p>     Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.</p>

<p>     Additionally, you'll have access to over 720 packages that can easily be installed with conda, our renowned package, dependency and environment manager, that is included in Anaconda. See the packages included with Anaconda and the Anaconda changelog。</p>

<a href="https://www.continuum.io/" target="_blank">Anaconda</a> 其实用于科学计算的 Python 发行版(不仅限于 Python)，集成了100多个科学包及其依赖。

### 2. Conda
Anaconda 集成了 Conda,  Conda 解决了Python的不同版本隔离（环境管理）和包管理。







<figure class="foto-legenda">
	<img src="{{ "/land-ml/assets/img/spark/header-head-first-pyspark.png"}}" alt="">
	<figcaption> <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Repellat architecto minus sed dolorum debitis iste quae harum, fuga commodi libero voluptatum voluptates nemo, assumenda itaque. Placeat neque voluptatem, veritatis quae.</p>
	</figcaption>
</figure>

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Tenetur, illo eaque incidunt voluptatibus minus repudiandae eius consectetur tempore enim quisquam, quia veniam fuga autem, labore quas voluptate suscipit. Omnis, rem!Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vero, veritatis modi libero unde! Sapiente tempora eius cum doloribus, non, provident, veniam placeat veritatis quos possimus asperiores ipsam animi aliquam vel!

<img src="https://octodex.github.com/images/codercat.jpg" alt="">

## Lorem ipsum dolor, alias.?

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nemo minima veritatis est, unde nesciunt optio debitis. Soluta eos temporibus harum esse eveniet, alias praesentium, sapiente ipsa excepturi reprehenderit ullam ea.

### Warning!

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Atque corporis, fuga sequi cumque in quos excepturi placeat iste! Eaque voluptatum laudantium, recusandae optio! Rem impedit laborum enim minima aliquid, repellendus.<br>
` scalability` Lorem ipsum dolor sit amet, consebus tempora!:

1. <a href="http://dba.stackexchange.com/questions/4508/what-does-horizontal-scaling-mean" target="_blank">What does horizontal scaling mean?</a>
2. <a href="https://blog.openshift.com/best-practices-for-horizontal-application-scaling/" target="_blank">Best Practices For Horizontal Application Scaling</a>
3. <a href="http://www.infoq.com/articles/ebay-scalability-best-practices" target="_blank">Scalability Best Practices: Lessons from eBay</a>
4. <a href="http://stackoverflow.com/questions/5401992/what-does-scale-horizontally-and-scale-vertically-mean" target="_blank">What does scale horizontally and scale vertically mean?</a>

