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

<p class="music-read"><a href="https://y.qq.com/n/yqq/song/434676_num.html?ADTAG=h5_playsong&no_redirect=1">Music for reading</a></p>

<img src="/land-ml/assets/img/header/python-env-best-prictise.png">

## 一、重建 macOS python

macOS Sierra 自带的版本是 Python2，通常位于 `/usr/bin/python`, 即便是 root 权限，也无法删除。当然，由于诸多系统软件依赖 Python2，也不建议删除。

python 允许多版本共存，并且目前 python 有众多包管理利器，诸如：celler、pip，aconda 等。

为了更好地管理 python 环境，我们先把其他各个渠道的 python 版本，统统删掉(通常位于 `/usr/local/bin`)。

以 python2.7 为例，具体步骤：

**1. 删除 Python 2.7 Framework**

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

**2. 清除软链接**

{% highlight shell %}
➜cd /usr/local/bin/python
➜ls -al | grep "python"
➜sudo rm -rf xxx
{% endhighlight %}

**3. 清除 相关 profile files 中的 `PATH` 等环境变量。**


## 二、安装 Anaconda

### 1. Anaconda 是什么？

<p>     Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.</p>

<p>     Additionally, you'll have access to over 720 packages that can easily be installed with conda, our renowned package, dependency and environment manager, that is included in Anaconda. See the packages included with Anaconda and the Anaconda changelog。</p>

<a href="https://www.continuum.io/" target="_blank">Anaconda</a> 其实用于科学计算的 Python 发行版(不仅限于 Python)，集成了100多个科学计算包及其依赖。

### 2. Conda
Anaconda 集成了 Conda,  Conda 解决了Python的不同版本隔离（环境管理）和包管理。

#### 环境管理




## 参考
1. <a href="http://stackoverflow.com/questions/3819449/how-to-uninstall-python-2-7-on-a-mac-os-x-10-6-4" target="_blank">How to uninstall Python 2.7 on a Mac OS X 10.6.4?</a>
