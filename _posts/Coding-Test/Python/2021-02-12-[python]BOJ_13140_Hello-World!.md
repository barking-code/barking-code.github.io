---
layout: post
title: "[Python]BOJ_13140_Hello World!"
categories:
  - Coding-Test
  - Python
tags:
  - Back Tracking
created_at: 2021-02-12T14:45:00+09:00
modified_at: 2021-02-12T14:45:00+09:00
visible: true
---



[BOJ 13140_Hello World!](https://www.acmicpc.net/problem/13140)

```python
from sys import stdin

def solution():
    def add_hello_world(h, w, e, o, l, r, d):
        return (h+w) * 10**4 + (e+o) * 10**3 + (l+r) * 10**2 + (l+l) * 10 + (o+d)

    def BACK(i):
        if i == 7:
            return add_hello_world(*hweolrd) == int(N)

        r = 1 if i < 2 else 0
        for j in range(r, 10):
            if visit[j]: continue
            visit[j] = 1
            hweolrd[i] = j

            ans = BACK(i+1)
            if ans:
                return ans

            hweolrd[i] = -1
            visit[j] = 0

        return 0

    N = int(stdin.readline())
    if not(33946 <= int(N) <= 184010): 
        print("No Answer")
        return

    visit = [0] * 10
    hweolrd = [-1] * 7

    ans = BACK(0)
    if ans:
        h, w, e, o, l, r, d = hweolrd
        print("  %s%s%s%s%s" % (h, e, l, l, o))
        print("+ %s%s%s%s%s" % (w, o, r, l, d))
        print("-------")
        print("%7s" % N)
    else:
        print("No Answer")

solution()
```

