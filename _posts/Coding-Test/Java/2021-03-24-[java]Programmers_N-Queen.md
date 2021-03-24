---
layout: post
title: "[Java]Programmers_N Queen"
categories:
  - Coding-Test
  - Java
tags:
  - Back Tracking
created_at: 2021-03-24T14:43:00+09:00
modified_at: 2021-03-24T14:43:00+09:00
visible: true
---



[Programmers N Queen](https://www.acmicpc.net/problem/12952)

```java
public class N_Queen {
    private boolean[][] board;
    private int total = 0;

    public int solution(int n) {
        board = new boolean[n][n];

        setPieces(0, n);
        return total;
    }

    private void setPieces(int r, int n) {
        if (r >= n) {
            total++;
            return ;
        }

        for (int c=0; c < n; c++) {
            if (isUsedColumn(c, n)) continue;
            if (isUsedDiagonal(r, c, n)) continue;
            board[r][c] = true;
            setPieces(r+1, n);
            board[r][c] = false;
        }
    }

    private boolean isUsedColumn(int c, int n) {
        for (int r=0; r < n; r++) {
            if (board[r][c]) return true;
        }

        return false;
    }

    private boolean isUsedDiagonal(int r, int c, int n) {
        int i = 1;
        // (r-i, c-i), (r+i, c+i), (r-i, c+i), (r+i, c-i)
        while (0 <= r-i || 0 <= c-i || r+i < n || c+i < n) {
            if (0 <= r-i && 0 <= c-i && board[r-i][c-i]) return true;
            if (r+i < n && c+i < n && board[r+i][c+i]) return true;
            if (0 <= r-i && c+i < n && board[r-i][c+i]) return true;
            if (r+i < n && 0 <= c-i && board[r+i][c-i]) return true;

            i++;
        }

        return false;
    }
}
```

