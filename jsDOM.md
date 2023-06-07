# 오늘 설명한 JS DOM 글로 읽기

# JS DOM 이란?

JS DOM 은 Document Object Model 의 약자로

> <br>Document : HTML 문서의<br><br>
> Object : 객체를<br><br>
> Model : 인식(상호작용) 하는 방식<br><br>

이라고 생각하시면 편합니다.

JS DOM 을 이용해서 HTML 요소를 맘대로 추가, 수정, 삭제 할 수 있습니다.

# JS DOM 코드 작성

JS DOM 으로 요소를 가져오는 방법은 크게 4가지가 있습니다.

각각

> <br>요소의 아이디, 클래스, 태그, 3가지 전체<br><br>

를 이용해서 가져올 수 있습니다.

모두 앞에 document 라고 써줘야지 주어진 문서에서 요소를 가져올 수 있습니다.

```js
document.getElementById("아이디");
document.getElementsByClassName("클래스");
document.getElementsByTagName("태그");
document.querySelector("태그 or #아이디 or .클래스)");
```

# getElement(getElements) 시리즈

얘네는 말 그대로 getElement 또는 getElements 뒤에 붙는 거를 찾아준다.

ById 는 아이디명로

ByClassName 은 클래스명으로

ByTagName 은 태그명으로

얘네는 모두 HTML 요소 객체를 가져오므로 당연하지만 변수에 담아서 사용하면 됩니다.

index.html

```html
<div id="box"></div>
```

script.js

```js
const div = document.getElementById("box");
```

# querySelector

위의 get 시리즈는 모두 각각 하나의 기능을 가졌다면,<br>
얘는 모든 기능을 짬뽕한 함수입니다.

뒤의 괄호에

태그명, .클래스명, #아이디명

이렇게 각각 아무것도 안 붙이면 태그, . 을 붙이면 클래스명, # 을 붙이면 아이디명으로 가져옵니다.

index.html

```html
<div id="box">Hello World</div>
```

script.js

```js
const div = document.querySelector("#box");
```

# 가져오고 끝?

당연히 아니죠.

가져오고 끝이면 왜 가져와요.

여러가지 것들을 바꿀 수 있습니다.

먼저 해당 요소가 가진 내용을 바꿀 수 있습니다.

innerText, innerHTML 속성인데

얘네를 바꿔주면 각각 내부 텍스트, 내부 HTML 을 바꿔줍니다.

사용 방법은 요소.innerText or innerHTML 입니다.

```html
<div id="box">
    <p>hello world</p>
</div>
```

script.js

```js
const div = document.querySelector("#box");

div.innerText = "hello world";
div.innerHTML = "<p>hello world</p>";
```

---

다음은 style 속성입니다.

얘는 해당 요소의 CSS 를 바꿀 수 있습니다.

하지만 querySelector 로 가져온 경우에는 사용할 수 없습니다.

사용 방법은 요소.style.CSS속성 입니다.

```html
<div id="box">
    <p>hello world</p>
</div>
```

script.js

```js
const div = document.getElementById("box");

div.style.color = "#magenta";
```

---

속성은 여러가지 더 있습니다.

하지만 그때 그때 찾아보는 것이 더 좋다고 생각되어 여기에 더 설명은 하지 않겠습니다.

찾아 볼 수 있는 속성의 기능은

> <br>클래스명, 자식 요소, 부모 요소 등등 <br><br>

이 있습니다.

# 이벤트

이벤트는 한 요소에 대한 모든 상호작용을 의미합니다.

마우스로 클릭을 하거나, 마우스가 위로 올라가거나 빠져나가거나, 스크롤을 하거나 등등 여러가지 상호작용이 존재하는데 이를 모두 이벤트라고 부릅니다.

이벤트는 addEventListener 라는 걸로 인식할 수 있습니다.

# addEventListener

index.html

```html
<div id="clicker">
    <p>times : 0</p>
</div>
```

script.js

```js
const clicker = document.getElementById("clicker");

clicker.addEventListener('이벤트', () => {'코드'});
```

위의 코드는 clicker 요소에 대한 이벤트를 인식하는 코드입니다.

'이벤트'에 해당하는 부분에 이벤트 이름을 넣어주면 되고, '코드'는 당연하게도 인식했을 때 실행할 코드를 작성하면 됩니다.

이벤트에는 여러 종류가 있는데, 이 중 마우스에 해당하는 이벤트만 봅시다.

> <br>click, dbclick, mousedown, mouseup, mousemove, mouseover, mouseout<br><br>

각각 클릭, 더블클릭, 마우스 클릭 상태, 마우스 클릭을 눌렀다 뗀 상태, 마우스 움직임, 요소 위로 마우스 올리기, 요소 밖으로 마우스 올리기 를 의미합니다.

그렇다면 클릭을 한 번 인식해봅시다.

script.js

```js
const clicker = document.getElementById("clicker");

clicker.addEventListener("click", () => {
    console.log("It's clicked!");
});
```

이렇게 하면 clicker 요소가 클릭될 때 마다 콘솔을 찍습니다.

***

이제 끝입니다. 과제는 아래 내용입니다.

clicker 요소의 times : 0 텍스트를 계속 업데이트 하도록 만들어보세요.
