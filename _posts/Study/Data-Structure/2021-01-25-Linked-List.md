---
layout: post
title: "4. Doubly Linked List"
categories:
  - Study
  - Data-Structure
tags:
  - Data Structure
  - Linked List
created_at: 2021-01-25T22:17:00+09:00
modified_at: 2021-01-25T22:17:00+09:00
visible: true
---

## Doubly Linked List란?

* Linked List가 한쪽 방향으로 연결된 자료구조라면 Doubly Linked List는 양쪽 방향 모두 연결된 자료구조이다.



## JAVA

##### 이중 연결 리스트로 구현한 Deque

```java
public class Deque_Linked<T> extends DataStructure {
    private Node<T> head = null;
    private Node<T> tail = null;
    private int size = 0;

    private class Node<T> {
        private Node<T> prev;
        private Node<T> next;
        private T data;
    
        public Node(Node<T> prev, Node<T> next, T data) {
            this.prev = prev;
            this.next = next;
            this.data = data;
        }

        public Node<T> getPrev() {
            return prev;
        }

        public void setPrev(Node<T> prev) {
            this.prev = prev;
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

    public void pushLeft(T data) {
        Node<T> node = new Node<>(null, this.head, data);

        if (this.head != null) {
            this.head.setPrev(node);
        }

        this.head = node;
        if (this.tail == null) {
            this.tail = node;
        }

        this.size++;
    }

    public void pushRight(T data) {
        Node<T> node = new Node<>(this.tail, null, data);

        if (this.tail != null) {
            this.tail.setNext(node);
        }

        this.tail = node;
        if (this.head == null) {
            this.head = node;
        }

        this.size++;
    }

    public T popLeft() {
        if (this.head == null) return null;

        T data = this.head.getData();

        this.head = this.head.getNext();
        if (this.head == null) {
            this.tail = null;
        } else {
            this.head.setPrev(null);
        }

        this.size--;

        return data;
    }
    
    public T popRight() {
        if (this.tail == null) return null;

        T data = this.tail.getData();

        this.tail = this.tail.getPrev();
        if (this.tail == null) {
            this.head = null;
        } else {
            this.tail.setNext(null);
        }

        this.size--;
        
        return data;
    }

    public T head() {
        return this.head.data;
    }

    public T tail() {
        return this.tail.data;
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
        
        return "Stack [ "+ bf.toString() +"]";
    }
}
```
