---
layout: post
title: "Elasticsearch7.3 High Level REST Client Java API 예제"
date: 2019-10-14 12:24:00 +0900
categories: Elasticsearch Java
tags: Elasticsearch Java
img: elasticsearch.png # Add image post (optional)  
---

# Initialization

```java
final ArrayList<HttpHost> hostList = new ArrayList<HttpHost>();

LogManager.logger.debug("Elasticsearch client initialization");

for (ESDataNodeVO esDataNodeVO : mESPropertiesVO.getDataNodeList())
    hostList.add(newHttpHost(esDataNodeVO.getHost(), esDataNodeVO.getPort(), "http"));
    
final RestClientBuilder builder = RestClient.builder(hostList.toArray(new HttpHost[hostList.size()]));

mCQueue.enqueue(new RestHighLevelClient(builder));
```

