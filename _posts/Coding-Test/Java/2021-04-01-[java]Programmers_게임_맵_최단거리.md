---
layout: post
title: "[Java]Programmers_게임 맵 최단거리"
categories:
  - Coding-Test
  - Java
tags:
  - BFS
created_at: 2021-04-01T21:56:00+09:00
modified_at: 2021-04-01T21:56:00+09:00
visible: true
---



[Programmers 게임 맵 최단거리](https://www.acmicpc.net/problem/1844)

```java
import java.util.Deque;
import java.util.LinkedList;

public class 게임_맵_최단거리 {
    private int R, C;
    private int[][] visit;
    private int[] dr = {-1, 0, 1, 0};
    private int[] dc = {0, 1, 0, -1};

    private int bfs(int[][] board) {
        int[] tmp = {0, 0};
        visit[0][0] = 1;
        Deque<int[]> dq = new LinkedList<>();
        dq.add(tmp);

        int r, c, tr, tc;
        while (!dq.isEmpty()) {
            tmp = dq.pollFirst();

            r = tmp[0];
            c = tmp[1];
            for (int d=0; d < 4; d++) {
                tr = r+dr[d];
                tc = c+dc[d];

                if (tr < 0 || tc < 0 || tr >= R || tc >= C) continue;
                if (board[tr][tc] == 0) continue;
                if (visit[tr][tc] != 0) continue;
                visit[tr][tc] = visit[r][c] + 1;

                if (tr == R-1 && tc == C-1) return visit[tr][tc];

                tmp = new int[2];
                tmp[0] = tr;
                tmp[1] = tc;

                dq.add(tmp);
            }
        }

        return -1;
    }

    public int solution(int[][] maps) {
        R = maps.length;
        C = maps[0].length;

        visit = new int[R][C];

        return bfs(maps);
    }
}
```

