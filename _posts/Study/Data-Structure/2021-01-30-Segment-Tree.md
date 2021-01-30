---
layout: post
title: "6. Segment Tree"
categories:
  - Study
  - Data-Structure
tags:
  - Data Structure
  - Tree
created_at: 2021-01-30T21:47:00+09:00
modified_at: 2021-01-30T21:47:00+09:00
visible: true
---

## Segment Tree란?

* 선형 자료구조에서 특정 구간의 합을 빠른 시간안에 구할 수 있도록 고안된 이진 트리
* 원래 데이터의 특정 구간의 합을 저장해 놓은 노드를 생성하여 각 노드의 합으로 원하는 구간의 합을 도출 해 낼 수 있다.
* 반대로 원래 데이터의 특정 인덱스의 값이 수정된 경우 해당 인덱스의 값이 포함된 노드만 찾아 수정하여 빠른 수정이 가능하다.



### 구현방법

1. data = int[n]의 경우 2^m 이면서 길이가 n보다 큰 새로운 배열(segmentT = new int[n*4])을 생성한다.
   * n < 2^m < n * 4

2. segmentT[1]에 data[0] ~ data[n-1]까지 더한 값을 저장한다.
3. segmentT[1 * 2], segmentT[1 * 2 + 1]에 각각 data[0] ~ data[(n-1) / 2], data[(n-1) / 2 + 1] ~ data[n-1]까지 더한 값을 저장한다.
4. 즉, 부모 노드의 구간의 합을 자식노드가 반씩 나눠 저장한다.
   * 부모 노드가 5 ~ 10 까지의 합을 가지고 있다면, 왼쪽 자식 노드는 5 ~ 7, 오른쪽 자식 노드는 8 ~ 10까지의 합을 가지고 있는다.
5. 리프 노드가 자기 자신의 값을 가질때까지 반복한다.
   * segmentT[i]가 data[j]의 값을 가질때까지



### 구간의 합을 구하는 방법

0. data = int[10], 합을 알고싶은 구간이 3 ~ 7인 경우(start = 3, end= 7)

1. segmentT[1]부터 탐색을 시작한다.
2. segmentT[1]은 0 ~ 9까지의 값을 가지고 있기 때문에 하위노드로 내려간다(l = 0, r = 9).
3. segmentT[2]는 0 ~ 4, segmentT[3]은 5 ~ 9까지의 값을 가지고 있기때문에 다시 아래로 내려간다.
4. segmentT[4]는 0 ~ 2 즉, 우리가 알고싶어하는 3 ~ 7 구간 밖이기 때문에 더하지않는다.(r(2) < start(3))
5. segmentT[5]는 3 ~ 4 즉, 우리가 알고싶어하는 3 ~ 7구간안에 **완전히** 포함되기 때문에 더해준다.(start(3) <= l(3) && r(4) <= end(7))
6. segmentT[6]은 5 ~ 7 즉, 우리가 알고싶어하는 3 ~ 7구간안에 **완전히** 포함되기 때문에 더해준다.(start(3) <= l(5) && r(7) <= end(7))
7. 이를 일반적으로 표현하면 다음과 같다
   * segmentT[i]가 합을 가지고 있는 구간이 알고싶은 구간을 **완전히** 벗어나는 경우 더해주지 않는다.
   * segmentT[i]가 합을 가지고 있는 구간이 알고싶은 구간과 일부 걸치는 경우 하위노드를 탐색한다.
   * segmentT[i]가 합을 가지고 있는 구간이 알고싶은 구간에 **완전히** 포함되는 경우 더한다.
   * 이를 맨위 노드 segmentT[1]부터 시작해서 재귀적으로 하위노드를 탐색한다.



### 구간의 합을 수정하는 방법

0. data = int[10], data[3] = 7 => 5로 바꾸고 싶은 경우
1. 바꾸고싶은 값(5) - 원래 데이터의 값(7) = 차이(-2)를 변경된 인덱스의 합을 가지고 있는 구간을 탐색하여 전부 변경해준다.
2. segmentT[1]부터 탐색을 시작한다.(l = 0, r = 9)
3. segmentT[1]은 0 ~ 9까지의 값을 가지고 있기 때문에 3이 포함되어 있으므로 값을 변경해주고 하위노드를 탐색한다.(segmentT[1] += diff)
4. segmentT[2]는 0 ~ 4 까지의 값을 가지고 있기때문에 3이 포함되어 있으므로 값을 변경해주고 하위노드를 탐색한다.(segmentT[2] += diff)
5. segmentT[3]은 5 ~ 9 까지의 값을 가지고 있기때문에 3이 포함되지 않으므로 값도 변경하지 않고 하위노드도 탐색하지 않는다.
6. segmentT[4]는 0 ~ 2 까지의 값을 가지고 있기때문에 3이 포함되지 않으므로 값도 변경하지 않고 하위노드도 탐색하지 않는다.
7. segmentT[5]는 3 ~ 4 까지의 값을 가지고 있기때문에 3이 포함되어 있으므로 값을 변경해주고 하위노드를 탐색한다.(segmentT[3] += diff)
8. segmentT[10]은 3 의 값을 가지고 있기때문에 3이 포함되어 있으므로 값을 변경해주고 하위노드가 없으므로(l == r) 탐색을 종료한다.
9. segmentT[11]은 4 의 값을 가지고 있기때문에 3이 포함되지 않으므로 값도 변경하지 않고 하위노드도 탐색하지 않는다.
10. 이를 일반적으로 표현하면 다음과 같다.
    * 변경하고자 하는 data의 인덱스가 segmentT[i]가 합을 가지고 있는 구간을 포함하는 경우 원래 값과 변경하고자 하는 값의 차이만큼 더해준다.
    * 변경 후, 만약 하위 노드가 존재하는 경우 탐색한다.
    * 변경하고자 하는 data의 인덱스가 segmentT[i]가 합을 가지고 있는 구간을 포함하지 않는 경우 탐색을 종료한다.



