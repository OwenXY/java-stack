# Elasticsearch

## 目录

- [Elasticsearch核心知识入门篇](#Elasticsearch核心知识入门篇)
    - [Elasticsearch快速入门](#Elasticsearch快速入门)
      - [Elasticsearch功能适用场景特点](#Elasticsearch功能适用场景特点)
      - [Elasticsearch核心概念](#Elasticsearch核心概念) 
      - [Elasticsearch安装部署](#Elasticsearch安装部署)
      - [Elasticsearch文档的CRUD](#Elasticsearch文档的CRUD)
      - [Elasticsearch多种搜索方式](#Elasticsearch多种搜索方式)
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

#### Elasticsearch安装部署

Elasticsearch安装

    docker pull elasticsearch:7.6.2

    vim /etc/sysctl.conf #文件最后添加一行 vm.max_map_count=262144
    
    mkdir -p /data/elasticsearch/config
    mkdir -p /data/elasticsearch/data
    
    进入config目录下 创建 elasticsearch.yml文件 粘贴下面配置
    
    http.host: 0.0.0.0
    http.port : 9200
    transport.tcp.port : 9300
    http.cors.enabled : true
    http.cors.allow-origin : "*"
    network.bind_host: 0.0.0.0
    xpack.security.enabled: true
    xpack.security.audit.enabled: true
    
    #启动
    
    docker run -d --restart=always -p 9200:9200 -p 9300:9300 --name elasticsearch -e "discovery.type=single-node" -e "cluster.name=elasticsearch" -v /data/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /data/elasticsearch/data:/usr/share/elasticsearch/data -v /data/elasticsearch/plugins:/usr/share/elasticsearch/plugins elasticsearch:7.6.2

    #启动完毕后设置密码 参考文档: https://www.cnblogs.com/woshimrf/p/docker-es7.html
    #进入容器
    docker exec -it elasticsearch /bin/bash
    执行: ./bin/elasticsearch-setup-passwords auto
    输出以下信息:
    Changed password for user apm_system
    PASSWORD apm_system = l5CWYr67Q6CJUzpKyvZb
    
    Changed password for user kibana
    PASSWORD kibana = HOauyvrBjHKxwQ1R2Idt
    
    Changed password for user logstash_system
    PASSWORD logstash_system = sHvJEh4kxu0inCAlk8Uc
    
    Changed password for user beats_system
    PASSWORD beats_system = 8YmZ4TAAlaSzuVMgBSDi
    
    Changed password for user remote_monitoring_user
    PASSWORD remote_monitoring_user = X48M4DRRnWBTgG8y9dWb
    
    Changed password for user elastic
    PASSWORD elastic = e4R0G5bbwWTT7IuTdR63
    
    审核服务器:
    Changed password for user apm_system
    PASSWORD apm_system = E1OeyBsIoY1f4Hk8p3gM
    
    Changed password for user kibana
    PASSWORD kibana = 2qlVVaovTSguYNhw4YRf
    
    Changed password for user logstash_system
    PASSWORD logstash_system = m0Z9JdoGcPLLuLtjqrNv
    
    Changed password for user beats_system
    PASSWORD beats_system = LgNP0AhqfkEBKyg7E006
    
    Changed password for user remote_monitoring_user
    PASSWORD remote_monitoring_user = MpiGnxDhy36DtSviy7Bj
    
    Changed password for user elastic
    PASSWORD elastic = YWUVdA9MQPhUcFAt9JdH
    
    生产密码:
    Changed password for user apm_system
    PASSWORD apm_system = rx7WKzaqc1jZMLISiodA
    
    Changed password for user kibana
    PASSWORD kibana = lXGbcUu5wFH27XLeOUfL
    
    Changed password for user logstash_system
    PASSWORD logstash_system = 9S2Mg1vkUjeqQUdDmCik
    
    Changed password for user beats_system
    PASSWORD beats_system = k0pxVqpDQtJnK6z6sjok
    
    Changed password for user remote_monitoring_user
    PASSWORD remote_monitoring_user = gN9dIqHHHRMyVmzifIVU
    
    Changed password for user elastic
    PASSWORD elastic = n4rI5IOzxqC0Db1HJKzc

查看Elasticsearch是否启动成功

http://ip:port/?pretty

    {
    "name" : "66405ae2daed",    //Node名称
    "cluster_name" : "docker-cluster",  //集群名称  在Elasticsearch.yml 文件里修改
    "cluster_uuid" : "5_7wD3BtSKSuIYrBas5w0A",
    "version" : {
    "number" : "7.13.1",         //版本号
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "9a7758028e4ea59bcab41c12004603c5a7dd84a9",
    "build_date" : "2021-05-28T17:40:59.346932922Z",
    "build_snapshot" : false,
    "lucene_version" : "8.8.2",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
    },
    "tagline" : "You Know, for Search"
    }


查看Elasticsearch集群状态
GET ip:port/_cat/health?v

green：每个索引的primary shard和replica shard 都是activity
yellow：每个索引的primary shard 都是activity ，部分replica shard 不是activity状态，是不可用的状态
red：不是所有的primary shard都是activity，部分索引有数据丢失

kibana安装

    mkdir -p /data/kibana/config
    docker pull kibana:7.6.2
    
    vim /data/kibana/config/kibana.yml # 填入下面配置
    
    i18n.locale: 'zh-CN'
    server.host: '0.0.0.0'
    elasticsearch.hosts: ['http://172.18.14.12:9200','http://172.18.14.15:9200','http://172.18.14.10:9200']
    elasticsearch.username: 'elastic'
    elasticsearch.password: 'n4rI5IOzxqC0Db1HJKzc'
    xpack:
      apm.ui.enabled: false
      graph.enabled: false
      ml.enabled: false
      monitoring.enabled: false
      reporting.enabled: false
      security.enabled: false
      grokdebugger.enabled: false
      searchprofiler.enabled: false

    
    # 运行
    docker run -d -it --restart=always --privileged=true --name=kibana -p 15601:5601 -v /data/kibana/config/kibana.yml:/usr/share/kibana/config/kibana.yml kibana:7.6.2


#### Elasticsearch文档的CRUD

快速查看集群中有哪些索引
    
        GET /_cat/indecs?v

创建索引

       PUT /test?pretty

删除索引

    DELETE /test?pretty


**document CRUD** 

    新增document文档
        put /index/type/id
        {
            "key1":"value1",
            "key2":"value2",
        }
    更新document文档
    POST /index/type/id/_update
       "doc" {
            "key1":"value1",
            "key2":"value2",
    }
    
    删除document文档
    DELETE /index/type/id?pretty
 

#### Elasticsearch多种搜索方式

（1）、query string search（因为search都是http请求query string来附带的）

    语法：GET /index/type/_search
    
    例：GET /index/type/_search?q="search"&sort=filed:desc

    结果
        {
        "took" : 0, h耗费了几秒
        "timed_out" : false, 是否超时
        "_shards" : { // 请求了几个shard
        "total" : 3,
        "successful" : 3,
        "skipped" : 0,
        "failed" : 0
        },
        "hits" : {
        "total" : {  查询的数量
        "value" : 174,
        "relation" : "eq"
        },
        "max_score" : 1.0, 相关度匹配分数，越相关就越匹配，分数越高
        "hits" : [  匹配的document的相关数据
        ]

在生产环境很少用

（2）、query DSL（Domain Specified Language 特定领域的语言） 基于Http request body请求体，可以用json格式构建语法，可以构建各种复杂的语法