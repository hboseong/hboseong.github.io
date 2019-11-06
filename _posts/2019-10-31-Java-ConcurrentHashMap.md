---
layout: post
title: "Thread-safe를 위한 ConcurrentHashMap"
date: 2019-10-31 12:51:00 +0900
categories: Java
tags: Java
img: concurrenthashmap.png 
---

# Thread-safe
동기화(Synchronize)라고 표현하기도 하며 어떠한 Class의 인스턴스가 여러개의 Thread에서 동시 참조되고 해당 객체에 Operation 이 발생해도 정합성을 유지해줄때 보통 우리는 Thread-Safe 하다 라고 표현한다.


참고: http://blog.breakingthat.com/2019/04/04/java-collection-map-concurrenthashmap/