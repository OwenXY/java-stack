# Elasticsearch

## 目录

- [Elasticsearch核心知识入门篇](#Elasticsearch核心知识入门篇)
    - [Elasticsearch快速入门](#Elasticsearch快速入门)
      - [Elasticsearch功能适用场景特点](#Elasticsearch功能适用场景特点)
      - [Elasticsearch核心概念](#Elasticsearch核心概念)
- [Elasticsearch高手进阶篇](#Elasticsearch高手进阶篇)
    - [redis](#redis)
  
# Elasticsearch

## Elasticsearch核心知识入门篇

### Elasticsearch快速入门


#### Elasticsearch功能适用场景特点

1.Elasticsearch的功能、适用场景、以及特点介绍

    1.分布式搜索引擎和数据分析引擎
    2.全文检索、结构化检索、数据分析
    3.对海量数据进行近实时处理

2.Elasticsearch适用场景
  
    1.维基百科、全文检索、高亮、搜索推荐
    2.用户日志、社交网络数据、分析新闻文章公众反馈
    3.日志数据分析、logstash采集日志、复杂的数据分析
    4.分布式搜索引擎和数据分析引擎
    5.全文检索、结构化检索、数据分析
    6.对海量数据进行近实时处理

3.Elasticsearch特点介绍

    1.可以作为大型分布式集群技术，处理PB级数据服务大公司，也可以在单机上服务小公司
    2.全文检索、数据分析、分布式技术结合在一起。
    3.开箱即用、非常简单
    4.Elasticsearch提供了全文检索、同义词处理、相关度排序、复杂数据分析、海量数据近实时的功能

#### Elasticsearch核心概念

    1.Near Realtime(NRT)：近实时,意思是：从查询数据库到数据可以被es搜索到有一个延迟(大概1S);基于es执行搜索和分析可以达到秒级
    2.cluster:集群,包含多个节点,每个节点属于哪个 集群是通过一个配置(集群名称,默认是elasticsearch)来决定的。
    3.node：节点，几圈中的一个节点，节点也有名称（默认是随机分配的）,节点名称很重要(在运维管理进行操作的时候),默认节点会去加入一个名称为"elasticsearch"的集群中，如果直接启动一堆节点,那么他们会自动组成elasticsearch集群，当然一个节点可以组成elasticsearch集群
    4.document:文档,es中最小的数据单元,一个document可以是一条订单数据或者是一个商品数据，通常用JSON数据结构表示,每个index下type中都可以存储多个document,一个document里面有多个field，每个field就是一个数据字段
    5.index:索引，包含一堆相似的文档数据,比如订单索引，索引有一个名称。一个index包含多个document，一个index就代表一类类似的document.比如说建立一个product index，商品索引,里面可能就存放了所有的商品数据，所有的商品document.
    6.type:类型,每个索引都可以有一个活多个type，type是index中的一个逻辑数据分类,一个type下的document都有相同的field
    7.shard：单台机器无法存储大量数据,es可以将一个索引中的数据切分为多个shard，分布在多台服务器上存储.有了shard就可以横向扩展，存储更多数据,让搜索和分析等操作分布到多台机器上，执行速度快,提升吞吐量和性能.
    8.replica:粉盒一个服务器随机可能出现故障或者宕机.因此可以为每个shard创建多个replica副本,replica可以在shard故障时候提供备用，保证数据不丢失。多个replica哈可以提升搜索作用的吞吐量和性能。
    primary shard(建立索引时候一次设置,不能修改,默认5个),replica shard（随时修改数量,默认1个）,默认每个索引10个shard.5个primary shard。5个replica shard。最小高可用配置，是两台server.
