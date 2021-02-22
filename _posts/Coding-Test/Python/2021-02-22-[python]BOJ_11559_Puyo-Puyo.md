---
layout: post
title: "[Python]BOJ_11559_Puyo Puyo"
categories:
  - Coding-Test
  - Python
tags:
  - Simulation
  - DFS
created_at: 2021-02-22T16:36:00+09:00
modified_at: 2021-02-22T16:36:00+09:00
visible: true
---



[BOJ 11559 Puyo Puyo](https://www.acmicpc.net/problem/11559)

```python
from sys import stdin

dr = [-1, 0, 1, 0]
dc = [0, 1, 0, -1]

def solution():
    def boom():
        visit = [[0 for _ in range(6)] for _ in range(12)]

        ret = False
        for r in range(12):
            for c in range(6):
                if board[r][c] == ".": continue
                if visit[r][c] == ".": continue

                visit[r][c] = 1

                ret = max(DFS((r, c), board[r][c], visit), ret)
        
        return ret


    def DFS(cor, color, visit):
        stack = [cor]

        block_set = [cor]
        while stack:
            r, c = stack.pop()

            for d in range(4):
                tr, tc = r+dr[d], c+dc[d]

                if not (0 <= tr < 12 and 0 <= tc < 6): continue
                if visit[tr][tc]: continue
                if board[tr][tc] != color: continue

                visit[tr][tc] = 1

                block_set.append((tr, tc))
                stack.append((tr, tc))
        
        if len(block_set) < 4: return False

        for r, c in block_set:
            board[r][c] = "."

        return True

    def gravity():
        for c in range(6):
            for r in range(11, -1, -1):
                if board[r][c] != ".": continue
                for tr in range(r-1, -1, -1):
                    if board[tr][c] == ".": continue
                    board[r][c], board[tr][c] = board[tr][c], board[r][c]
                    break


    board = [[*stdin.readline().strip()] for _ in range(12)]
    
    cnt = 0
    while boom():
        gravity()
        cnt += 1
    
    print(cnt)

solution()
```

