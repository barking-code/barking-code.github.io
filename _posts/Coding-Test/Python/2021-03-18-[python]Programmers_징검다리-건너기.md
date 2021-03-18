---
layout: post
title: "[Python]Programmers_징검다리 건너기"
categories:
  - Coding-Test
  - Python
tags:
  - Sliding Window
created_at: 2021-03-18T17:46:00+09:00
modified_at: 2021-03-18T17:46:00+09:00
visible: true
---



[Programmers 징검다리 건너기](https://programmers.co.kr/learn/courses/30/lessons/64062)

```python
from collections import deque

def solution(stones, k):
    window = deque()
    _min = max(stones)
    for i in range(len(stones)):
        while window and window[-1][0] <= stones[i]:
            window.pop()
        
        window.append((stones[i], i))

        while window[0][1] <= i - k:
            window.popleft()

        if i >= k-1:
            _min = min(_min, window[0][0])

    return _min
```
