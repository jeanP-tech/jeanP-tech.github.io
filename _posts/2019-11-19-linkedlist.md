---



layout: post

title: "[Python] 연결 리스트 (Linked Lists) - 단순 연결, Dummy Node"

comment: true

tags:
- 자료구조
- 연결리스트

categories: [Data Structure]
---
> 프로그래머스의 자료구조 강의를 들은 뒤, 인터넷의 여러 자료를 참고해 재구성한 내용입니다.

### 연결 리스트란?
- 앞에 있는 것이 뒤에 있는 것을 가리키도록 연결된 자료구조
- 각각의 아이템을 노드(Node)라고 부른다
    - 노드는 Data와 Link를 담고 있음
    - 노드 내의 데이터는 다른 구조로 이루어질 수 있다

### 배열과의 차이점
 배열 | 연결 리스트
 --- | ---
연속한 저장 공간 위치 | 임의의 위치
특정 원소 지칭 매우 간편 O(1) | 불편. 선형탐색과 유사O(n)
데이터의 추가/삭제가 불편|데이터의 추가/삭제가 용이
크기를 키우기 어려움| 용이
정적인 자료 구조 | 동적인 자료 구조

## 단순 연결 리스트 (Singly Linked List)
- 노드를 한 방향으로 연결하는 자료구조

###Node
```
class Node:
	def __init__(self, item):
    	self.data = item
        self.next = None

class LinkedList:
	def __init__(self):
    	self.nodeCount = 0
        self.head = None
        self.tail = None
```

### 특정 원소 참조
```
def getAt(self, pos):
	if pos <= 0 or pos > self.nodeCount:
    	return None
    i = 1
    curr = self.head
    while i < pos:
    	curr = curr.next
        i += 1
    return curr
```
### 원소의 삽입
```
def insertAt(self, pos, newNode):
	if pos < 1 or pos > self.nodeCount + 1:
    	return False
    if pos == 1:
    	newNode.next = self.head
        self.head  = newNode
    else:
    	prev = self.getAt(pos-1)
       	newNode.next = prev.next
        prev.next = newNode
    if pos == self.nodeCount + 1
        self.tail = newNode
    self.nodeCount += 1
    return True

```
### 원소의 삭제
삭제하려는 데이터를 data에 저장해두고, 삭제가 완료되면 True를 return
```
def popAt(self, pos):
	if pos < 1 or pos > self.nodeCount:
    	return False
    elif pos == 1 and self.nodeCount == 1:
    	data = self.head.data
        self.head = None
        self.tail = None
    else:
    	prev = self.getAt(pos-1)
        data = prev.next.data
        if pos == self.nodeCount:
        	self.tail = prev
            prev.next = None
        else:
        	prev.next = prev.next.next
    self.nodeCount -= 1
    return True
```

### Dummy Node
- '특정 원소'를 삽입/삭제하는 코드가 아니라, '특정 원소의 다음'을 삽입/삭제하는 코드를 짠다면?
- 맨 앞 원소를 삽입하고 제거하기 힘들어짐
	- -> 맨 앞에 더미 노드 추가
	- 더미 노드: 실제로 데이터를 가지지는 않고, 구현의 편의를 위해 두는 무의미한 노드

### 코드 구현
```
class Node:

    def __init__(self, item):
        self.data = item
        self.next = None


class LinkedList:

    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = None
        self.head.next = self.tail


    def traverse(self):
        result = []
        curr = self.head
        while curr.next:
            curr = curr.next
            result.append(curr.data)
        return result


    def getAt(self, pos):
        if pos < 0 or pos > self.nodeCount + 1:
            raise IndexError

        i = 0
        curr = self.head
        while i < pos:
            curr = curr.next
            i += 1

        return curr


    def insertAfter(self, prev, newNode):
        newNode.next = prev.next
        if prev.next == None:
            self.tail = newNode
        prev.next = newNode
        self.nodeCount += 1
        return True


    def insertAt(self, pos, newNode):
        if pos < 1 or pos > self.nodeCount + 1:
            return False
        if pos != 1 and pos == self.nodeCount + 1:
            prev = self.tail
        else:
            prev = self.getAt(pos-1)
        return self.insertAfter(prev, newNode)


    def popAfter(self, prev):
        if prev.next == None:
            return None
        curr = prev.next
        if curr.next == None:
            self.tail = prev

        prev.next = curr.next
        self.nodeCount -= 1
        return curr.data


    def popAt(self, pos):
        if pos < 1 or pos > self.nodeCount + 1:
            raise IndexError
        prev = self.getAt(pos-1)
        return self.popAfter(prev)

```
