---
layout: post
title: "[Python]Programmers_합승 택시 요금"
categories:
  - Coding-Test
  - Python
tags:
  - Dijkstra
created_at: 2021-03-15T18:16:00+09:00
modified_at: 2021-03-15T18:16:00+09:00
visible: true
---



[Programmers 합승 택시 요금](https://programmers.co.kr/learn/courses/30/lessons/72413)

```python
import heapq

def solution(n, s, e1, e2, fares):
    def dijkstra(s, e, n):
        if s == e: return 0
        
        visit = [0] * n
        
        heap = [(0, s)]
        while heap:
            cost, node = heapq.heappop(heap)
            
            if visit[node]: continue
            visit[node] = 1
            
            if node == e: return cost
                
            for n, c in nodes[node]:
                if visit[n]: continue
                heapq.heappush(heap, (c+cost, n))
        
        return float('inf')
                
    nodes = [[] for _ in range(n)]
    
    for a, b, c in fares:
        nodes[a-1].append((b-1, c))
        nodes[b-1].append((a-1, c))
    
    _min = float('inf')
    for i in range(n):
        _min = min(_min, dijkstra(s-1, i, n) + dijkstra(i, e1-1, n) + dijkstra(i, e2-1, n))
        
    return _min
```