## JAVA

```java
public class Segment_Tree {
    private int[] arr;
    private int[] data;
    private int dataLen;
    private int maxSize;
    private int depth;
    
    public Segment_Tree(int[] data) {
        this.dataLen = data.length;
        this.data = data;

        this.arr = new int[this.dataLen * 4];
        this.maxSize = this.dataLen * 4 - 1;
        
        int d = 1;
        while (Math.pow(2, d+1) <= this.maxSize) {
            d++;
        }
        this.depth = d;

        setSegmentSumData(0, this.dataLen-1, 1);
    }

    private void setSegmentSumData(int dataS, int dataE, int i) {
        if (dataS == dataE) {
            this.arr[i] = this.data[dataS];
        } else {
            int dataM = (dataE - dataS) / 2 + dataS;
            setSegmentSumData(dataS, dataM, i * 2);
            setSegmentSumData(dataM+1, dataE, i * 2 + 1);
            this.arr[i] = this.arr[i*2] + this.arr[i*2+1];
        }
    }

    public int findSum(int startIndex, int endIndex) {
        return findSum(0, this.dataLen-1, 1, startIndex, endIndex);
    }

    private int findSum(int sumBoundaryL, int sumBoundaryR, int i, int startIndex, int endIndex) {
        // sumBoundaryL ~ sumBoundaryR 의 합이 this.arr[i]
        // 구하려는 구간이 현재 노드가 가지고 있는 합의 바깥구간일 경우 더하지않음
        if (startIndex > sumBoundaryR || endIndex < sumBoundaryL) return 0;

        // 구하려는 구간안에 현재 노드가 가지고 있는 합의 구간이 포함된 경우 더해줌 
        if (startIndex <= sumBoundaryL && endIndex >= sumBoundaryR) return this.arr[i];

        // 구하려는 구간이 현재 노드가 가지고 있는 합의 구간과 걸친 경우 합의 구간이 모두 포함될때까지 아래노드로 내려감
        int sumBoundaryM = (sumBoundaryR - sumBoundaryL) / 2 + sumBoundaryL;

        return findSum(sumBoundaryL, sumBoundaryM, i * 2, startIndex, endIndex) + findSum(sumBoundaryM + 1, sumBoundaryR, i * 2 + 1, startIndex, endIndex);
    }

    public void update(int target, int data) {
        int diff = data - this.data[target];

        this.data[target] = data;
        
        update(0, this.dataLen - 1, 1, diff, target);
    }

    private void update(int sumBoundaryL, int sumBoundaryR, int i, int diff, int target) {
        // 현재 노드가 target에 대한 정보를 가지고 있는 경우 diff를 갱신
        if (target >= sumBoundaryL && target <= sumBoundaryR) {
            this.arr[i] += diff;
        }

        // 앞으로 탐색할 하위노드가 남아있는 경우 하위 노드를 재귀적으로 갱신
        if (sumBoundaryL < sumBoundaryR) {
            int sumBoundaryM = (sumBoundaryR - sumBoundaryL) / 2 + sumBoundaryL;
            update(sumBoundaryL, sumBoundaryM, i * 2, diff, target);
            update(sumBoundaryM + 1, sumBoundaryR, i * 2 + 1, diff, target);
        }
    }

    @Override
    public String toString() {
        int level = 1;
        StringBuffer bf = new StringBuffer();

        int i = 1;
        while (level <= this.depth) {
            for (int l=0; l < depth-level; l++) {
                bf.append(" ");
            }
            while (i < Math.pow(2, level)) {
                if (this.arr[i] == 0) {
                    bf.append("_ ");
                } else {
                    bf.append(this.arr[i] + " ");
                }
                i++;
            }
            bf.append("\n");
            level++;
        }

        return bf.toString();
    }
}
```


