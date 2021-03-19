---
layout: post
title: "[Python]Programmers_줄 서는 방법"
categories:
  - Coding-Test
  - Python
tags:
  - Combination
created_at: 2021-03-19T20:45:00+09:00
modified_at: 2021-03-19T20:45:00+09:00
visible: true
---



[Programmers 줄 서는 방법](https://programmers.co.kr/learn/courses/30/lessons/12936)

```python
def solution(n, k):
    fac = [1] * (n)
    for i in range(1, n):
        fac[i] = fac[i-1] * i

    nums = [i for i in range(1, n+1)]
    ans = []
    k -= 1
    while n > 0:
        if k == 0:
            ans.extend(nums)
            break

        i, k = k // fac[n-1], k % fac[n-1]
        ans.append(nums.pop(i))
        
        n -= 1
        
    return ans
```
