---



layout: post

title: "[CSS] line-height를 이용한 텍스트 수직 중앙 정렬 (text vertical-align)"

comment: true

tags:
- vertical-align
- line-height
- 중앙정렬
- 수직정렬
- html
- css

categories: [WEB]
---

swim 웹을 제작할 때 수직정렬 때문에 애를 조금 먹었다.  
그 중 밑과 같은 문제가 발생했는데,
![image](https://user-images.githubusercontent.com/45560971/70289880-333e0780-17a4-11ea-9978-e164448f8829.PNG)
텍스트 background의 height를 조정했더니 수직 중앙 정렬이 안 되는 것.
여러 해결법을 찾긴 했지만, div를 이것저것 추가하고 싶지 않았기 때문에 가장 간단한 방법을 원했다.  

그렇게 발견한 것이 line-height를 통한 중앙 정렬.
해결법은 아주 쉬운데, 배경 박스의 높이와 글자의 line height를 똑같이 설정하면 된다.
```
.time_list h3{
  font-size: 30px;
  color: #ffffff;
  background-color: #0090ff;
  display: inline-block;
  height: 32px;
  line-height: 32px;
}
```

### 원리
![image](https://pearsonified.com/wp-content/uploads/2011/12/font-size-line-height.png)

line height에서 font size를 제외한 공간을 leading이라 한다.
여기서 line-height를 증가시키면 이 부분만 위 아래로 똑같이 늘어나게 된다.
