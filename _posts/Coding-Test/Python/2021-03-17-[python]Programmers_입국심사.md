---
layout: post
title: "[Python]Programmers_입국심사"
categories:
  - Coding-Test
  - Python
tags:
  - Binary Search
created_at: 2021-03-17T17:56:00+09:00
modified_at: 2021-03-17T17:56:00+09:00
visible: true
---



[Programmers 입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

```python
def solution(n, times):
    def binary(s, e, n):
        if s == e: return s

        m = (s + e) // 2

        cnt = 0
        for time in times:
            cnt += m // time
        
        if cnt < n:
            return binary(m+1, e, n)
        else:
            return binary(s, m, n)

    return binary(0, min(times) * n, n)
```
