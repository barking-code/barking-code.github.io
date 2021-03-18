---
layout: post
title: "[Python]Programmers_경주로 건설"
categories:
  - Coding-Test
  - Python
tags:
  - Dijkstra
created_at: 2021-03-18T18:39:00+09:00
modified_at: 2021-03-18T18:39:00+09:00
visible: true
---



[Programmers 경주로 건설](https://programmers.co.kr/learn/courses/30/lessons/67259)

```python
import heapq

dr = [-1, 0, 1, 0]
dc = [0, 1, 0, -1]

def solution(board):
    def dijkstra():
        visit = [[[100000000 for _ in range(4)] for _ in range(N)] for _ in range(N)]
        for d in range(4):
            visit[0][0][d] = 0

        heap = []
        if not board[0][1]:
            heap.append((100, 0, 1, 1))
            visit[0][1][1] = 100
        if not board[1][0]:
            heap.append((100, 1, 0, 2))
            visit[1][0][2] = 100
        
        heapq.heapify(heap)
        while heap:
            cost, r, c, dirt = heapq.heappop(heap)

            for d in range(4):
                tr, tc = r+dr[d], c+dc[d]

                if not (0 <= tr < N and 0 <= tc < N): continue
                if board[tr][tc]: continue

                curve = 0 if dirt % 2 == d % 2 else 500
                if visit[tr][tc][d] < cost + 100 + curve: continue

                visit[tr][tc][d] = cost + 100 + curve
                heapq.heappush(heap, (cost + 100 + curve, tr, tc, d))
        
        return min(visit[N-1][N-1])

        
    N = len(board)
    return dijkstra()
```
