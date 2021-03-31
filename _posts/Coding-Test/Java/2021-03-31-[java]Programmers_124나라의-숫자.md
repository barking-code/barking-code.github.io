---
layout: post
title: "[Java]Programmers_124나라의 숫자"
categories:
  - Coding-Test
  - Java
tags:
  - Math
created_at: 2021-03-31T21:45:00+09:00
modified_at: 2021-03-31T21:45:00+09:00
visible: true
---



[Programmers 124나라의 숫자](https://www.acmicpc.net/problem/12899)

```java
public class _124나라의_숫자 {
    public String solution(int n) {
        StringBuffer answer = new StringBuffer();
        int e;
        while (n != 0) {
            e = n % 3;

            if (e == 0) {
                e = 4;
                n = n / 3 - 1;
            } else {
                n /= 3;
            }

            answer.insert(0, e);
        }
        
        return answer.toString();
    }
}
```

