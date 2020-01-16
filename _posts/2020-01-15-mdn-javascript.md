---



layout: post

title: "MDN JavaScript 첫걸음 공부하면서 정리"

comment: true

tags:
- 자바스크립트
- JavaScript
- Web
- 기초

categories: [Web]

---

MDN의 JavaScript 첫걸음에서 'JavaScript가 뭔가요?' 부분을 혼자 공부하면서 정리한 내용입니다.  
출처: https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps


- html: 웹 컨텐츠를 문단, 제목, 표 등으로 정의하고 부여하는 마크업 언어 
(마크업 언어란? 태그 등을 이용하여 언어나 데이터의 구조를 명시하는 언어)
- css: html 컨텐츠를 꾸며주는 스타일 규칙 언어
- Javascript: 동적으로 컨텐츠를 바꾸는 스크립트 언어 (스크립트 언어란? 기존에 이미 존재하는 소프트웨어를 제어하기 위한 언어)

## 코어 자바스크립트 언어 기반의 기능성
- Application Programming Interfaces (APIs)
- API는 이미 만들어진 코드의 집합체
   
     
- Browser API는 웹 브라우저에 설치된 API.
	- DOM (Document Object Model) API :HTML과 CSS를 알맞게 조정
	- Geolocation API : 지리적인 정보 검색
	- Canvas, WebGL: 2D와 3D 그래픽을 만들 수 있게 함
- Third party API: 브라우저에 기본적으로 설치된 API가 아닌 인터넷에서 개인적으로 프로그래밍한 것
	- Twitter API: 웹사이트에 가장 최근의 트윗을 보여줌
	- Google Maps API, OpenStreetMap API: 웹사이트에 원하는 지도를 넣어주고 추가기능 지원

## 웹 페이지에서 JavaScript는 어떤 일을 하는가?
- 브라우저에서 웹페이지를 불러올 때, 브라우저 안에서 HTML, CSS, Javascript 코드가 실행됨
- html과 css가 결합되고 웹페이지 상에 올려진 후, 브라우저의 스크립트 엔진에 의해 자바스크립트가 실행됨
- 자바스크립트는 해석형 언어이다. 코드가 순차적으로 실행되고 그 결과가 즉시 반환. 브라우저에서 동작하기 전에 코드를 변환할 필요가 없음. 

## 인라인 JavaScript 처리기
```
<button onclick="createParagraph()">Click me!</button>
```
- 이 방법은 효율적이지 않음. html 소스를 복잡하게 하고 모든 버튼마다 onclick 속성을 포함해야 함. 

## 스크립트의 로딩 방법
- 자바스크립트가 html 요소보다 먼저 실행된다면 조작할 요소가 존재하지 않기에 작동하지 않을 것. 
- 내부 자바스크립트 예제 해결 방법
```
document.addEventListener("DOMContentLoaded", function() {
  ...
});
``` 
"DOMContentLoad" 이벤트가 발생했을 때 function()을 실행한다는 의미. 
- 외부 자바스크립트 해결 방법
`<script src="script.js" async></script>`
async 속성 사용. 비동기방식으로 <script> 태그에 도달했을 때 브라우저에게 html 요소를 멈추지 않고 다운받도록 유지시킨다.
  
(웹 개발시 실제로 겪었던 에러이고, async 속성을 통해 해결했었다.)

### async & defer 
위 문제를 해결하기 위한 두 가지 방법. 
- async는 페이지 렌더링 중단 없이 스크립트를 다운로드 하고, 다운로드가 끝나자마자 이를 실행시킴. async는 각각의 스크립트가 독립적으로, 서로에게 의존하지 않는 관계일 때 적절. 

```
<script async src="js/vendor/jquery.js"></script>

<script async src="js/script2.js"></script>

<script async src="js/script3.js"></script>
```
3개의 스크립트를 로딩하지만 이들의 순서는 보장할 수 없다.
- defer는 이와 다르게 순서대로 다운로드 한 후 모든 스크립트와 내용이 다운로드 되었을 때 실행됨.
