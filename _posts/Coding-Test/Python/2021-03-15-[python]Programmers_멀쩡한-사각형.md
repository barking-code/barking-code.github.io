---
layout: post
title: "[Python]Programmers_멀쩡한 사각형"
categories:
  - Coding-Test
  - Python
tags:
  - Math
created_at: 2021-03-15T16:34:00+09:00
modified_at: 2021-03-15T16:34:00+09:00
visible: true
---



[Programmers 멀쩡한 사각형](https://programmers.co.kr/learn/courses/30/lessons/62048)

```python
import math

def solution(w,h):
    if w == h: return w**2 - w
    
    gcd = math.gcd(w, h)
    x, y = w // gcd, h // gcd
    
    return x * y * (gcd**2 - gcd) + gcd * count_square(x, y)

def count_square(x, y):
    total = 0
    
    for xx in range(1, x):
        total += (y*xx) // x
        
    return total * 2
```
