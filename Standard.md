# ⚛️ 리액트의 기초

> ### ⚠️ 이 글은 React.js 공식 자습서에 의존하고 있는 글입니다.

TicTacToe를 만들때에는 `Class`형 컴포넌트를 사용했다면 이번 기초예제는 `Function`형 컴포넌트를 사용해볼려고 합니다.

최근에는 Function형 컴포넌트가 많이 쓰이고 있으니 천천히 배워보도록 하겠습니다.

<hr />

# 목차

이번 목차는 다음과 같습니다.

![image](https://user-images.githubusercontent.com/48292190/116813790-88946900-ab90-11eb-9e42-46a285a0f2ea.png)

# 목적

리액트 공식 사이트에서 TicTacToe가 예제로 나왔는데 이를 보고 이해를 하지 못하는 사람들도 많고 햇갈리는 부분이 있을수도 있기때문에 이를 보완하고자. 이 기초 파트를 준비했습니다.

> ### ⚠️ 이 글은 React.js 공식 자습서에 의존하고 있는 글입니다.

시작해보도록 하겠습니다.

# JSX

## 🤨 JSX 소개

먼저, 아래의 코드를 보도록 합시다.

```js
const element = <h1>Hello, world!</h1>;
```

위의 문법은 HTML도, 문자열도 아닙니다.

**JavaScript를 확장한 문법인 JSX라고 합니다.**

JSX는 JavaScript의 모든 기능이 포함되어 있습니다.

**JSX는 엘리먼트(element)를 생성합니다.**

React에서는 이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등 **렌더링 로직이 본질적으로 다른 UI 로직과 연결된다는 사실을 받아들입니다.**

![image](https://blog.kakaocdn.net/dn/bgsR0l/btqBSOXRul7/vqCF5iy4EpEpxY3qIulYCK/img.png)

JSX는 사실 리액트에서 `필수`로 요구되는 문법은 아닙니다. [관련 링크](https://ko.reactjs.org/docs/react-without-jsx.html)

대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다.

이제 JSX를 사용하는 방법을 알아보도록 하겠습니다.
예제를 보면 이해가 수월해질 겁니다.

## JSX에 표현식 포함하기

```js
const name = "Josh Perez";
const element = <h1>Hello, {name}</h1>;
```

JSX에 {}안에는 모든 JavaScript표현식을 넣을 수 있습니다.

예를 들면 `2 + 2`나 `user.name`이나 `formatTime(time)`등이나 사용할 수 있는것이죠.

## JSX도 표현식입니다

컴파일이 끝나면, JSX 표현식이 정규 JavaScript 함수 호출이 되고 JavaScript 객체로 인식됩니다.

그러면 우리가 무슨작업을 할 수 있냐면,

다음과 같은 작업을 수행할 수 있습니다.

```js
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

지금 집중해서 볼 부분은 if문입니다. 이러한 표현식이 가능한것이죠.

**JSX를 if 구문 및 for loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있습니다.**

## JSX 속성 정의

속성에 따옴표를 이용해 문자열 리터럴을 정의할 수 있습니다.

```js
const element = <div tabIndex="0"></div>;
```

또한 JavaScript표현식도 넣을 수 있습니다.

```js
const element = <img src={user.avatarUrl}></img>;
```

> ## ⚠️주의할 점
>
> 어트리뷰트에 JavaScript 표현식을 삽입할 때 중괄호 주변에 따옴표를 입력하지 마세요. 따옴표(문자열 값에 사용) 또는 중괄호(표현식에 사용) 중 하나만 사용하고, 동일한 어트리뷰트에 두 가지를 동시에 사용하면 안 됩니다.

JSX는 HTML보다 JavaScript에 더 가깝기때문에 **React DOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용합니다.**

대표적인 예로는 `class`가 아니라 `className`입니다.

## JSX로 자식 정의

태그가 비어있다면 XML처럼 /> 를 이용해 바로 닫아주어야 합니다.

```js
const element = <img src={user.avatarUrl} />;
```

JSX태그는 자식을 표함할 수 있습니다.

```js
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

**JSX태그는 반드시 최상위 태그가 닫혀있어여합니다.**

## JSX는 주입 공격을 방지합니다

XSS인 사이트 간 스크립팅 공격을 방지할 수 있습니다. 기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 이스케이프 하므로 가능한 일이죠. **애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않습니다. 모든 항목은 렌더링 되기 전에 문자열로 변환됩니다.**

![image](https://portswigger.net/web-security/images/cross-site-scripting.svg)

## JSX는 객체를 표현합니다.

Babel은 JSX를 React.createElement() 호출로 컴파일합니다.

코드를 보고 알아보도록 하죠.

```js
const element = <h1 className="greeting">Hello, world!</h1>;
```

```js
const element = React.createElement(
  "h1",
  { className: "greeting" },
  "Hello, world!"
);
```

**이제 createElement가 무엇을 만드는지 보도록 할까요?**

```js
// 주의: 다음 구조는 단순화되었습니다
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world!",
  },
};
```

위와 같은 형식으로 만들어줍니다. 즉, 객체를 표현합니다.

> 이러한 객체를 “React 엘리먼트”라고 하며, 화면에서 보고 싶은 것을 나타내는 표현이라 생각하면 됩니다. React는 이 객체를 읽어서, DOM을 구성하고 최신 상태로 유지하는 데 사용합니다.