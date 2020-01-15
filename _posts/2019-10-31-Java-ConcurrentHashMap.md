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

# ConcurrentHashMap
&nbsp; Map 자료구조를 사용하는 Multi-Thread에서 HashMap을 사용한다면  **ConcurrentModificationException**을 마주하게 될 것이다. HashMap은 Hash 알고리즘으로 구현되어 있기에 데이터를 가져오는(Get) 속도가 빠르고 효율적이어서 많이 활용하는 자료구조이다. 그러나 내부 메소드에 Synchronized가 선언 되어있지 않기 때문에  Multi-Thread 환경에서 동시 Access를 할 경우 데이터 무결성이 보장되지 않는다.<br> 
&nbsp; Map 자료구조의 Thread-Safe를위해  HashTable Class나 Collections.synchronizedMap(HashMap)으로 Wrapping하여 처리했지만 Java1.5 이후 **[java.util.concurrent](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/concurrent/package-summary.html)** Package가 나오면서 **[ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)** Class가 등장했다.

### ▶ Synchronized Map
```java
Map<String, Object> hashTable = new Hashtable<String, Object>();
Map<String, Object> synchronizedMap = Collections.synchronizedMap(new HashMap<String, Object>());
Map<String, Object> concurrentHashMap = new ConcurrentHashMap<String, Object>();
```

<!--
<div class="iframely-embed">
	<div class="iframely-responsive" style="padding-bottom: 56.2493%;">
		<a href="https://gist.github.com/hboseong/a8b642ae38fde033e109880b620c19dd" data-iframely-url="//cdn.iframe.ly/LMmmroc"></a>
	</div>
</div>
<script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>
--> 

# Example

```java

package com.boseong.test.concurrenthashmap;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

public class ThreadSafeTest {

	public static void main(String[] args) {
		
		final ThreadSafeTest threadSafeTest = new ThreadSafeTest();
		threadSafeTest.work(new HashMap<Integer, String>());
		threadSafeTest.work(new ConcurrentHashMap<Integer, String>());
		
	}
	
	public ThreadSafeTest() {
		
	}
	
	public void work(Map<Integer, String> map) {
		
		final Thread putThread = new Thread(()-> {
			
			for (int i = 0; i < 10; i++) 
				map.put(i, i + "_value");
			
			System.out.println("[ " + map.getClass() + "] " + " success put: " + map);
			
		});
		
		putThread.start();
		
		final Thread removeThread = new Thread(()-> {
			
			try {
				
				for (Integer key : map.keySet()) 
					map.remove(key);
				
				System.out.println("[ " + map.getClass() + "] " + " success remove: " + map);
			
			} catch (Exception e) {
				System.err.println("[ " + map.getClass() + "] " + " exception remove: " + e);
			}
			
		});
		
		removeThread.start();
		
	}
	
}

```

<!--
<div class="iframely-embed">
	<div class="iframely-responsive" style="padding-bottom: 56.2493%;">
		<a href="https://gist.github.com/hboseong/14f7949dff1f36761dd66db9d6a922a6" data-iframely-url="//cdn.iframe.ly/puf2tKM"></a>
	</div>
</div>
<script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>
-->

Reference: [조금 늦은, IT 관습 넘기](http://blog.breakingthat.com/2019/04/04/java-collection-map-concurrenthashmap) / [JDM's Blog](https://jdm.kr/blog/197)  / [이러쿵저러쿵](https://ooz.co.kr/71)
