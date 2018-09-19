---
description: elasticsearch search type
---

# ES分布式搜索的集中不同策略

{% embed data="{\"url\":\"https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-search-type.html\",\"type\":\"link\",\"title\":\"Search Type\\n        \| Elasticsearch Reference \[6.3\]\\n      \| Elastic\",\"description\":\"Get started with the documentation for Elasticsearch, Kibana, Logstash, Beats, X-Pack, Elastic Cloud, Elasticsearch for Apache Hadoop, and our language clients.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.elastic.co/android-chrome-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.elastic.co/static/images/elastic-logo-200.png\",\"width\":200,\"height\":200,\"aspectRatio\":1}}" %}

## 分布式索索

![](../.gitbook/assets/image%20%2816%29.png)

![](../.gitbook/assets/image%20%2810%29.png)

##  **query\_then\_fetch**

 如果你搜索时，没有指定搜索方式，就是使用的这种搜索方式。这种搜索方式，大概分两个步骤，第一步，先向所有的shard发出请求，各分片只返回排序和排名相关的信息（注意，不包括文档document\)，然后按照各分片返回的分数进行重新排序和排名，取前size个文档。然后进行第二步，去相关的shard取document。这种方式返回的document与用户要求的size是相等的。

##  **query and fetch**

 向索引的所有分片（shard）都发出查询请求，各分片返回的时候把元素文档（document）和计算后的排名信息一起返回。这种搜索方式是最快的。因为相比下面的几种搜索方式，这种查询方法只需要去shard查询一次。但是各个shard返回的结果的数量之和可能是用户要求的size的n倍。

##  **DFS query then fetch**

dfs 搜索类型有一个预查询的阶段，它会从全部相关的分片里取回项目频数来计算全局的项 目频数。 从es的官方网站我们可以指定，初始化散发其实就是在进行真正的查询之前，先把各个分片的词频率和文档频率收集一下，然后进行词搜索的时候，各分片依据全局的词频率和文档频率进行搜索和排名。显然如果使用DFS\_QUERY\_THEN\_FETCH这种查询方式，效率是最低的，因为一个搜索，可能要请求3次分片。但，使用DFS方法，搜索精度应该是最高的。

 这种方式比query then fetch多了一个初始化散发\(initial scatter\)步骤，有这一步，据说可以更精确控制搜索打分和排名。

##  **DFS query and fetch**

这种方式比query andfetch多了一个初始化散发\(initial scatter\)步骤，有这一步，据说可以更精确控制搜索打分和排名。

 总结一下，从性能考虑QUERY\_AND\_FETCH是最快的，DFS\_QUERY\_THEN\_FETCH是最慢的。从搜索的准确度来说，DFS要比非DFS的准确度更高。

## count

count（计数） 搜索类型只有一个 query（查询） 的阶段。当不需要搜索结果只需要知道满足查 询的document的数量时，可以使用这个查询类型。  


## scan

scan（扫描） 搜索类型是和 scroll（滚屏） API连在一起使用的，可以高效地取回巨大数量的结 果。它是通过禁用排序来实现的。  


![](../.gitbook/assets/image%20%284%29.png)

