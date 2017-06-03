# Apache Pig

## 1. About Apache Pig

[Apache Pig](http://pig.apache.org/) is a platform for analyzing large data sets that consists of a high-level language for expressing data analysis programs, coupled with infrastructure for evaluating these programs. The salient property of Pig programs is that their structure is amenable to substantial parallelization, which in turns enables them to handle very large data sets.

At the present time, Pig's infrastructure layer consists of a compiler that produces sequences of Map-Reduce programs, for which large-scale parallel implementations already exist \(e.g., the Hadoop subproject\). Pig's language layer currently consists of a textual language called Pig Latin, which has the following key properties:

* ** Ease of programming.** It is trivial to achieve parallel execution of simple, "embarrassingly parallel" data analysis tasks. Complex tasks comprised of multiple interrelated data transformations are explicitly encoded as data flow sequences, making them easy to write, understand, and maintain.

* **Optimization opportunities. **The way in which tasks are encoded permits the system to optimize their execution automatically, allowing the user to focus on semantics rather than efficiency.

* **Extensibility.** Users can create their own functions to do special-purpose processing.

[Apache Pig ](http://blog.fens.me/hadoop-family-roadmap/)是一个基于Hadoop的大规模数据分析工具，它提供的SQL-LIKE语言叫Pig Latin，该语言的编译器会把类SQL的数据分析请求转换为一系列经过优化处理的MapReduce运算。

## 2. Apache Pig Installation

### 2.1 Download Pig

Download from [http://pig.apache.org](http://pig.apache.org).

> wget [http://mirrors.hust.edu.cn/apache/pig/pig-0.16.0/pig-0.16.0.tar.gz](http://mirrors.hust.edu.cn/apache/pig/pig-0.16.0/pig-0.16.0.tar.gz)

### 2.2 Unpack to target folder

> tar -zxvf pig-0.16.0.tar.gz

### 2.3 Edit ~/.bashrc and add following contents

```
# Pig Environment
export PIG_HOME=/home/hadoop/pig-0.16.0
export PIG_CLASSPATH=${HADOOP_HOME}/etc/hadoop
export PATH=$PATH:${PIG_HOME}/bin
```

### 2.4 Run pig

When running pig witch will enter grunt shell like `grunt>`.Noting that you can run pig based on local mode using `pig -x local` and cluster mode using `pig` or `pig -x mapreduce`

> $pig

## 3. Usage of Apache Pig

### 3.1 Basic Command

* Show hdfs root directory `/input`

> ls /input

* Show file in the hdfs

> cat /input/README.md

### 3.2 Data Analysis

* WordCount

> grunt&gt;
>
> ```
> a = LOAD '/input/README.md' as (line:chararray);
> words = FOREACH a GENERATE flatten(TOKENIZE(line)) as w;
> g = GROUP words by w;
> wordcount = FOREACH g GENERATE group,COUNT(words);
> dump wordcount;
> ```

* wordcount2\(带词频倒排序\)

  ```
  a = LOAD '/input/README.md' as (line:chararray);
  words = FOREACH a GENERATE flatten(TOKENIZE(line)) as w;
  g = GROUP words by w;
  wordcount = FOREACH g GENERATE group,COUNT(words) as count;//给单词数所在列加一个别名count
  r = foreach wordcount generate count,group;//将结果列交换，将变成{count，word}这种结构
  g2 = group r by count;//按count分组
  x = foreach g2 generate group,r.group;//去掉无用的列
  y = order x by group desc;//按count倒排
  ```
