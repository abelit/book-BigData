# Hadoop

## 1. About Hadoop

#### What Is Apache Hadoop?

The[ Apache™ Hadoop®](http://hadoop.apache.org/) project develops open-source software for reliable, scalable, distributed computing.

The Apache Hadoop software library is a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage. Rather than rely on hardware to deliver high-availability, the library itself is designed to detect and handle failures at the application layer, so delivering a highly-available service on top of a cluster of computers, each of which may be prone to failures.

The project includes these modules:

* Hadoop Common: The common utilities that support the other Hadoop modules.
* Hadoop Distributed File System \(HDFS™\): A distributed file system that provides high-throughput access to application data.
* Hadoop YARN: A framework for job scheduling and cluster resource management.
* Hadoop MapReduce: A YARN-based system for parallel processing of large data sets.

[Apache Hadoop:](http://blog.fens.me/hadoop-family-roadmap/) 是Apache开源组织的一个分布式计算开源框架，提供了一个分布式文件系统子项目\(HDFS\)和支持MapReduce分布式计算的软件架构。

## 2. Hadoop Installation

### 2.1 Download Hadoop

* Download from [http://hadoop.apache.org](http://hadoop.apache.org/)
  > wget [http://mirrors.hust.edu.cn/apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz](http://mirrors.hust.edu.cn/apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz)

### 2.2 Unpack to target folder

> tar -zxvf hadoop-2.7.3.tar.gz

### 2.3 Edit `~/.bashrc` and add following contents

```
# Hadoop Environment
export HADOOP_HOME=/home/hadoop/hadoop-2.7.3
export HADOOP_MAPRED_HOME=${HADOOP_HOME}
export HADOOP_COMMON_HOME=${HADOOP_HOME}
export HADOOP_HDFS_HOME=${HADOOP_HOME}
export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop
export HDFS_CONF_DIR=${HADOOP_HOME}/etc/hadoop
export YARN_HOME=${HADOOP_HOME}
export YARN_CONF_DIR=${HADOOP_HOME}/etc/hadoop
export PATH=$PATH:${HADOOP_HOME}/bin:${HADOOP_HOME}/sbin
```

### 2.4 Edit `hadoop-env.sh, mapred-env.sh, yarn-env.sh`

* hadoop-env.sh

  ```
  export JAVA_HOME=/home/hadoop/jdk1.8.0_112
  ```

* mapred-env.sh

  ```
  export JAVA_HOME=/home/hadoop/jdk1.8.0_112
  ```

* yarn-env.sh

  ```
  export JAVA_HOME=/home/hadoop/jdk1.8.0_112
  ```

### 2.5 Edit `core-site.xml, hdfs-site.xml, mapred-site.xml, yarn-site.xml`

* core-site.xml

  ```
  <configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://master:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>file:/home/hadoop/hadoop-2.7.3/tmp</value>
    </property>
  </configuration>
  ```

* hdfs-site.xml

  ```
  <configuration>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>master:9001</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/home/hadoop/hadoop-2.7.3/hdfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/hadoop/hadoop-2.7.3/hdfs/data</value>
    </property>
  </configuration>
  ```

* mapred-site.xml

  ```
  <configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>master:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>master:19888</value>
    </property>
  </configuration>
  ```

* yarn-site.xml

  ```
  <configuration>
  <!-- Site specific YARN configuration properties -->
  <!--
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>master</value>
    </property>
  -->
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
    <property>
        <name>yarn.resourcemanager.address</name>
        <value>master:8032</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>master:8030</value>
    </property>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>master:8031</value>
    </property>
    <property>
        <name>yarn.resourcemanager.admin.address</name>
        <value>master:8033</value>
    </property>
  <!--
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>master:8088</value>
    </property>
  -->
  </configuration>
  ```

### 2.6 Edit slaves

* slaves
  ```
  node1
  node2
  ```

### 2.7 Put hadoop to the other nodes

> scp -r hadoop-2.7.3 hadoop@node1:.
>
> scp -r hadoop-2.7.3 hadoop@node2:.
>
> scp -r .bashrc hadoop@node1:.
>
> scp -r .bashrc hadoop@node2:.

### 2.8 Formart namenode

> hdfs namenode -format

### 2.9 Manage hadoop service

* Startup service

  > $HADOOP\_HOME/sbin/start-all.sh

* Query hadoop status

  > jps

* Query hadoop service by web-ui

```
http://master:50070
http://master:8088
```

## 3. Usage of Hadoop

### 3.1 Basic Operation

* List hfs directory
* > bin/hadoop dfs -ls /



