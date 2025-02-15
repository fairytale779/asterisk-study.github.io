---
title: "이희진 복습일지"
layout: post
comments: true
categories: [이희진/복습일지]
tags: []
---

### 221011 || URI vs URL
URI는 URL를 포함하는 상위개념이라 하나 둘의 차이가 명확하게 와닿지는 않는다.  
이 둘의 명확한 구분을 위해 좀 더 상세히 살펴보면 다음과 같다.  
먼저 URI는 통합 자원 식별자(Uniform Resource Identifier)의 약자로 논리적 및 물리적 리소스를 식별하는 고유한 문자열 시퀸스다.  
그럼 URL은 무엇일까? 통합 자원 위치 탐사기(Uniform Resource Locator)로 네트워크 상에서 리소스가 어디에 있는지 알려주는 규약이다.  
요약하면 URI는 식별을 하고 URL는 위치까지 가르킨다. 그렇기 때문에 URI이더라도 위치 정보가 없다면 URL이 될 수 없으므로 'URL은 URI이다'는 성립이 되지만 'URI는 URL이다'는 성립이 되지 못한다.  

즉, 한 가지 예를 들어 설명하면 다음과 같다.  
http://asterisk.com/user?id=123  
이 경우, '?id=123(query)'의 결과에 따라 특정 자원의 결과가 다르게 나올 수 있으므로 이를 식별자라 한다. 즉, 식별자 이전까지는 URL이라 할 수 있으나 식별자가 붙은 형태는 URL이라 할 수 없고 오로지 URI라고만 할 수 있다.  
<br />

### 221016 || express 라이브러리
express.js로 서버를 여는 건 어쩌면 node.js보다 간단할 수 있다. 그럼 express 라이브러리 설치 후 실행을 시키는 건 어떤 과정을 거칠까.
```js
const express = require('express');
const app = express();

app.listen(port, function(){실행할 코드});
```   
이게 하나의 기본 양식이다. 아래의 listen()을 통해 서버를 열 수 있는데 listen()에는 총 두 개의 인자가 들어간다. 하나는 서버를 띄울 포트, 하나는 서버를 열고 실행할 코드로 완성한다면 해당 포트로 접속했을 때 사용자가 마주할 페이지를 마음대로 설정할 수 있다. 또한 여기서 멈추지 않고 서버를 띄웠을 때 서버로 오는 다양한 요청들을 처리할 수 있어야 한다. 가장 보편적인 예로 사용자가 URL을 통해 GET 요청을 보냈을 때 요청에 맞춰 페이지 응답을 보낼 수 있어야 하는 것이다.  
```js
app.get( '경로', function(req, res){
   res.send('전달인자로 받은 경로로 접속했을 때 실행할 코드);
   }
```
만약 '/books'라는 경로에 도달했을 때 다양한 책의 목록이 나오는 페이지를 띄우고 싶다면 res.send()안에 원하는 페이지를 띄우는 코드를 작성하면 된다. 이것이 기본적인 express 라이브러리를 실행하는 틀이며 다양한 활용을 통해 동적인 페이지를 구성할 수 있다.  
<br />

### 221022 || DOM(1)
DOM은 정확히 무엇일까? 브라우저 렌더링 엔진이 HTML 문서를 파싱(일련의 문자열을 token 단위로 분해해 parse tree을 생성)하여 만든 자료 구조를 DOM이라 한다. HTML 요소들(태그, 어트리뷰트 이름 및 값, 콘텐츠)은 파싱을 통해 요소 노드 객체(요소 노드, 어트리뷰트 노드, 텍스트 노드)로 변환된다.

HTML 요소 간에는 중첩 관계가 있기 때문에 이 사이엔 부모-자식 관계가 형성이 되고 이를 기반으로 비선형(하나의 자료 뒤에 여러 개의 자료가 존재함) 자료구조 중 하나인 트리 자료구조가 생성된다.

파싱을 통해 형성된 DOM의 노드 객체는 총 12개가 있으며 이 중 중요한 노드 타입은 총 4개 있다.

