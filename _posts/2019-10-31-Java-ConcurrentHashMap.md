---
layout: post
title: "Thread-Safe를 위한 ConcurrentHashMap"
date: 2019-10-31 12:51:00 +0900
categories: Java
tags: Java
img: concurrenthashmap.png 
---

# Thread-Safe
&nbsp; Multi-Thread 환경에서 개발 시 Thread-Safe는 중요한 부분이다. 현재 업무에서 Multi-Thread를 다루기 이 부분을 정리하고자 한다.<br>
&nbsp; Thread-Safe란, 동기화(Synchronize)라고 표현하기도 하며 어떠한 Class의 인스턴스가 여러개의 Thread에서 동시 참조되고 해당 객체에 Operation 이 발생해도 정합성을 유지해줄때 보통 우리는 Thread-Safe 하다 라고 표현한다.

# ConcurrentHashMap

Reference: [조금 늦은, IT 관습 넘기](http://blog.breakingthat.com/2019/04/04/java-collection-map-concurrenthashmap/)
