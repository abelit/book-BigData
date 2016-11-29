
# Apache Hbase

## 1. About Apache Hbase
A scalable, distributed database that supports structured data storage for large tables

[Apache HBase™ ](http://hbase.apache.org/)is the Hadoop database, a distributed, scalable, big data store.

Use Apache HBase™ when you need random, realtime read/write access to your Big Data. This project's goal is the hosting of very large tables -- billions of rows X millions of columns -- atop clusters of commodity hardware. Apache HBase is an open-source, distributed, versioned, non-relational database modeled after Google's Bigtable: A Distributed Storage System for Structured Data by Chang et al. Just as Bigtable leverages the distributed data storage provided by the Google File System, Apache HBase provides Bigtable-like capabilities on top of Hadoop and HDFS.

[Apache HBase:](http://blog.fens.me/hadoop-family-roadmap/) 是一个高可靠性、高性能、面向列、可伸缩的分布式存储系统，利用HBase技术可在廉价PC Server上搭建起大规模结构化存储集群。


## 2. Apache Hbase Installation
### 2.1 Download Hbase
Download from [http://hbase.apache.org](http://hbase.apache.org/).
> wget http://mirrors.hust.edu.cn/apache/hbase/1.2.4/hbase-1.2.4-bin.tar.gz

### 2.2 Unpack to target folder
> tar -zxvf hbase-1.2.4-bin.tar.gz

### 2.3 Edit ```~/.bashrc``` and add following contents

```
# Hbase Environment
export HBASE_HOME=/home/hadoop/hbase-1.2.4
export HBASE_CONF_DIR=${HBASE_HOME}/conf
export PATH=$PATH:${HBASE_HOME}/bin
```

### 2.4 Edit ```$HBASE_CONF_DIR/hbase-env.sh``` and add following contents

```
export JAVA_HOME=/home/hadoop/jdk1.8.0_112
export HBASE_CLASSPATH=/home/hadoop/hadoop-2.7.3/conf
export HBASE_LOG_DIR=${HBASE_HOME}/logs
export HBASE_MANAGES_ZK=false
```

### 2.5 Edit ```$HBASE_CONF_DIR/hbase-site.xml```

```
<configuration>
    <property>
        <name>hbase.rootdir</name>
        <value>hdfs://master:9000/hbase</value>
    </property>
    <property>
        <name>hbase.cluster.distributed</name>
        <value>true</value>
    </property>
    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>master,node1,node2</value>
    </property>
</configuration>
```

### 2.6 Edit ```$HBASE_CONF_DIR/regionservers
```
node1
node2
```

### 2.7 Put hbase and ```.bashrc``` to the other nodes
> scp -r hbase-1.2.4 hadoop@node1:.
>
> scp -r hbase-1.2.4 hadoop@node2:.
> 
> scp -r .bashrc hadoop@node1:.
>
> scp -r .bashrc hadoop@node2:.

### 2.8 Manage Hbase Service
* Startup service
> $start-hbase.sh

* Stop service 
> $stop-hbase.sh

### 2.9 Run Hbase
> $hbase shell

## 3. Usage of Apache Hbase
