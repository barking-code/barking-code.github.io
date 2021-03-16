---
layout: post
title: "[Python]Programmers_오픈채팅방"
categories:
  - Coding-Test
  - Python
tags:
  - String
created_at: 2021-03-16T14:58:00+09:00
modified_at: 2021-03-16T14:58:00+09:00
visible: true
---



[Programmers 오픈채팅방](https://programmers.co.kr/learn/courses/30/lessons/42888)

```python
def solution(record):
    _in = '님이 들어왔습니다.'
    _out = '님이 나갔습니다.'
    ans = []
    
    users = dict()
    for r in record:
        r = r.split()
        
        if len(r) == 2:
            op, user = r
            ans.append([user, _out])
        else:
            op, user, name = r
        
            if op == 'Enter':
                ans.append([user, _in])
        
            users[user] = name
    
    return [*map(''.join, map(lambda x: (users[x[0]], x[1]), ans))]
```
