---



layout: post

title: "[Python] 이진 탐색 트리 (Binary Search Trees)"

comment: true

tags:
- 자료구조
- 트리
- trees
- 이진트리
- Binary Tree
- 추상적자료구조
- 파이썬
- 정리
- 개인공부

categories: [Data Structure]
---
> 프로그래머스 자료구조 강의와 각종 인터넷 자료를 참고하여 재구성한 내용입니다.

## 이진 탐색 트리
- 모든 노드에 대하여
	- 왼쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 작고
	- 오른쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 크고
	- 왼쪽과 오른쪽 서브트리 각각 역시 이진 탐색 트리여야 한다

## 목적
- 이진 탐색 트리는 이진 탐색(binary search)과 연결 리스트(linked lists)를 결합한 자료 구조의 일종
- 이진 탐색은 탐색에 소요되는 계산 복잡성이 O(logn)으로 빠르지만 자료 입력, 삭제가 불가능하다
- 연결 리스트는 자료 입력, 삭제에 필요한 계산 복잡성이 O(1)로 효율적이지만 탐색을 하는데는 O(n)의 계산 복잡성이 요구된다
- 이진 탐색 트리의 핵심 연산인 탐색, 삽입, 삭제의 계산 복잡성은 트리의 높이가 h일 때 O(h)이다
- 그러나 배열을 이용한 이진 탐색과 비교했을 때 공간 소요가 크다는 단점이 있다


## 코드 구현 - 초기화
```
class Node:
	def __init__(self, key, data):
    	self.key = key
        self.data = data
        self.left = None
        self.right = None
        
class BinSearchTree:
	def __init__(self):
    	self.root = None
```

## 원소 탐색 연산 구현 (lookup)
찾으려는 대상의 key를 입력 받아, 찾은 노드와 그 부모 노드를 return 한다.
```
class BinSearchTree:
	def lookup(self, key):
    	if self.root:
        	return self.root.lookup(key)
        else:
        	return None, None
            
class Node:
	def lookup(self, key, parent=None):
    	if key < self.key:
        	if self.left:
            	return self.left.lookup(key, self)
            else:
            	return None, None
        elif key > self.key:
        	if self.right:
            	return self.right.loopup(key, self)
            else:
            	return None, None
        else:
        	return self, parent
```

## 원소 삽입 연산 구현 (insert)
- 입력: key, 데이터 원소
- return: 없음

```
class BinSearchTree:
	def insert(self, key, data):
    	if self.root:
        	self.root.insert(key, data)
        else:
        	self.root = Node(key, data)

class Node:
	def insert(self, key, data):
    	if key < self.key:
        	if self.left:
				self.left.insert(key, data)
            else:
            	self.left = Node(key, data)
        elif key > self.key:
        	if self.right:
        		self.right.insert(key, data)
            else:
            	self.right = Node(key, data)
        else:
        	raise KeyError
```

## 원소 삭제 연산 구현 (remove)
- 지우려는 값이 leaf node에 있으면 그냥 삭제
- internal node일 경우
	- child node가 1개일 경우: 삭제되는 노드 자리에 그 자식을 배치
	- child node가 2개일 경우: 삭제되는 노드보다 바로 다음으로 큰 키를 가지는 노드를 찾아 그 노드를 대신 배치

```
# 자식의 개수를 알아야하므로 countChildren 메소드 생성
class Node:
	def countChildren(self):
    	count = 0
        if self.left:
        	count += 1
        if self.right:
        	count += 1
        return count

class BinSearchTree:
	def remove(self, key):
    	node, parent = self.lookup(key)
        if node:
        	nChldren = node.countChildren()
            if nChildren == 0:
            	if parent:
                	if node == parent.left:
                    	parent.left = None
                    else:
                    	parent.right = None
                else:
                	self.root = None
            elif nChildren == 1:
            	if node.left:
                	var = node.left
                else:
                	var = node.right
            	if parent:
                	if parent.left == node:
                    	parent.left = var
                    else:
                    	parent.right = var
                else:
                	self.root = var
            else:
            	parent = node
                successor = node.right
                while successor.left:
                	parent = successor
                    successor = successor.left
                node.key = successor.key
                node.data = successor.data
            	if successor == parent.left:
                	parent.left = successor.right
                else:
                	parent.right = successor.right
            return True
        else:
        	return False
            
```

## 참조
- 프로그래머스 ['어서와! 자료구조와 알고리즘은 처음이지?'](https://programmers.co.kr/learn/courses/57)

