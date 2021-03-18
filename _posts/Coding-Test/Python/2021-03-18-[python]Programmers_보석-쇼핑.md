---
layout: post
title: "[Python]Programmers_보석 쇼핑"
categories:
  - Coding-Test
  - Python
tags:
  - Two Pointer
created_at: 2021-03-18T16:31:00+09:00
modified_at: 2021-03-18T16:31:00+09:00
visible: true
---



[Programmers 보석 쇼핑](https://programmers.co.kr/learn/courses/30/lessons/67258)

```python
def solution(gems):
    gem_dict = {k:0 for k in set(gems)}
    N = len(gems)
    T = len(gem_dict)
    
    total = 0
    s, e = 0, 0
    _min = float('inf')
    while e < N:
        if not gem_dict[gems[e]]:
            total += 1
        
        gem_dict[gems[e]] += 1

        if total == T:
            while gem_dict[gems[s]] > 1:
                gem_dict[gems[s]] -= 1
                s += 1
            
            if _min > e - s:
                _min = e - s
                ans = [s+1, e+1]
        
        e += 1

    return ans
```
