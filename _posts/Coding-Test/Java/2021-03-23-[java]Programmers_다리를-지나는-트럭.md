---
layout: post
title: "[Java]Programmers_다리를 지나는 트럭"
categories:
  - Coding-Test
  - Java
tags:
  - Queue
created_at: 2021-03-23T19:09:00+09:00
modified_at: 2021-03-23T19:09:00+09:00
visible: true
---



[Programmers 다리를 지나는 트럭](https://www.acmicpc.net/problem/42583)

```java
package Solutions;

import java.util.LinkedList;
import java.util.Queue;

public class 다리를_지나는_트럭 {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int time = 0;
        Queue<Integer[]> movingTruck = new LinkedList<>();
        Queue<Integer> waitingTruck = new LinkedList<>();

        for (int w: truck_weights) {
            waitingTruck.add(w);
        }

        while (!movingTruck.isEmpty() || !waitingTruck.isEmpty()) {
            time++;

            if (!movingTruck.isEmpty() && time - movingTruck.peek()[0] == bridge_length) {
                weight += movingTruck.peek()[1];
                movingTruck.poll();
            }

            if (!waitingTruck.isEmpty() && weight - waitingTruck.peek() >= 0) {
                Integer[] truck = {time, waitingTruck.poll()};

                weight -= truck[1];

                movingTruck.add(truck);
            }
        }

        return time;
    }
}
```

