---
layout: post
title: "[Python]BOJ_1005_ACM Craft"
categories:
  - Coding-Test
  - Python
tags:
  - Dynamic Programming
  - Tree
created_at: 2021-02-08T13:55:00+09:00
modified_at: 2021-02-08T13:55:00+09:00
visible: true
---



[BOJ 1005 ACM Craft](https://www.acmicpc.net/problem/1005)

```python
from sys import stdin, setrecursionlimit

setrecursionlimit(100000000)

def solution():
    def get_total_build_time(i):
        if total_build_time[i] != -1:
            return total_build_time[i]
        
        total_build_time[i] = build_time[i] + max([get_total_build_time(b) for b in build_tree[i]])

        return total_build_time[i]

    N, K = map(int, stdin.readline().split())
    build_time = [0] + [*map(int, stdin.readline().split())]
    build_tree = [[] for _ in range(N+1)]
    
    for _ in range(K):
        b, a = map(int, stdin.readline().split())
        build_tree[a].append(b)
    
    W = int(stdin.readline())
    total_build_time = [-1] * (N+1)
    for n in range(1, N+1):
        if not build_tree[n]:
            total_build_time[n] = build_time[n]
    
    print(get_total_build_time(W))

    
T = int(stdin.readline())
for t in range(T):
    solution()
```

