# Apache Sqoop

## 1. About Apache Sqoop
Apache Sqoop(TM) is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases.
=======
## About Apache Sqoop
[Apache Sqoop(TM)](http://sqoop.apache.org/) is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases.

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
export SQOOP_CONF_DIR=${SQOOP_HOME}/conf
export PATH=$PATH:${SQOOP_HOME}/bin
```
### Note:
* Download MySQL JDBC Driver to $SQOOP_HOME/tools/lib
> wget http://cdn.mysql.com/Downloads/Connector-J/mysql-connector-java-5.1.36.tar.gz

### 2.4 Edit ```$HADOOP_CONF_DIR/core-site.xml``` and add following contents

```
<property>
  	<name>hadoop.proxyuser.hadoop.hosts</name>
  	<value>*</value>
</property>
<property>
  	<name>hadoop.proxyuser.hadoop.groups</name>
  	<value>*</value>
</property>
```

### 2.5 Edit ```$SQOOP_CONF_DIR/sqoop_bootstrap.properties```

```
sqoop.config.provider=org.apache.sqoop.core.PropertiesConfigurationProvider 
```

### 2.6 Edit ```$SQOOP_CONF_DIR/sqoop.properties```
```
org.apache.sqoop.submission.engine.mapreduce.configuration.directory=/home/hadoop/hadoop-2.7.3/etc/hadoop  
org.apache.sqoop.security.authentication.type=SIMPLE  
org.apache.sqoop.security.authentication.handler=org.apache.sqoop.security.authentication.SimpleAuthenticationHandler  
org.apache.sqoop.security.authentication.anonymous=true  
```

### 2.7 Put sqoop and ```.bashrc``` to the other nodes
> scp -r sqoop-1.99.7 hadoop@node1:.
>
> scp -r sqoop-1.99.7 hadoop@node2:.
> 
> scp -r .bashrc hadoop@node1:.
>
> scp -r .bashrc hadoop@node2:.

### 2.8 Manage Sqoop Service
* Verify sqoop
> sqoop2-tool verify 

* Startup service
> $sqoop2-server start

* Stop service 
> $sqoop2-server stop

## 3. Usage of Apache Sqoop

