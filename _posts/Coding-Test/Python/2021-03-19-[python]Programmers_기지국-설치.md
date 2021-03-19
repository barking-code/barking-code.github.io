---
layout: post
title: "[Python]Programmers_기지국 설치"
categories:
  - Coding-Test
  - Python
tags:
  - Math
created_at: 2021-03-19T21:32:00+09:00
modified_at: 2021-03-19T21:32:00+09:00
visible: true
---



[Programmers 기지국 설치](https://programmers.co.kr/learn/courses/30/lessons/12979)

```python
def solution(n, stations, w):
    total = 0
    l = 0
    stations.append(n+w+1)
    for r in stations:
        rr = r - w - 1
        if rr <= l:
            l = r + w
            continue

        total += (rr-l) // (w*2+1)
        if (rr-l) % (w*2+1):
            total += 1
        
        l = r + w
    return total

print(solution(11, [4, 11], 1))
```
