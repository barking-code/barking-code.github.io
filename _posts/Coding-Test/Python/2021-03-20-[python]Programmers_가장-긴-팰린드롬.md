---
layout: post
title: "[Python]Programmers_가장 긴 팰린드롬"
categories:
  - Coding-Test
  - Python
tags:
  - Two Pointer
created_at: 2021-03-20T02:01:00+09:00
modified_at: 2021-03-20T02:01:00+09:00
visible: true
---



[Programmers 가장 긴 팰린드롬](https://programmers.co.kr/learn/courses/30/lessons/12904)

```python
def solution(s):
    def palindrome_checker(l, r, s):
        while l < r:
            if s[l] != s[r]: return False
            l += 1
            r -= 1
        
        return True

    for i in range(len(s)-1, 1, -1):
        for j in range(len(s)-i):
            if palindrome_checker(j, j+i, s): return i+1
    return 1
```
