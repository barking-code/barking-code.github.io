---
layout: post
title: "[Java]Programmers_멀리 뛰기"
categories:
  - Coding-Test
  - Java
tags:
  - Memoization
created_at: 2021-03-24T17:35:00+09:00
modified_at: 2021-03-24T17:35:00+09:00
visible: true
---



[Programmers 멀리 뛰기](https://www.acmicpc.net/problem/12914)

```java
public class 멀리_뛰기 {
    public long solution(int n) {
        if (n < 3) return n;
        
        long tmp = 0;
        long before = 1;
        long answer = 2;
        int k = 2;
        while (k < n) {
            tmp = answer;
            answer += before;
            before = tmp;

            answer %= 1234567;
            k++;
        }

        return answer;
    }
}
```

