# Apache Sqoop

<<<<<<< HEAD
## 1. About Apache Sqoop
Apache Sqoop(TM) is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases.
=======
## About Apache Sqoop
[Apache Sqoop(TM)](http://sqoop.apache.org/) is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases.
>>>>>>> 390f050218cb97de266a277c7f45f124d97df634

[Apache Sqoop:](http://blog.fens.me/hadoop-family-roadmap/) 是一个用来将Hadoop和关系型数据库中的数据相互转移的工具，可以将一个关系型数据库（MySQL ,Oracle ,Postgres等）中的数据导进到Hadoop的HDFS中，也可以将HDFS的数据导进到关系型数据库中。

## 2. Apache Sqoop Installation
### 2.1 Download Sqoop
Download from [http://sqoop.apache.org](http://sqoop.apache.org/).
> wget http://mirrors.hust.edu.cn/apache/sqoop/1.99.7/sqoop-1.99.7.tar.gz

### 2.2 Unpack to target folder
> tar -zxvf sqoop-1.99.7.tar.gz

### 2.3 Edit ```~/.bashrc``` and add following contents

```
# Hbase Environment
export SQOOP_HOME=/home/hadoop/sqoop-1.99.7
export PATH=$PATH:${SQOOP_HOME}/bin
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

