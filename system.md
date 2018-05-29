[TOC]

# 分布式系统

## ELK stack
[elasticsearch](https://www.elastic.co/cn/products/elasticsearch)+[logstash](https://www.elastic.co/cn/products/logstash)+[kibana](https://www.elastic.co/cn/products/kibana)

### elasticstash
* 是一个分布式的RESTful风格的搜索和数据分析引擎，封装了Lucene。
* 允许执行和合并多种类型的搜索——结构化、非结构化、地理位置、度量指标——搜索方式随心而变。
* 可在笔记本电脑上运行也可以在承载了PB级数据的成百上千台服务器上运行。
* 运行在一个分布式环境中，从设计初考虑到了硬件故障，网络瞬断问题。
* 客户端支持的语言：Curl, Java, C#, Python, JavaScript, PHP, Perl, Ruby。

### logstash
* 开源的服务器端数据处理管道，能够同时从多个来源采集数据、转换数据，然后将数据发送到存储库中。
![logstash-diagram-6](D:\terry\notes\images\system\logstash-diagram-6.png)

### kibana
* 可视化Elasticsearch中的数据并操作Elastic stack。
* 支持柱状图、线状图、饼图、环形图等等。他们充分利用了Elasticsearch的聚合功能。

### X-PACK插件
* 为集群添加身份认证，监控Elasticsearch是如何运行的，通过运行机器学习的任务来发现异常等等。X-Pack提供的特性包括security、monitoring、alerting、reporting、graph关联分析和machine learning。

###  Elasticsearch加Hadoop
* 可以使用Elasticsearch-Hadoop(ES-hadoop)连接器，利用Elasticsearch的实时搜索和分析功能处理大数据。

### Elasticsearch加其它数据库
* Elasticsearch有自己的nosql类型的数据库，也可以与其它数据库一起使用。
* 通过logstash的插件：logstash-input-jdbc；需要使用的数据库找到相应的jdbc driver，比如mysql，使用mysql connector，mongo使用mongo-connector。

## Hadoop

### Hadoop
* Hadoop实现了一个分布式文件系统（Hadoop Distributed File System），简称HDFS。
* HDFS有高容错性的特点，并且设计用来部署在低廉的（low-cost）硬件上；而且它提供高吞吐量（high throughput）来访问应用程序的数据，适合那些有着超大数据集的应用程序。HDFS放宽了POSIX的要求，可以以流的形式访问（streaming access）文件系统中的数据。
* Hadoop的框架核心设计是：HDFS和MapReduce。HDFS为海量的数据提供了存储，MapReduce为海量的数据提供了计算。

Hadoop解决哪些问题？
	*  海量数据需要及时分析和处理
	*  海量数据需要深入分析和挖掘
	*  数据需要长期保存

海量数据存储的问题：
	* 磁盘IO成为瓶颈，而非CPU资源
	* 网络带宽是一种稀缺资源
	* 硬件故障成为影响稳定的一大因素

### Hadoop相关技术
![hadoop](D:\terry\notes\images\system\hadoop.png)

#### Hbase
* Nosql数据库，key-value存储
* 最大化利用内存

#### HDFS
* Hadoop distribute file system（分布式文件系统）
* 最大化利用磁盘

#### MapReduce
* 编程模型，并行计算框架，主要用来做数据分析
* 最大化利用CPU

#### Hive
* 数据仓库工具

#### Zookeeper
* 分布式锁设施，提供类似Google chubby的功能

#### Avro
* 新的数据序列化格式与传输工具，将逐步取代Hadoop原有的IPC机制。

#### Pig
* 大数据分析平台

#### Ambari
* Hadoop管理工具，可以快捷的监控、部署、管理集群。

#### sqoop
* Hadoop与传统的数据库间进行数据的传递。


# 数据库

## 数据库类型

### 关系型数据库遵循ACID规则
1. **A**（Atomicity）原子性

  原子性就是说事务里的所有操作要么全部做完，要么都不做，事务成功的条件是事务里的所有操作都成功，只要一个操作失败，整个事务就失败，需要回滚。
2. **C**（Consistency）一致性
    一致性就是说数据库要一直处于一致的状态，事务的运行不会改变数据库原本的一致性约束。
3. **I**（Isolation）独立性
    是指并发的事务之间不会互相影响，如果一个事务要访问的数据正在被另外一个事务修改，只要另外一个事务未提交，它所访问的数据就不受未提交事务的影响。
4. **D**（Durability）持久性
    是指一旦事务提交后，它所做的修改将会永久的保存在数据库上，即使出现宕机也不会丢失。

### 分布式系统
分布式系统（distributed system）由多台计算机和通信的软件通过计算机网络连接（本地网络或广域网）组成。分布式系统是建立在网络之上的软件系统。正是因为软件的特性，所以分布式系统具有高度的内聚性和透明性。
因此，网络和分布式系统之间的区别更多的在于高层软件（特别是操作系统），而不是硬件。
分布式系统可以应用在不同的平台上如：PC、工作站、局域网和广域网上等。

### 分布式计算的优点
* 可靠性（容错） ：
分布式计算系统中的一个重要的优点是可靠性。一台服务器的系统崩溃并不影响到其余的服务器。
* 可扩展性：
在分布式计算系统可以根据需要增加更多的机器。
* 资源共享：
共享数据是必不可少的应用，如银行，预订系统。
* 灵活性：
由于该系统是非常灵活的，它很容易安装，实施和调试新的服务。
* 更快的速度：
分布式计算系统可以有多台计算机的计算能力，使得它比其他系统有更快的处理速度。
* 开放系统：
由于它是开放的系统，本地或者远程都可以访问到该服务。
* 更高的性能：
相较于集中式计算机网络集群可以提供更高的性能（及更好的性价比）。

### 分布式计算的缺点
* 故障排除：
故障排除和诊断问题。
* 软件：
更少的软件支持是分布式计算系统的主要缺点。
* 网络：
网络基础设施的问题，包括：传输问题，高负载，信息丢失等。
* 安全性：
开放系统的特性让分布式计算系统存在着数据的安全性和共享的风险等问题。

###  RDBMS vs NoSQL
* RDBMS
	* 高度组织化结构化数据 
	* 结构化查询语言（SQL） (SQL) 
	* 数据和关系都存储在单独的表中。 
	* 数据操纵语言，数据定义语言 
	* 严格的一致性
	* 基础事务
* NoSQL
	* 代表着不仅仅是SQL
	* 没有声明性查询语言
	* 没有预定义的模式
	* 键 - 值对存储，列存储，文档存储，图形数据库
	* 最终一致性，而非ACID属性
	* 非结构化和不可预知的数据
	* CAP定理 
	* 高性能，高可用性和可伸缩性

### CAP定理（CAP theorem）
在计算机科学中，CAP定理（CAP theorem），又被称作布鲁尔定理（Brewer’s theorem），它指出对于一个分布式计算系统来说，不可能同时满足以下三点：
* **一致性（Consistency）**（所有节点在同一时间具有相同的数据）
* **可用性（Availability）**（保证每个请求不管成功或者失败都有响应）
* **分隔容忍（Partition tolerance）**（系统中任意信息的丢失或失败不会影响系统的继续运作）
CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，最多只能同时较好的满足两个。
因此，根据CAP原理将NoSQL数据库分成了满足CA原则、满足CP原则和满足AP原则三大类：
* CA-单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大。
* CP-满足一致性，分区容忍性的系统，通常性能不是特别高。
* AP-满足可用性，分区容忍性的系统，通常可能对一致性要求低一些。
![cap-theoram-image](D:\terry\notes\images\system\cap-theoram-image.png)

### NoSQL的优点/缺点
* 优点：
	* 高可扩展性
	* 分布式计算
	* 低成本
	* 架构的灵活性，半结构化数据
	* 没有复杂的关系 
* 缺点：
	* 没有标准化
	* 有限的查询功能（到目前为止）
	* 最终一致是不直观的程序

### BASE
BASE：Basically Available，Soft-state，Eventually Consistent。由Eric Brewer定义。
CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，最多只能同时较好的满足两个。
BASE是NoSQL数据库通常对可用性及一致性的弱要求原则：
* Basically Available -- 基本可用
* Soft-state -- 软状态/柔性事务。“Soft state”可以理解为“无连接”的，而“Hard state”是“面向连接”的。
* Eventual Consistency -- 最终一致性，也是ACID的最终目的。

### ACID vs BASE
| ACID                      | BASE                                    |
| ------------------------- | --------------------------------------- |
| 原子性（**A**tomicity）   | 基本可用（**B**asically **A**vailable） |
| 一致性（**C**onsistency） | 软状态/柔性事务（**S**oft state）       |
| 隔离性（**I**solation）   | 最终一致性（**E**ventual consistency）  |
| 持久性（**D**urable）     |                                         |

### NoSQL数据库分类
| 类型          | 部分代表                                                     | 特点                                                         |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 列存储        | Hbase<br />Cassandra<br />Hypertable                         | 顾名思义，是按列存储数据的。最大的特点是方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的IO优势"。 |
| 文档存储      | MongoDB<br />CouchDB                                         | 文档存储一般用类似json的格式存储，存储的内容是文档型的。这样也就有机会对某些字段建立索引，实现关系数据库的某些功能。 |
| Key-value存储 | Tokyo Cabinet/Tyrant<br />Berkeley DB<br />MemcacheDB<br />Redis | 可以通过key快速查询到其value。一般来说，存储不管value的格式，照单全收。（Redis包含了其他功能）。 |
| 图存储        | Neo4J<br />FlockDB                                           | 图形关系的最佳存储。使用传统关系数据库来解决的话性能低下，而且设计使用不方便。 |
| 对象存储      | db4o<br />Versant                                            | 通过类似面向对象语言的语法操作数据库，通过对象的方式存取数据。 |
| xml数据库     | Berkeley DB XML<br />BaseX                                   | 高效的存储XML数据，并支持XML的内部查询语法，比如XQuery，Xpath。 |

## MongoDB
* MongoDB是一个基于分布式文件存储的数据库。由C++语言编写。
* MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。

### MongoDB概念解析
| SQL术语/概念 | MongoDB术语/概念 | 说明                                 |
| ------------ | ---------------- | ------------------------------------ |
| database     | database         | 数据库                               |
| table        | collection       | 数据库表/集合                        |
| row          | document         | 数据记录行/文档                      |
| column       | field            | 数据字段/域                          |
| index        | index            | 索引                                 |
| table joins  |                  | 表连接，MongoDB不支持                |
| primary key  | primary key      | 主键，MongoDB自动将_id字段设置为主键 |

### MongoDB的复制
* 什么是复制
	* 保障数据的安全性
	* 数据高可用性（24*7）
	* 灾难恢复
	* 无需停机维护（如备份，重建索引，压缩）
	* 分布式读取数据

* 复制原理
	* MongoDB的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。
	* MongoDB各个节点常见的搭配方式为：一主一从、一主多从。
	* 主节点记录在其上的所有操作oplog，从节点定期轮询主节点获取这些操作，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致。
![mongodb-replication](D:\terry\notes\images\system\mongodb-replication.png)
以上结构图中，客户端从主节点读取数据，在客户端写入数据到主节点时，主节点与从节点进行数据交互保障数据的一致性。

副本集特征：
* N个节点的集群
* 任何节点可作为主节点
* 所有写入操作都在主节点上
* 自动故障转移
* 自动恢复

### MongoDB分片
在MongoDB里面存在另一种集群，就是分片技术，可以满足MongoDB数据量大量增长的需求。当MongoDB存储海量的数据时，一台机器可能不足以存储数据，也可能不足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。

* 为什么使用分片
	* 复制所有的写入操作到主节点
	* 延迟的敏感数据会在主节点查询
	* 单个副本集限制在12个节点
	* 当请求量巨大时会出现内存不足
	* 本地磁盘不足
	* 垂直扩展价格昂贵

* MongoDB分片
下图展示了在MongoDB中使用分片集群结构分布：
![mongodb-sharding](D:\terry\notes\images\system\mongodb-sharding.png)
上图中主要有如下所述三个主要组件：
	* Shard：
用于存储实际的数据块，实际生产环境中一个shard server角色可由几台机器组成一个replica set承担，防止主机单点故障
	* Config Server：
MongoDB实例，存储了整个ClusterMetadata，其中包括chunk信息。
	* Query Routers：
前端路由，客户端由此接入，且让整个集群看上去像单一数据库，前端应用可以透明使用。

### MongoDB备份（mongodump）与恢复（mongorestore）
* MongoDB数据备份
在MongoDB中我们使用mongodump命令来备份MongoDB数据。该命令可以导出所有数据到指定目录中。Mongodump命令可以通过参数指定导出的数据量级转存的服务器。
* MongoDB数据恢复
MongoDB使用mongorestore命令来恢复备份的数据。

### MongoDB监控
在你已经安装部署并允许MongoDB服务后，你必须要了解MongoDB的运行情况，并查看MongoDB的性能。这样在大流量的情况下可以很好的应对并保证MongoDB正常运作。
MongoDB中提供了mongostat和mongotop两个命令来监控MongoDB的运行情况。