1. 문서 노드(Document node)  
DOM 트리의 최상위에 존재하는 루트 노드인 document 객체를 의미한다. window.document 또는 document로 참조 가능하며 이때 window 객체는 하나의 전역 객체라 모든 자바 스크립트 코드가 공유하고 window의 document 프로퍼티에 바인딩 되어 있는 하나의 document 객체를 보게 된다. 따라서, HTML 문서당 window 객체는 유일하다. 문서 노드는 앞서 말했듯 루트 노드이기 때문에 요소, 어트리뷰트, 텍스트 등 다른 노드에 접근하기 위해서는 문서 노드를 꼭 거쳐야 한다. 이러한 특징 때문에 문서 노드는 진입점 역할을 담당한다 할 수 있다. 

2. 요소 노드(Element node)  
HTML 요소를 가리키는 객체로 해당 노드는 다른 노드와 부모-자식 관계를 가질 수 있고 이 관계를 통해 구조(트리 구조)화가 가능하다. 이 때문에 요소 노드는 문서의 구조를 표현한다고 할 수 있다. 

3. 어트리뷰트 노드(attribute node)  
어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체로 해당 노드에 접근하기 위해서는 요소 노드에 먼저 접근해야 한다. 이는 어트리뷰트 노드가 오로지 요소 노드에만 연결되어 있기 때문이다. 단, 여기서 주의해야 하는 것은 해당 연결은 상위로 연결된 게 아니라 동등한 위치에서 연결된 것으로 요소 노드와 어트리뷰트 노드의 관계는 부모-자식이라 할 수 없다.  

4. 텍스트 노드(Text node)  
HTML 요소의 텍스트를 가리키는 객체로 요소 노드가 문서의 구조라면 텍스트 노드는 문서의 내용을 의미한다. 텍스트 노드는 요소 노드의 자식 노드로 접근하기 위해선 요소 노드에 먼저 접근해야 하며 텍스트 노드는 본인의 자식 노드를 가질 수 없는 리프 노드다. 즉, DOM 트리의 최종단이라 할 수 있다.  
<br />

### 221030 || DOM(2)
HTML을 자바스크립트를 사용해 동적으로 제어하기 위해선 먼저 요소 노드를 취득해야 한다. 텍스트 노드도 어트리뷰트 노드도 결국 요소 노드와 연결되어 있으므로 이는 어떤 노드를 제어하려 해도 기본적으로 요소 노드에 먼저 접근해야 함을 알 수 있다. 요소 노드를 취득하는 방법은 총 4가지로 말할 수 있다.  

1. id 이용   
* document.prototype.getElementById() 메서드 : 인수로 전달한 id 값을 갖는 하나의 요소 노드 반환하며 만약 없을 시 null 반환함
```js
<ul>
  <li id='red'>빨강</li>
  <li id='blue'>파랑</li>
  <li id='green'>초록</li>
</ul>

<script>
 let useOfIdVal = document.getElementById('red') 
 // 이렇게 되면 useOfIdVal에 id 값이 'red'인 요소 노드가 할당됨
</script>
```
이때, HTML 요소에 id 값을 부여하면 해당 값이 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과가 발생한다. 하지만 id 값과 동일한 이름의 전역 변수가 이미 선언되어 있다면 이 변수에 노드 객체가 재할당되는 일은 발생하지 않는다. 
```js
<div id="happy">행복</dive> // 만 있을 경우 전역 변수 happy에는 해당 요소 노드(div)가 할당된다.

<div id="happy">행복</dive>
let happy = 'you' // 그러나 이렇게 동일한 변수명으로 변수 선언 및 할당이 되어 있는 경우 요소 노드가 할당되는 일은 없다.
``` 
   
2. 태그 이름 이용    
* document.prototype.getElementByTagName() 메서드 : 인수로 전달한 태그 이름을 갖는 모든 노드 요소를 HTMLCollection 객체로 반환함
```js
<ul>
  <li id='red'>빨강</li>
  <li id='blue'>파랑</li>
  <li id='green'>초록</li>
</ul>

<script>
 let useOfTagName = document.getElementByTagName('li') 
 // 이렇게 되면 <li>에 해당하는 모든 요소 노드에 대한 HTMLCollection(DOM 컬렉션 객체로 유사 배열 객체) 객체가 반환됨
</script>
```
이때 document 자리에 특정 요소 노드를 넣어 호출이 가능한데 이럴 경우 특정 요소 노드의 자손 노드 중에서 탐색해 반환한다.   

