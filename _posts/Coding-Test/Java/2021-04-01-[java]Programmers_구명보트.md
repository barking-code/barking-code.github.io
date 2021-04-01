---
layout: post
title: "[Java]Programmers_구명보트"
categories:
  - Coding-Test
  - Java
tags:
  - Greedy
created_at: 2021-04-01T18:54:00+09:00
modified_at: 2021-04-01T18:54:00+09:00
visible: true
---



[Programmers 구명보트](https://www.acmicpc.net/problem/42885)

```java
import java.util.Arrays;

public class 구명보트 {
    public int solution(int[] people, int limit) {
        Arrays.sort(people);
        
        int cnt = 0;
        int hi = people.length;
        int lo = 0;
        while (hi > lo) {
            hi--;

            if (people[hi] + people[lo] <= limit) {
                lo++;
            }

            cnt++;
        }
        
        return cnt;
    }
}
```

