---
layout: post
title: "[Java]Programmers_카카오프렌즈 컬러링북"
categories:
  - Coding-Test
  - Java
tags:
  - BFS
created_at: 2021-03-24T18:25:00+09:00
modified_at: 2021-03-24T18:25:00+09:00
visible: true
---



[Programmers 카카오프렌즈 컬러링북](https://www.acmicpc.net/problem/1829)

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class 카카오프렌즈_컬러링북 {
    private int[] answer = new int[2];
    private int R, C;
    private boolean[][] visit;
    private int[] dr = {-1, 0, 1, 0};
    private int[] dc = {0, 1, 0, -1};

    private class Cor {
        public int r, c;
        public Cor(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }

    private int countAreaSize(int r, int c, int[][] board) {
        int color = board[r][c];
        Cor cor = new Cor(r, c);
        visit[r][c] = true;
        
        Deque<Cor> dq = new ArrayDeque<>();
        dq.add(cor);

        int cnt = 1;
        while (!dq.isEmpty()) {
            cor = dq.pollFirst();

            for (int d=0; d < 4; d++) {
                int tr = cor.r+dr[d];
                int tc = cor.c+dc[d];

                if (tr < 0 || tr >= R || tc < 0 || tc >= C) continue;
                if (board[tr][tc] != color) continue;
                if (visit[tr][tc]) continue;

                visit[tr][tc] = true;
                cnt++;

                Cor tmp = new Cor(tr, tc);
                dq.add(tmp);
            }
        }

        return cnt;
    }

    public int[] solution(int m, int n, int[][] picture) {
        R = m;
        C = n;
        visit = new boolean[R][C];

        for (int r=0; r < R; r++) {
            for (int c=0; c < C; c++) {
                if (visit[r][c]) continue;
                if (picture[r][c] == 0) continue;

                answer[0]++;
                answer[1] = Math.max(answer[1], countAreaSize(r, c, picture));
            }
        }

        return answer;
    }
}
```

