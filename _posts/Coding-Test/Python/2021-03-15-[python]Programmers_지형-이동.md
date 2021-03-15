---
layout: post
title: "[Python]Programmers_지형 이동"
categories:
  - Coding-Test
  - Python
tags:
  - Djikstra
  - Priority Queue
created_at: 2021-03-15T16:08:00+09:00
modified_at: 2021-03-15T16:08:00+09:00
visible: true
---



[Programmers 지형 이동](https://programmers.co.kr/learn/courses/30/lessons/62050)

```python
import heapq

dr = [-1, 0, 1, 0]
dc = [0, 1, 0, -1]

def solution(land, height):
    def dijkstra(r, c):
        total = 0
        
        visit = [[False for _ in range(N)] for _ in range(N)]
        
        heap = []
        heapq.heappush(heap, (0, r, c))
        while heap:
            cost, r, c = heapq.heappop(heap)
            
            if visit[r][c]: continue
            visit[r][c] = True
            
            total += cost
            
            for d in range(4):
                tr, tc = r+dr[d], c+dc[d]
                
                if not (0 <= tr < N and 0 <= tc <N): continue
                if visit[tr][tc]: continue
                
                diff = abs(land[r][c] - land[tr][tc])
                
                if diff <= height:
                    heapq.heappush(heap, (0, tr, tc))
                else:
                    heapq.heappush(heap, (diff, tr, tc))
                    
        return total
    
    N = len(land)
    
    return dijkstra(0, 0)
```
