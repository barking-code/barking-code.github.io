---
layout: post
title: "3. Linked List"
categories:
  - Study
  - Data-Structure
tags:
  - Data Structure
  - Linked List
created_at: 2021-01-25T21:01:00+09:00
modified_at: 2021-01-25T21:01:00+09:00
visible: true
---

## Linked List란?

* 데이터와 포인터를 가진 Node를 연결하여 연속적으로 이어놓은 자료구조이다.
* Stack, Queue와 같은 자료구조를 만들때 사용한다.



### VS Array

1. 메모리

   * 배열은 index로 데이터에 접근하기 위해 연속적인 메모리 주소를 할당받아야 한다. 임의로 크기를 늘리는 것이 불가능하다.
   * Linked List는 Node간의 연결로 생성하기 때문에 Node를 생성할 수 있는 메모리 주소만 있으면 무한히 연결시켜 늘리는 것이 가능하다.
   * 배열은 메모리를 연속적으로 할당하기 때문에 주소를 저장할 공간이 필요없어 상대적으로 적은 메모리를 사용한다.
   * 연결 리스트는 값과 함께 다음 값이 저장된 메모리의 주소 또한 저장해야 하기 때문에 더 많은 메모리를 차지한다.

2. 접근방법

   * 배열은 연속적인 메모리 공간에 할당되어 있기 때문에 임의의 index와 함께 배열의 메모리 주소를 통해 O(1)의 시간으로 값에 접근이 가능하다.
   * 연결 리스트는 처음부터 원하는 인덱스까지 하나하나 탐색해 나가야 하기 때문에 O(n)의 시간으로 값에 접근이 가능하다.

   * 배열은 값의 삭제시 뒤에 있는 값을 하나하나 앞으로 당겨와 빈 공간을 채워야 하기 때문에 시간이 오래 걸린다.
   * 연결 리스트는 삭제할 Node간의 연결을 끊고 다음 노드와 이어주기만 하면 되기 때문에 상대적으로 시간이 적게 걸린다.



## JAVA

1. 연결 리스트로 구현한 Stack

```java
public class Stack_Linked<T> extends DataStructure {
    private Node<T> top = null;
    private int size = 0;

    // 값과 이전에 삽입된 자료의 주소 저장이 가능한 Node
    private class Node<T> {
        private Node<T> prev;
        private T data;
    
        public Node(Node<T> prev, T data) {
            this.prev = prev;
            this.data = data;
        }

        public Node<T> getPrev() {
            return prev;
        }
    
        public T getData() {
            return data;
        }
    }

    public void push(T data) {
        Node<T> node = new Node<>(top, data);

        this.top = node;
        this.size++;
    }

    public T pop() {
        if (this.top == null) return null;

        T data = this.top.getData();

        this.top = this.top.getPrev();
        this.size--;
        return data;
    }
    
    public T top() {
        if (this.top == null) return null;
        return this.top.getData();
    }

    public boolean isEmpty() {
        return this.top == null;
    }
    
    @Override
    public int size() {
        return this.size;
    }

    @Override
    public String toString() {
        StringBuffer bf = new StringBuffer();

        Node<T> node = this.top;
        while (node != null) {
            bf.insert(0, " ");
            bf.insert(0, node.getData());
            node = node.getPrev();
        }
        
        return "Stack [ "+ bf.toString() +"]";
    }
}
```



2. 연결 리스트로 구현한 Queue

```java
public class Queue_Linked<T> extends DataStructure {
    private Node<T> head = null;
    private Node<T> tail = null;
    private int size = 0;

    private class Node<T> {
        private Node<T> next;
        private T data;
    
        public Node(Node<T> next, T data) {
            this.next = next;
            this.data = data;
        }
    
        public Node<T> getNext() {
            return next;
        }
    
        public void setNext(Node<T> next) {
            this.next = next;
        }
    
        public T getData() {
            return data;
        }
    } 

    public void push(T data) {
        Node<T> node = new Node<>(null, data);

        if (this.head == null) {
            this.head = node;
            this.tail = node;
        } else {
            this.tail.setNext(node);
        }
        
        this.tail = node;
        this.size++;
    }

    public T pop() {
        if (this.head == null) return null;

        T data = this.head.getData();

        this.head = this.head.getNext();
        this.size--;

        if (this.head == null) {
            this.tail = null;
        }

        return data;
    }

    public T head() {
        if (this.head == null) return null;
        return this.head.getData();
    }

    public T tail() {
        if (this.tail == null) return null;
        return this.tail.getData();
    }
    
    public boolean isEmpty() {
        return this.head == null;
    }

    @Override
    public int size() {
        return this.size;
    }

    @Override
    public String toString() {
        StringBuffer bf = new StringBuffer();
        
        Node<T> node = this.head;
        while (node != null) {
            bf.append(node.getData());
            bf.append(" ");
            node = node.getNext();
        }
        
        return "Queue [ "+ bf.toString() +"]";
    }
}
```

