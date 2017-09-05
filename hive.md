* # Apache Hive

## 1. About Apache Hive

A data warehouse infrastructure that provides data summarization and ad hoc querying.The [Apache Hive ™ ](http://hive.apache.org/)data warehouse software facilitates reading, writing, and managing large datasets residing in distributed storage using SQL. Structure can be projected onto data already in storage. A command line tool and JDBC driver are provided to connect users to Hive.

[Apache Hive:](http://blog.fens.me/hadoop-family-roadmap/) 是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，通过类SQL语句快速实现简单的MapReduce统计，不必开发专门的MapReduce应用，十分适合数据仓库的统计分析。

## 2. Apache Hive Installation

### 2.1 Download Hive

Download from [http://hive.apache.org](http://hive.apache.org).

> wget [http://mirrors.hust.edu.cn/apache/hive/hive-2.1.0/apache-hive-2.1.0-bin.tar.gz](http://mirrors.hust.edu.cn/apache/hive/hive-2.1.0/apache-hive-2.1.0-bin.tar.gz)

### 2.2 Unpack to target folder

> tar -zxvf apache-hive-2.1.0-bin.tar.gz

### 2.3 Edit ~/.bashrc and add following contents

```
# Hive Environment
export HIVE_HOME=/home/hadoop/apache-hive-2.1.0-bin
export HIVE_CONF_DIR=${HIVE_HOME}/conf
export PATH=$PATH:${HIVE_HOME}/bin
```

### 2.4 Edit `hive-env.sh`

```
export HIVE_CONF_DIR=/home/hadoop/apache-hive-2.1.0-bin/conf
HADOOP_HOME=/home/hadoop/hadoop-2.7.3
```

### 2.4 Edit `hive-site.xml`

* Configure `hive-site.xml`  based derby.

```
<configuration>
    <property>
        <name>hive.metastore.uris</name>
        <value>thrift://master:9083</value>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionURL</name>
        <value>jdbc:derby:;databaseName=metastore_db;create=true</value>
        <description>JDBC connect string for a JDBC metastore</description>
    </property>

    <property>
        <name>javax.jdo.option.ConnectionDriverName</name>
        <value>org.apache.derby.jdbc.EmbeddedDriver</value>
        <description>Driver class name for a JDBC metastore</description>
    </property>
        <property>
        <name>javax.jdo.option.ConnectionUserName</name>
        <value>APP</value>
        <description>username to use against metastore database</description>
    </property>

    <property>
        <name>javax.jdo.option.ConnectionPassword</name>
        <value>mine</value>
        <description>password to use against metastore database</description>
    </property>
</configuration>
```

* Configure `hive-site.xml`  based on mysql.

```
<configuration>
    <property>  
        <name>hive.metastore.uris</name>  
        <value>thrift://master:9083</value>  
    </property>
    <property>   
        <name>datanucleus.fixedDatastore</name>   
        <value>false</value>   
    </property>
    <!-- metadata database connection configuration -->
    <property>
        <name>javax.jdo.option.ConnectionURL</name>
        <value>jdbc:mysql://master:3306/hive?useUnicode=true&characterEncoding=UTF-8&createDatabaseIfNotExist=true</value>
        <description>JDBC connect string for a JDBC metastore</description>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionDriverName</name>
        <value>com.mysql.jdbc.Driver</value>
        <description>Driver class name for a JDBC metastore</description>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionUserName</name>
        <value>hive</value>
        <description>username to use against metastore database</description>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionPassword</name>
        <value>hive</value>
        <description>password to use against metastore database</description>
    </property>

    <property>
        <name>hive.hwi.listen.host</name>
        <value>master</value>
        <description>This is the host address the Hive Web Interface will listen on</description>
    </property>
    <property>
        <name>hive.hwi.listen.port</name>
        <value>9999</value>
        <description>This is the port the Hive Web Interface will listen on</description>
    </property>
</configuration>
```

### Note:

If you configure hive based on mysql,please make sure that install mysql-server and creating database for storing hive metastore data.

* Install MySQL\(Ubuntu\)

  > sudo apt-get install mysql-server mysql-client

* Login MySQL and Create database

  > mysql -u root -p

```
create user 'hive'@'%' identified by 'hive';
grant all on hive.* to hive@'%'  identified by 'hive';  
flush privileges;
```

> mysql -uhive -p

`create database hive;`

* Download MySQL JDBC Driver to $HIVE\_HOME/lib
  > wget [http://cdn.mysql.com/Downloads/Connector-J/mysql-connector-java-5.1.36.tar.gz](http://cdn.mysql.com/Downloads/Connector-J/mysql-connector-java-5.1.36.tar.gz)

### 2.6 Run Hive

* Initial hive database metastore based on derby.

  > schematool -initSchema -dbType derby

* Initial hive database metastore based on mysql.

  > schematool -initSchema -dbType mysql

* Startup metastore service using following cmd or `hive --service metastore &`

  > $nohup hive --service metastore &gt;hive\_metastore.run.log 2&gt;&1 &

* Run hive

  > $hive

## 3. Usage of Apache Hive

### 3.1 Basic Command

* List all databases

  > hive&gt; show databases;

* Create tables

  > hive&gt; create table users\(id int, name string, email string\);

* List all tables

  > hive&gt; show tables;

* Insert data to the table

  > hive&gt; insert into users values\(1,'abelit','ychenid@live.com'\);

* Query data

  > hive&gt; select \* from users;

* Query file's contents on the hdfs

  > hive&gt; bin/hadoop dfs -cat /user/hive/warehouse/users/000000\_0

### 3.2 Load data to hive

* Load local data to hive

```
hive> create table a_qyzt (nbxh string,qymc string,qylx string, djjg string) row format delimited fields terminated by ',' stored as textfile;
hive> load data local inpath './export.csv' into table a_qyzt;
hive> select count(\*) from a_qyzt where djjg like '520101%';
hive> select djjg,count(*) from a_qyzt group by djjg;
```

* Load hdfs data to hive

  > hive&gt; load data inpath '/input/export.csv' into table a_qyzt;

* Insert data to hive from other table

  > hive&gt; create table a_qyzt_new (nbxh string,qymc string,qylx string, djjg string) row format delimited fields terminated by ',' stored as textfile;
  
  > hive&gt; insert overwrite table a_qyzt_new select nbxh,qymc,qylc,djjg from a_qyzt;
