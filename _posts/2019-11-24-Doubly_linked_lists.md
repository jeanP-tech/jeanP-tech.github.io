---



layout: post

title: "[Python] 양방향 연결 리스트 (Doubly Linked Lists)"

comment: true

tags:
- 자료구조
- 연결리스트
- 양방향연결리스트

categories: [Data Structure]
---

## 양방향 연결 리스트 (Doubly linked lists)

- 단방향 연결 리스트는 역방향 탐색이 쉽지 않다. 또한 단방향(head) 쪽으로만 삽입, 삭제, 조회가 가능.
	- 이를 해결하려면? 양방향 이동 구현
	- 다음 노드와 이전 노드의 이동이 가능하도록 구성

![doblylinkedlists](https://wikidocs.net/images/page/34342/02c%EC%9D%B4%EC%A4%91%EC%97%B0%EA%B2%B0%EB%A6%AC%EC%8A%A4%ED%8A%B8%EA%B8%B0%EB%B0%98.png)
<center>(출처: wikidocs)</center>
- 단일 연결 리스트보다 손상에 강하다


```
# 노드 구조 확장
class Node:

    def __init__(self, item):
        self.data = item
        self.next = None
        self.prev = None


class LinkedList:

    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = Node(None)
        self.head.prev = None
        self.head.next = self.tail
        self.tail.prev = self.head
        self.tail.next = None

    def traverse(self):
        result = []
        curr = self.head
        while curr.next.next: # self.tail 에 dummy node를 놓으므로
            curr = curr.next
            result.append(curr.data)
        return result

    def reverse(self):
        result = []
        curr = self.tail
        while curr.prev.prev:
            curr = curr.prev
            result.append(curr.data)
        return result


    def getAt(self, pos):
        if pos < 0 or pos > self.nodeCount + 1:
            raise IndexError
        if pos > self.nodeCount // 2:
            i = 0
            curr = self.tail
            while i < self.nodeCount - pos + 1:  
                curr = curr.prev
                i += 1
        else:
            i = 0
            curr = self.head
            while pos > i:
                curr = curr.next
                i += 1
        return curr


    def insertBefore(self, next, newNode):
        prev = next.prev
        newNode.prev = prev
        prev.next = newNode
        newNode.next = next
        next.prev = newNode
        self.nodeCount += 1
        return True


    def insertAfter(self, prev, newNode):
        next = prev.next
        prev.next = newNode
        newNode.prev = prev
        next.prev = newNode
        newNode.next = next
        self.nodeCount += 1
        return True


    def insertAt(self, pos, newNode):
        if pos < 1 or pos > self.nodeCount + 1:
            return False
        prev = getAt(pos-1)
        return insertAfter(prev, newNode)


    def popAfter(self, prev):
        curr = prev.next
        prev.next = curr.next
        curr.next.prev = prev
        self.nodeCount -= 1
        return curr.data


    def popBefore(self, next):
        prev = next.prev
        prev.prev.next = next
        next.prev = prev.prev
        self.nodeCount -= 1
        return prev.data

    def popAt(self, pos):
        if pos < 0 or pos > self.nodeCount:
            raise IndexError
        if self.nodeCount == 0:
            raise IndexError
        prev = self.getAt(pos-1)
        return self.popAfter(prev)

```
