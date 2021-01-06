# 1일차(1, 2장)

## React?

**React**는 Facebook에서 개발해 Facebook과 Instagram, Airbnb 등에서 사용하고 있는 **오픈소스 UI 프레임워크**입니다.

**React**는 다음과 같은 특징을 가지고 있습니다.

- **<span style="color: #4ca8c7">컴포넌트</span>** 기반
  - 재사용, 유지보수에 이점을 가짐
  - 관심사를 분리(여러 부분을 나누어 집중할 수 있게함)
- **<span style="color: #4ca8c7">Virtual DOM</span>** 을 사용
  - 최소한의 DOM 업데이트 가능하게 함 &rarr; 렌더링 성능향상
- **단방향 데이터 흐름**
  - 하향식의 데이터 흐름을 가짐
  - 데이터 추척과 디버깅이 쉬움

> 💡 **<span style="color: #4ca8c7">컴포넌트</span>** : 독립적이고 재사용가능한 코드들의 모음  
> 💡 **<span style="color: #4ca8c7">Virtual DOM</span>** : 추상적인 DOM으로 DOM의 변경사항을 한번에 받아서 DOM 조작이 빠르게 일어나게 함

<br/>

## Hello World 예제

React의 Hello world 예제는 아래와 같습니다.

```jsx
ReactDOM.render(
  <h1>Hellow World</h1>,  
  document.getElementById("root")
);
```

<br />

<p align="center">
  <img src="./images/hello_world.PNG" />
</p>

<br />

- `ReactDOM.render(element, container[, callback])`
  - `element`를 `container`에 렌더링함
  - `callback` 컴포넌트가 렌더링되거나 업데이트 된 후에 실행됨

<br />

## JSX

### 개요

React는 _JavaScript + html_ 같은 **JSX** 라는 언어를 사용합니다.
**JSX**는 컴파일러에 의해 JavaScript 함수로 호출되어 JavaScript 객체로 인식됩니다.

- html 부분을 마치 html처럼 사용할 수 있습니다.
  - **속성**을 사용
  - 자식 Element 포함할 수 있다.
- `{}`을 사용해서 html에서도 JavaScript 식과 값을 사용할 수 있습니다.
- React를 모듈을 import 해야 **JSX**를 사용할 수 있습니다.

```jsx
import React from "react";            // React 모듈을 가져와야 JSX를 사용 가능
import ReactDOM from "react-dom";     // 컴포넌트를 렌더링

const NAME = "Josh Perez";

// HTML 부분은 `<태그></태그>` 형태로 작성되어야 합니다.
const HTML_ELEMENT = <h1>Hello, {NAME}</h1>;      // {} 로 값 사용

// 만약 태그 내에 자식이 없는 경우 `<태그 />` 로 축약할 수 있습니다.
const IMG_TAG = <img src="someURL" />;

ReactDOM.render(
  <ul>
    <li>{ HTML_ELEMENT }</li>
    <li>{ IMG_TAG }</li>
    <li>또 다른 자식 등등...</li>
  </ul>,
  document.getElementById("root")
);
```

<br/>

<p align="center">
  <img src="./images/ex_2.PNG" />
</p>

<br/>

> ⚠️ JSX에서 HTML 엘리먼트 속성명은 **camelCase** 를 사용해야합니다.
>
> ```jsx
> import React from "react";           // 이를 해줘야 JSX 사용 가능
> 
> // var example-property-name = 'no'       // kabap-case
> var examplePropertyName = "yes"           // camelCase
>
> // onclick 이 아닌 onClick으로 속성을 줘야합니다.
> const JSX_EXP = <button onClick={() => clickFun()}>버튼 클릭</button>
> ```

<br/>

### 주석

JSX 안에서의 주석은 `{/* 주석입니다. */}` 형식으로 사용하면 됩니다.

```jsx
// JSX 밖에서는 JavaScript 주석 사용이 가능합니다.
const JSX_ELEMENT = <div>
  {/* 다만 JSX 안에서는  */}
  <span>
</div>
```

<br/>

### class 대신 className

JSX도 결국 JavaScript 이기 때문에 `class` 대신 `className`을 사용해야합니다.

```jsx
import React from "react";

const foo = "bar";

ReactDOM.render(
  /* <div class={foo}></div> */
  <p className={foo}>This is Text</p>
  document.getElementById("root")
);
```

<br/>

### 주입(injection) 공격 방지

**<span style="color: #4ca8c7">주입(injection) 공격</span>** 이란 프로그램을 주입하여 정보를 탈취하는 공격입니다.

React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 **<span style="color: #4ca8c7">이스케이프</span>** 하므로, 애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않습니다.

```jsx
import React from "react";           // 이를 해줘야 JSX 사용 가능

const title = response.potentially_malicious_input;   // 어떠한 injection 코드
const element = <h1>{title}</h1>;                     // 이스케이프되어 텍스트로만 출력됩니다.
```

> 📖 좀 더 자세한 [주입 공격 방지 예제](https://stackoverflow.com/questions/57746377/react-documentation-jsx-prevents-injection-attacks)

> 💡 이스케이프 : 특정 문자를 HTML로 변하는 행위(`&lt;`는 `<`으로 출력)

<br/>

### JSX는 객체를 표현

JSX로 작성된 코드는 **<span style="color: #4ca8c7">Babel</span>** 을 통해 JavaScript로 변경하게 됩니다.  
이때  `React.createElement()` 함수를 이용하여 새로운 **<span style="color: #4ca8c7">React 엘리먼트</span>**
를 생성하여 반환합니다.

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);

/* 위 코드는 babel에 의해 아래와 같이 변경됩니다. */

const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

`React.createElement()` 는 객체 반환하며 이 객체를 **<span style="color: #4ca8c7">React 엘리먼트</span>** 라고 합니다.

JSX는 `React.createElement()`의 **Syntax Sugar**(코드를 간결하게 표현) 입니다.

<br/>

> 💡 **<span style="color: #4ca8c7">Babel</span>** : 수많은 JavaScript 버전으로 트랜스파일하는 **트랜스파일러**

> 📖 `React.createElement()` 함수를 이용하여 [JSX 없이 React 코드를 작성](https://ko.reactjs.org/docs/react-without-jsx.html)할 수 있습니다.
