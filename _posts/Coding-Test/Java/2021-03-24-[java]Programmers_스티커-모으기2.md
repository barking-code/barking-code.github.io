---
layout: post
title: "[Java]Programmers_스티커 모으기2"
categories:
  - Coding-Test
  - Java
tags:
  - Dynamic Programming
created_at: 2021-03-24T02:16:00+09:00
modified_at: 2021-03-24T02:16:00+09:00
visible: true
---



[Programmers 스티커 모으기2](https://www.acmicpc.net/problem/12971)

```java
package Solutions;

public class 스티커_모으기2 {
    public static int N;
    public static int max = 0;

    public int solution(int sticker[]) {
        N = sticker.length;
        if (N == 1) return sticker[0];
        if (N == 2) return Math.max(sticker[0], sticker[1]);

        int[][] selectFirst = new int[2][N];
        selectFirst[1][0] = sticker[0];
        selectFirst[0][1] = sticker[0];
        
        for (int i=2; i < N-1; i++) {
            selectFirst[0][i] = Math.max(selectFirst[0][i-1], selectFirst[1][i-1]);
            selectFirst[1][i] = Math.max(selectFirst[0][i-1], selectFirst[1][i-2]) + sticker[i];
        }
        
        int[][] skipFirst = new int[2][N];
        skipFirst[1][1] = sticker[1];

        for (int i=2; i < N; i++) {
            skipFirst[0][i] = Math.max(skipFirst[0][i-1], skipFirst[1][i-1]);
            skipFirst[1][i] = Math.max(skipFirst[0][i-1], skipFirst[1][i-2]) + sticker[i];
        }

        for (int i=0; i < 2; i ++) {

            max = Math.max(selectFirst[i][N-2], max);
            max = Math.max(skipFirst[i][N-1], max);
        }

        return max;
    }
}
```

