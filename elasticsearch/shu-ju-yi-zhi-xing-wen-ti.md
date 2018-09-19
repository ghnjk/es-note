# 数据一致性问题

## 分片一致性

{% embed data="{\"url\":\"https://www.elastic.co/blog/tracking-in-sync-shard-copies\",\"type\":\"link\",\"title\":\"Elasticsearch Internals - Tracking in-sync shard copies\",\"description\":\"Deep dive into Elasticsearch\'s internals, highlighting how the consensus module and the data replication layer interact beautifully to keep your data safe.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.elastic.co/android-chrome-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.elastic.co/assets/blt8d293f3ba741a82d/thumbnail.jpg\",\"width\":720,\"height\":420,\"aspectRatio\":0.5833333333333334}}" %}

{% embed data="{\"url\":\"https://www.elastic.co/guide/en/elasticsearch/reference/6.3/docs-replication.html\#\_basic\_write\_model\",\"type\":\"link\",\"title\":\"Reading and Writing documents\\n        \| Elasticsearch Reference \[6.3\]\\n      \| Elastic\",\"description\":\"Get started with the documentation for Elasticsearch, Kibana, Logstash, Beats, X-Pack, Elastic Cloud, Elasticsearch for Apache Hadoop, and our language clients.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.elastic.co/android-chrome-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.elastic.co/static/images/elastic-logo-200.png\",\"width\":200,\"height\":200,\"aspectRatio\":1}}" %}

![](../.gitbook/assets/image%20%2814%29.png)

    简单的说，写请求转发到primary shard逅，primary会判断各备份分片的状态决定是否继续执行。 如果允许写时， 先在本地执行写后， 会将请求并发到备份分片， 等待分片写成功后再返回给客户端。如果存在备份分片执行失败， 则将该分片id从in-sync set剔除， 发通知给master。由master协调数据后再加回来。

![](../.gitbook/assets/image%20%281%29.png)

![](../.gitbook/assets/image%20%2811%29.png)