3. class 이용
* document.prototype.getElementsByClassName() 메서드 : 인수로 전달한 class 값을 갖는 모든 요소 노드를  HTMLCollection 객체로 반환함  
```js
<ul>
  <li class=' color red'>빨강</li>
  <li class='color blue'>파랑</li>
  <li class='color green'>초록</li>
</ul>

<script>
 let useOfTagName = document.getElementsByClassName('color')
 // 이렇게 되면 클래스 값 color에 해당하는 모든 요소 노드에 대한 HTMLCollection 객체가 반환됨
 // 태그 이름을 이용해 탐색할 때와 마찬가지로 특정 요소의 자손 노드를 탐색하는 것이 가능함
</script>
```  

4. CSS 선택자 이용 
* document.prototype.querySelector() 메서드 : 인수로 전달한 CSS 선택자에 해당하는 하나의 요소 노드를 반환함  
```js
//대표적인 CSS 선택자
* { ... } // 모든 요소 선택
div { ... } // div 태그 요소 모두 선택
#id값 { ... } // id값에 해당하는 요소 선택 
.class값 { ... } // class값에 해당하는 요소 선택

<script>
 let useOfCSSSelector = document.querySelector('.color')
 // 이렇게 되면 클래스 값 color에 해당하는 첫 번째 요소 노드를 반환함
 // 이때 querySelectorAll 일 경우, 인수에 해당하는 모든 노드 요소에 대한 DOM 컬랙션 객체인 Nodeliest를 반환함
</script>
``` 
* element.prototype.matches() 메서드 : 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득 가능한지에 대해 booleanr값을 반환함
```js
<script>
 let useOfCSSSelector = document.querySelector('.red')
 useOfCSSSelector.matches('.blue')
 // 해당 CSS 선택자로 class값이 red인 요소 노드에 접근할 수 없으므로 false가 반환됨
</script>
``` 
<br />

### 221106 || DOM(3)
요소 노드를 취득해야 그의 자식 노드 등에 접근할 수 있다. 앞서 말했듯 자식 노드, 텍스트 노드, 어트리뷰트 노드 등에 접근하기 위해선 일단 요소 노드를 취득해야 하기 때문이다. 이번 파트에서 다룰 내용은 요소 노드 취득 후 어떻게 탐색하는가에 대한 내용이다.  

1. 자식 노드 탐색   
* Node.protptype.childNodes: 자식 노드를 전부 탐색해 Nodelist에 반환한다.
* Element.prototype.children: 자식 노드 중에서 요소 노드만 모두 탐색해 HTMLCollection에 담아 반환한다.
* Node.prototype.firstChild(lastChild): 첫 번째(마지막) 자식 노드를 반환하며 해당 노드는 텍스트 노드이거나 요소 노드이다.
* Element.protptype.first(last)ElementChild: 첫 번째(마지막) 자식 요소 노드를 반환하며 해당 노드는 요소 노드이다.   

2. 부모 노드 탐색 : Node.prototype.parentNode 프로퍼티를 이용해 탐색한다.    

3. 형제 노드 탐색   
* Node.protptype.previousSibling(nextSibling): 형제 노드 중 자신의 바로 이전(다음) 형제 노드를 탐색해 반환한다.
* Element.prototype.Previous(Next)ElementSibling: 형제 노드 중 자신의 바로 이전(다음) 형제 노드를 탐색해 반환하며 요소 노드만 반환한다.   

이렇게 탐색 후, 간혹 노드에 대한 조작이 필요한 경우가 있다. 그 중 텍스트 노드에 대한 조작이 필요할 경우 사용하는 프로퍼티는 다음과 같다.   
* nodeValue: 텍스트 노드의 nodeValue 프로퍼티에 변경하고자 하는 값을 할당하면 변경이 된다.
* textContent: nodeValue와 유사하나 HTML 마크업이 파싱되지 않아 자식 노드가 있을 경우 함부로 변경하면 자식 노드가 사라진다. 따라서 할당할 때 주의가 필요하다.
* innerText 프로퍼티 또한 텍스트 노드를 변경할 수는 있으나 CSS에 의해 비표시된 요소 노드의 텍스트를 반환하지 않는 등 CSS에 영향을 크게 받아 잘 사용하지 않는다.



