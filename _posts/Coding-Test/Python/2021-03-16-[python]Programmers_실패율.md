---
layout: post
title: "[Python]Programmers_실패율"
categories:
  - Coding-Test
  - Python
tags:
  - Sort
created_at: 2021-03-16T14:26:00+09:00
modified_at: 2021-03-16T14:26:00+09:00
visible: true
---



[Programmers 실패율](https://programmers.co.kr/learn/courses/30/lessons/42889)

```python
def solution(N, stages):  
    fail = [0] * (N+2)
    for s in stages:
        fail[s] += 1
        
    total = fail[:]
    for i in range(N, 0, -1):
        total[i] += total[i+1]
        
    return sorted([i for i in range(1, N+1)], key=lambda x: (-fail[x]/total[x] if total[x] else 0, x))
```
