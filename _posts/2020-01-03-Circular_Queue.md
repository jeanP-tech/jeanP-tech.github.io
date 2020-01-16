---



layout: post

title: "[Python] 환형 큐 (Priority Queues) (2)"

comment: true

tags:
- 자료구조
- 큐
- 환형큐
- 원형큐
- 파이썬
- 정리
- 개인공부

categories: [Data Structure]
---
> 프로그래머스 자료구조 강의와 각종 인터넷 자료를 참고하여 재구성한 내용입니다.

## Circular Queue
- Linear queue에서는 큐가 꽉 차면 dequeu를 하더라도 새 element를 넣을 수 없다.
	- queue의 front를 옮기고 rear는 큐의 맨 뒤에 있기 때문에
- 이를 해결하기 위해서는 새롭게 시작하기 위해 queue를 reset해야 함
- Circular queue는 마지막에 큐를 끝내는 대신 새 포지션을 시작한다
![queue](https://www.studytonight.com/data-structures/images/linear-queue-full-2.png)
<center>(출처: studytonight)</center>

## Circular Queue의 기본 특징
1. head는 큐의 맨 앞을 가리키고, tail은 큐의 맨 끝을 가리킨다.
2. 처음 큐가 비었을 때 head와 tail은 같은 곳을 가리킨다
3. 새로 추가된 데이터는 tail이 가리켰던 위치로 추가된다. tail은 다음 위치를 가리킨다.
4. 환형 큐에서 데이터는 실질적으로 삭제되지 않는다. dequeue가 실행될 때 head 포인터만 한 칸 증가한다. 큐 데이터는 head와 tail 사이에 있는 것만 포함되므로 그 바깥에 있는 데이터는 더이상 큐의 일부분이 되지 않는다.
5. head와 tail은 큐의 맨 끝에 다다를 때 0으로 초기화된다.
6. head와 tail은 서로 cross할 수 있다. 즉, head pointer가 tail보다 커질 수 있다. 이는 dequeue를 몇 회 시행하고 tail이 다시 초기화 될 때 일어난다.

## Circular Queue 구현
python list를 이용한 구현
```
class CircularQueue:

	def __init__(self, n):
        self.maxCount = n
        self.data = [None] * n
        self.count = 0
        self.front = -1
        self.rear = -1

    def size(self):
    	return self.count

    def isEmpty(self):
    	return self.count == 0

    def isFull(self):
    	return self.count == self.maxCount

    def enqueue(self, x):
    	if self.isFull():
        	raise IndexError('Queue full')
        self.rear = (self.rear + 1) % self.maxCount
        self.data[self.rear] = x
        self.count += 1

    def dequeue(self):
    	if self.isEmpty():
            raise IndexError('Queue empty')
        self.front = (self.front + 1) % self.maxCount
        x = self.data[self.front]
        self.count -= 1
        return x

    def peek(self):
    	if self.isEmpty():
        	raise IndexError('Queue empty')
        return self.data[(self.front+1) % self.maxCount]

```

## 참조
- 프로그래머스 ['어서와! 자료구조와 알고리즘은 처음이지?'](https://programmers.co.kr/learn/courses/57)
- StudytoNight [What is a Circular Queue?](https://www.studytonight.com/data-structures/circular-queue)
