# Apache ZooKeeper
## 1. About Apache ZooKeeper

A high-performance coordination service for distributed applications.

[ZooKeeper](http://zookeeper.apache.org/) is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these kinds of services are used in some form or another by distributed applications. Each time they are implemented there is a lot of work that goes into fixing the bugs and race conditions that are inevitable. Because of the difficulty of implementing these kinds of services, applications initially usually skimp on them ,which make them brittle in the presence of change and difficult to manage. Even when done correctly, different implementations of these services lead to management complexity when the applications are deployed.

[Apache Zookeeper:](http://blog.fens.me/hadoop-family-roadmap/) 是一个为分布式应用所设计的分布的、开源的协调服务，它主要是用来解决分布式应用中经常遇到的一些数据管理问题，简化分布式应用协调及其管理的难度，提供高性能的分布式服务.

## 2. Apache Zookeeper Installation
### 2.1 Download ZooKeeper
Download from [http://zookeeper.apache.org/](http://zookeeper.apache.org/).
> wget http://mirrors.hust.edu.cn/apache/zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz

### 2.2 Unpack to target folder
> tar -zxvf zookeeper-3.4.9.tar.gz

### 2.3 Edit ~/.bashrc and add following contents

```
# Zookeeper Envirionment
export ZK_HOME=/home/hadoop/zookeeper-3.4.9
export ZK_CONF_DIR=${ZK_HOME}/conf
export PATH=$PATH:${ZK_HOME}/bin
```

###2.4 Edit $ZK_CONF_DIR/conf/zoo.cfg
```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
#dataDir=/tmp/zookeeper
dataDir=/home/hadoop/zookeeper-3.4.9/data
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
server.1=master:2888:3888
server.2=node1:2888:3888
server.3=node2:2888:3888
```
* Make dataDir and Touch myid
> mkdir $ZK_HOME/data
> 
> echo 1 > $ZK_HOME/data/myid


### 2.5 Put ```zookeeper-3.4.9``` to the other nodes and edit ```$ZK_HOME/conf/data/myid```
> scp -r zookeeper-3.4.9 hadoop@node1:.
>
> scp -r zookeeper-3.4.9 hadoop@node2:.

### 2.6 Put ```.bashrc``` to the other nodes
> scp -r ~/.bashrc hadoop@node1:.
>
> scp -r ~/.bashrc hadoop@node2:.

### 2.7 Manage ZooKeeper Service on all nodes
* Startup service
> zkServer.sh start

* Query status of service 
> zkServer.sh status

* Close service
> zkServer.sh stop

#### Note:
