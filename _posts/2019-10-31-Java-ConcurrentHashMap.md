---
layout: post
title: "Thread-Safe를 위한 ConcurrentHashMap"
date: 2019-10-31 12:51:00 +0900
categories: Java
tags: Java
img: concurrenthashmap.png 
---

# Thread-Safe
&nbsp; Multi-Thread 환경에서 개발 시 Thread-Safe는 중요한 부분이다. 현재 업무에서 Multi-Thread를 다루기에 이 부분을 정리하고자 한다.<br>
&nbsp; Thread-Safe란, 동기화(Synchronize)라고 표현하기도 하며 어떠한 Class의 인스턴스가 여러개의 Thread에서 동시 참조되고 해당 객체에 Operation 이 발생해도 정합성을 유지해줄때 보통 우리는 Thread-Safe 하다 라고 표현한다.

# Map
&nbsp; Map 자료구조를 사용하는 Multi-Thread 환경에서 개발 시  **ConcurrentModificationException**을 한번쯤은 마주할 것이라 생각한다. 
그 중 HashMap은 Hash 알고리즘으로 구현되어 있기에 데이터를 가져오는(Get) 속도가 빠르고 효율적이어서 많이 활용하는 자료구조이다. 
 내부 메소드에 Synchronized가 선언 되어있지 않기 때문에  Multi-Thread 환경에서 동시 참조 할 경우 데이터 무결성이 보장되지 않는다.<br> 
&nbsp; 동기화 collection인 HashTable이나 Collections.synchronizedMap(new HashMap())으로 Wrapping하여 Thread-Safe는 보장할 수 있다고는 하나(완벽히라고는 할 수 없다) **ConcurrentModificationException**을 피할 수는 없을 것이다.
이 두 구조는 내부적으로 모든 데이터 변경 메소드가 syncronized로 선언되어 있어 전체 Lock을 통해 Thread-Safe가 보장된다. 그러나 객체를 참조하는 갯수가 늘어나고 대기시간이 길어질 수록 성능 저하는 당연한 결과일 것이다. 
또한 반복문(Iterator) 실행 도중 내부 값이 변경된다면 즉시 멈춤(Fail-Fast) 방식으로 앞에서 언급했던 **ConcurrentModificationException** 예외를 발생시키고 멈추어 버린다.



 Java1.5 이후 **[java.util.concurrent](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/concurrent/package-summary.html)** Package가 나오면서 **[ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)** Class가 등장했다.

### ▶ Synchronized Map
```java
Map<String, Object> hashTable = new Hashtable<String, Object>();
Map<String, Object> synchronizedMap = Collections.synchronizedMap(new HashMap<String, Object>());
Map<String, Object> concurrentHashMap = new ConcurrentHashMap<String, Object>();
```

# ConcurrentHashMap

<!--
iframely 이용한 gist 코드 

<div class="iframely-embed">
	<div class="iframely-responsive" style="padding-bottom: 56.2493%;">
		<a href="https://gist.github.com/hboseong/a8b642ae38fde033e109880b620c19dd" data-iframely-url="//cdn.iframe.ly/LMmmroc"></a>
	</div>
</div>
<script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>
--> 

# Example
Reference: [조금 늦은, IT 관습 넘기](http://blog.breakingthat.com/2019/04/04/java-collection-map-concurrenthashmap) / [JDM's Blog](https://jdm.kr/blog/197)  / [이러쿵저러쿵](https://ooz.co.kr/71)
