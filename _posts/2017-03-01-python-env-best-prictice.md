---
layout: post
title:  "Python环境搭建最佳实践"
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

## 本文核心：

一、重建 macOS python
二、Anaconda 管理 envs & packages
三、Spark 环境搭建


## 一、重建 macOS python

macOS Sierra 自带的版本是 Python2，通常位于 `/usr/bin/python`, 即便是 root 权限，也无法删除。当然，由于诸多系统软件依赖 Python2，也不建议删除。

python 允许多版本共存，并且目前 python 有众多包管理利器，诸如：celler、pip，aconda 等。

为了更好地管理 python 环境，我们先把其他各个渠道的 python 版本，统统删掉(通常位于 `/usr/local/bin`)。

以 python2.7 为例，具体步骤：

**1.删除 Python 2.7 Framework**

```shell
➜ where python
/usr/bin/python
/usr/local/bin/python
```

确定删除 `/usr/local/bin/python`。进入 `/usr/local/bin`，确定真身。

```shell
➜ls -al | grep "python"
lrwxr-xr-x  1 root       wheel    35B 12  7 10:28 2to3-2 -> ../Cellar/python/2.7.6_1/bin/2to3-2
lrwxr-xr-x  1 root       wheel    37B 12  7 10:28 2to3-2.7 -> ../Cellar/python/2.7.6_1/bin/2to3-2.7
lrwxr-xr-x  1 root       wheel    41B 12  7 10:28 easy_install -> ../Cellar/python/2.7.6_1/bin/easy_install
lrwxr-xr-x  1 root       wheel    45B 12  7 10:28 easy_install-2.7 -> ../Cellar/python/2.7.6_1/bin/easy_install-2.7
```

原来，位于 `../Cellar/python`, 删除之。

``` shell
➜sudo rm -rf "../Cellar/python/"
```

**2.清除软链接**

```shell
➜cd /usr/local/bin/python
➜ls -al | grep "python"
➜sudo rm -rf xxx
```

**3.清除 相关 profile files 中的 `PATH` 等环境变量。**


## 二、安装 Anaconda

### Anaconda 是什么？

<p>     Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.</p>

<p>     Additionally, you'll have access to over 720 packages that can easily be installed with conda, our renowned package, dependency and environment manager, that is included in Anaconda. See the packages included with Anaconda and the Anaconda changelog。</p>

<a href="https://www.continuum.io/" target="_blank">Anaconda</a> 其实用于科学计算的 Python 发行版(不仅限于 Python)，集成了100多个科学计算包及其依赖。

### Conda
Anaconda 集成了 Conda,  Conda 解决了Python的不同版本隔离（环境管理）和包管理。

#### 环境管理

```shell
# 创建 python27 的环境，conda 自动搜索2.7最新版本
conda create --name python27 python=2.7

# 激活 python27 环境
source activate python27
变成: 
(python27) ➜  ~ 

# 回复默认环境
source deactivate python27

# 删除环境
conda remove --name python27 --all

# 查看已有环境
conda info -e

# conda environments:
#
python27                 /Users/fandennis/anaconda/envs/python27
root                  *  /Users/fandennis/anaconda
```

可以看出安装的 env 都放在 `~/anaconda/envs` 路径下。

#### 包管理

```shell
# conda 远程搜索 pip 信息与依赖
conda install pip

# 安装 package
conda install -n python27 pip

# 安装 anaconda package sets
conda install anaconda

# 创建是安装 anaconda package sets
conda create -n python27 python=2.7 anaconda

# 更新package
conda update -n python27 pip

# 删除package
conda remove -n python27 pip

# 查找package信息
conda search pip

# 查看已安装 packages
conda list

# 查看指定环境已安装 package
conda list -n python27
```

值得注意的是，conda 将 python、conda 本身看成 package，及其方便管理。

#### 添加镜像

``` shell
# 添加 Anaconda 镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

# 显示通道地址
conda config --set show_channel_urls yes
```

可以在 `anaconda` 查看


<figure class="foto-legenda">
    <img src="{{ "/land-ml/assets/img/python/python-env-best-prictice/anaconda-config.png"}}" alt="">
    <figcaption> <p>aconda 可视化配置</p>
    </figcaption>
</figure>


to be continued...


## 参考
1. <a href="http://stackoverflow.com/questions/3819449/how-to-uninstall-python-2-7-on-a-mac-os-x-10-6-4" target="_blank">How to uninstall Python 2.7 on a Mac OS X 10.6.4?</a>
