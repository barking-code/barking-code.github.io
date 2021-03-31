---
layout: post
title: "[Java]Programmers_더 맵게"
categories:
  - Coding-Test
  - Java
tags:
  - Priority Queue
created_at: 2021-03-31T23:10:00+09:00
modified_at: 2021-03-31T23:10:00+09:00
visible: true
---



[Programmers 더 맵게](https://www.acmicpc.net/problem/42626)

```java
import java.util.PriorityQueue;

class 더_맵게 {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> heap = new PriorityQueue<>();
        for (int i: scoville) {
            heap.add(i);
        }

        int cnt = 0;
        int lo, lo2;
        while (heap.size() > 1) {
            lo = heap.poll();
            lo2 = heap.poll();

            if (lo >= K) return cnt;

            heap.add(10 + lo2*2);
            cnt++;
        }

        return heap.poll() >= K ? cnt : -1;
    }
}
```

