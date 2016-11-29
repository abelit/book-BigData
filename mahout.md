# Apache Mahout

## 1. About Apache Mahout
A Scalable machine learning and data mining library. The Apache Mahout™ project's goal is to build an environment for quickly creating scalable performant machine learning applications. 

[Apache Mahout software](http://mahout.apache.org/) provides three major features:

* A simple and extensible programming environment and framework for building scalable algorithms
* A wide variety of premade algorithms for Scala + Apache Spark, H2O, Apache Flink
* Samsara, a vector math experimentation environment with R-like syntax which works at scale

[Apache Mahout:](http://blog.fens.me/hadoop-family-roadmap/)是基于Hadoop的机器学习和数据挖掘的一个分布式框架。Mahout用MapReduce实现了部分数据挖掘算法，解决了并行挖掘的问题。


## 2. Apache Mahout Installation
### 2.1 Download Mahout
Download from [http://mahout.apache.org](http://mahout.apache.org).
> wget http://mirrors.hust.edu.cn/apache/mahout/0.12.2/apache-mahout-distribution-0.12.2.tar.gz

### 2.2 Unpack to target folder
> tar -zxvf apache-mahout-distribution-0.12.2.tar.gz

### 2.3 Edit ~/.bashrc and add following contents

```
# Mahout Environment
export MAHOUT_HOME=/home/hadoop/apache-mahout-distribution-0.12.2
export MAHOUT_CONF_DIR=${MAHOUT_HOME}/conf
export PATH=$PATH:${MAHOUT_HOME}/bin
```

### 2.4 Run Mahout

When running ```mahout``` on the shell,it will list all algorithm of mahout and that means you have installed and configured mahout successfully.

> $mahout

## 3. Usage of Apache Mahout

### 3.1 Kmeans Method

* Download  testing data
> axel http://archive.ics.uci.edu/ml/databases/synthetic_control/synthetic_control.data

* Put testing data to hdfs
> hadoop fs -mkdir /input/testdata
> hadoop fs -put synthetic_control.data /input/testdata

* Run it using kmeans method
> hadoop jar apache-mahout-distribution-0.12.2/mahout-examples-0.12.2-job.jar org.apache.mahout.clustering.syntheticcontrol.kmeans.Job

* Show the results
> hadoop fs -ls output