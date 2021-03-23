---
layout: post
title: "[Python]Programmers_3진법 뒤집기"
categories:
  - Coding-Test
  - Python
tags:
  - Math
created_at: 2021-03-22T17:38:00+09:00
modified_at: 2021-03-22T17:38:00+09:00
visible: true
---



[Programmers 3진법 뒤집기](https://programmers.co.kr/learn/courses/30/lessons/68935)

```python
def solution(n):
    _3jin = []
    
    while n // 3:
        _3jin.append(n % 3)
        n //= 3
        
    _3jin.append(n)
    
    ans = 0
    i = 0
    while _3jin:
        ans += _3jin.pop() * 3**i
        i += 1
        
    return ans
```
