---
layout: post
title: "[Java]Programmers_프린터"
categories:
  - Coding-Test
  - Java
tags:
  - Priority Queue
created_at: 2021-03-31T23:00:00+09:00
modified_at: 2021-03-31T23:00:00+09:00
visible: true
---



[Programmers 프린터](https://www.acmicpc.net/problem/42587)

```java
import java.util.PriorityQueue;

public class 프린터 {
    public int solution(int[] priorities, int location) {
        int N = priorities.length;

        PriorityQueue<Integer> priority = new PriorityQueue<>();
        for (int i: priorities) {
            priority.add(-i);
        }

        boolean[] print = new boolean[N];
        
        int i = -1;
        int cnt = 0;
        while (cnt < N) {
            i = (i+1) % N;
            
            if (print[i]) continue;
            if (priority.peek() != -priorities[i]) continue;

            print[i] = true;
            priority.poll();
            cnt++;
            if (i == location) return cnt;
        }
        
        return cnt;
    }
}
```

