---
layout: post
title: "Elasticsearch Java High Level REST Client API 예제"
date: 2019-10-14 12:24:00 +0900
categories: Elasticsearch Java
tags: Elasticsearch Java
img: elasticsearch.png # Add image post (optional)  
---

request.settings(Settings.builder() 
    .put("index.number_of_shards", 3)
    .put("index.number_of_replicas", 2)
);


commit test tt