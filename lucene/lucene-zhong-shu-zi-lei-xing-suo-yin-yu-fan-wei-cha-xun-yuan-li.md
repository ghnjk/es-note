# lucene中数字类型索引与范围查询原理

## 问题

目前lucene要求term按照字典序\(lexicographic sortable\)排列,然后它的范围查询根据tii找到范围的起始Term，然后把这中间的所有的Term展开成一个BooleanQuery。  
因此, 若按照现有的方式, 如果直接保存16,24,3,46, 当搜索\[24,46\]的时候, 会同时将3也搜索出来, 这是有问题的.



