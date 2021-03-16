---
layout: post
title: "[Python]Programmers_무지의 먹방 라이브"
categories:
  - Coding-Test
  - Python
tags:
  - Priority Queue
created_at: 2021-03-16T18:36:00+09:00
modified_at: 2021-03-16T18:36:00+09:00
visible: true
---



[Programmers 오픈채팅방](https://programmers.co.kr/learn/courses/30/lessons/42888)

```python
from queue import PriorityQueue

def solution(food_times, k):
    N = len(food_times)

    if N > k: return k+1
    if sum(food_times) <= k: return -1
    
    q = PriorityQueue()
    for h in map(lambda x: (food_times[x], x), [i for i in range(N)]):
        q.put(h)

    count = N
    cycle = 0
    while not q.empty() and k - (q.queue[0][0] - cycle) * count >= 0:
        f, i = q.get()
        k -= (f - cycle) * count
        
        count -= 1
        cycle = f
        
    if q.empty(): return -1
    
    q.queue.sort(key=lambda x: x[1])
    return q.queue[k % q.qsize()][1] + 1
```

* 동일한 로직의 heapq 를 사용한 풀이는 더 오래걸린다

```python
import heapq

def solution(food_times, k):
    N = len(food_times)

    if N > k: return k+1
    if sum(food_times) <= k: return -1
    
    heap = [*map(lambda x: (food_times[x], x), [i for i in range(N)])]
    heapq.heapify(heap)

    count = N
    cycle = 0
    while heap and k - (heapq.nsmallest(1, heap)[0][0] - cycle) * count >= 0:
        f, i = heapq.heappop(heap)
        k -= (f - cycle) * count
        
        count -= 1
        cycle = f
        
    if not heap: return -1
    
    heap.sort(key=lambda x: x[1])
    return heap[k % len(heap)][1] + 1
```

