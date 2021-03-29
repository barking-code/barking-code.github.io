---
layout: post
title: "[Python]Programmers_등굣길"
categories:
  - Coding-Test
  - Python
tags:
  - Dynamic Programming
created_at: 2021-03-22T17:52:00+09:00
modified_at: 2021-03-22T17:52:00+09:00
visible: true
---



[Programmers 등굣길](https://programmers.co.kr/learn/courses/30/lessons/42898)

```python
def solution(R, C, puddles):
    def set_dp(r, c):
        if not (0 <= r < R and 0 <= c < C): return 0
        if board[r][c]: return 0
        if dp[r][c]: return dp[r][c]

        dp[r][c] = (set_dp(r-1, c) + set_dp(r, c-1)) % 1000000007
        return dp[r][c]

    board = [[0 for _ in range(C)] for _ in range(R)]

    for r, c in puddles:
        board[r-1][c-1] = 1

    dp = [[0 for _ in range(C)] for _ in range(R)]
    dp[0][0] = 1

    return set_dp(R-1, C-1)
```
