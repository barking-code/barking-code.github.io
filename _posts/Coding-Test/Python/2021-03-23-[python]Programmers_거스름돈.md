---
layout: post
title: "[Python]Programmers_거스름돈"
categories:
  - Coding-Test
  - Python
tags:
  - Dynamic Programming
created_at: 2021-03-23T16:18:00+09:00
modified_at: 2021-03-23T16:18:00+09:00
visible: true
---



[Programmers 거스름돈](https://programmers.co.kr/learn/courses/30/lessons/12907)

```python
def solution(n, money):
    dp = [0] * (n + 1)
    
    for coin in reversed(money):
        for m in range(coin+1, n-coin+1):
            if not dp[m]: continue
            dp[coin+m] += dp[m]
            dp[coin+m] %= 1000000007
        
        coin_d = coin
        while coin_d <= n:
            dp[coin_d] += 1
            coin_d += coin

    return dp[n]
```
