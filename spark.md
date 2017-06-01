# Apache Spark

## 1. About Apache Spark

A fast and general compute engine for Hadoop data. Spark provides a simple and expressive programming model that supports a wide range of applications, including ETL, machine learning, stream processing, and graph computation.

## 2. Apache Spark Installation

### 2.1 Download Apache Spark

* Download spark from [http://spark.apache.org](http://spark.apache.org/)
> wget [http://mirrors.hust.edu.cn/apache/spark/spark-2.0.2/spark-2.0.2-bin-hadoop2.7.tgz](http://mirrors.hust.edu.cn/apache/spark/spark-2.0.2/spark-2.0.2-bin-hadoop2.7.tgz)

### 2.2 Unpack to target folder
* 
> tar -zxvf spark-2.0.2-bin-hadoop2.7.tgz

### 2.3 Edit `~/.bashrc` and add following contents

* .bashrc
```
# Spark Environment
export SPARK_HOME=/home/hadoop/spark-2.0.2-bin-hadoop2.7
export SPARK_CONF_DIR=${SPARK_HOME}/conf
export PATH=$PATH:${SPARK_HOME}/bin:${SPARK_HOME}/sbin
```

### 2.4 Edit `spark-env.sh`

* spark-env.sh
  ```
  export JAVA_HOME=/home/hadoop/jdk1.8.0_112
  export SCALA_HOME=/home/hadoop/scala-2.11.8
  export HADOOP_HOME=/home/hadoop/hadoop-2.7.3
  export HADOOP_CON_DIR=${HADOOP_HOME}/etc/hadoop
  export SPARK_MASTER_IP=master
  export SPARK_WORKER_MEMORY=256m
  ```

### 2.5 Edit `spark-defaults.conf`

* spark-defaults.conf


### 2.6 Edit `slaves`

* slaves
  ```
  node1
  node2
  ```

### 2.7 Put hadoop and `.bashrc` to the other nodes

> scp -r spark-2.0.2-bin-hadoop2.7 hadoop@node1:.
>
> scp -r spark-2.0.2-bin-hadoop2.7 hadoop@node2:.
>
> scp  .bashrc hadoop@node1:.
>
> scp  .bashrc hadoop@node2:.

### 2.8 Manage Spark service

* Startup service

  > $SPARK\_HOME/sbin/start-all.sh

* Query spark status

  > jps

* Query spark service by web-ui

```
http://master:8080
```

## 3. Usage of Apache Spark
