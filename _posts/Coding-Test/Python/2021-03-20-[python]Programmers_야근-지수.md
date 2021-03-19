---
layout: post
title: "[Python]Programmers_야근 지수"
categories:
  - Coding-Test
  - Python
tags:
  - Math
created_at: 2021-03-20T01:11:00+09:00
modified_at: 2021-03-20T01:11:00+09:00
visible: true
---



[Programmers 야근 지수](https://programmers.co.kr/learn/courses/30/lessons/12927)

```python
def solution(n, works):
    if sum(works) <= n: return 0

    works.sort(reverse=True)
    W = len(works)

    i = 0
    while n > 0:
        works[i] -= 1

        if i == W-1 or works[i] >= works[i+1]:
            i = 0
        else:
            i += 1

        n -= 1
    
    return sum(map(lambda x: x**2 if x > 0 else 0, works))
```
