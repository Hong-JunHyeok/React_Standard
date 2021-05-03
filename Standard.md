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

# 엘리먼트 랜더링

> "엘리먼트는 React 앱의 가장 작은 단위입니다." - 리액트 공식문서

이번에 알아볼것은 엘리먼트의 랜더링입니다.

엘리먼트는 **화면에 표시할 내용**을 기술합니다.

> 이쯤되면 **컴포넌트**와 **엘리먼트**가 햇갈릴 수 있습니다.
> 엘리먼트는 컴포넌트의 “구성 요소”입니다. 자세한 설명은 다음장에 계속 설명하겠습니다.

## DOM에 엘리먼트 렌더링하기

HTML파일 어딘가에 <div>가 있다고 생각해봅시다.

```js
<div id="root"></div>
```

이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 “루트(root)” DOM 노드라고 부릅니다.

**React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있습니다.** React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM 노드가 있을 수 있습니다.

**React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 ReactDOM.render()로 전달하면 됩니다.**

```js
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById("root"));
```

## 렌더링 된 엘리먼트 업데이트하기

React 엘리먼트는 **불변객체**입니다.

**불변객체**... 이부분이 중요한 부분입니다.

엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할 수 없습니다. 엘리먼트는 영화에서 하나의 프레임과 같이 특정 시점의 UI를 보여줍니다.

**UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고 이를 ReactDOM.render()로 전달하는 것입니다.**

```js
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById("root"));
}

setInterval(tick, 1000);
```

위의 함수는 1초마다 새로운 리액트 DOM을 랜더링합니다.

> 실제로 대부분의 React 앱은 ReactDOM.render()를 한 번만 호출합니다.

## 변경된 부분만 업데이트하기

> React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트합니다.

이 말이 무슨말이냐면 "변경된 부분만 업데이트"하는 것입니다.

![gif](https://ko.reactjs.org/c158617ed7cc0eac8f58330e49e48224/granular-dom-updates.gif)

매초 전체 UI를 다시 그리도록 엘리먼트를 만들었지만 React DOM은 내용이 변경된 텍스트 노드만 업데이트했습니다.

# Components and Props

컴포넌트의 개념을 설명해보도록 하겠습니다.

**컴포넌트는 JavaScript 함수와 유사합니다. “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환합니다.**

## 함수 컴포넌트와 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 JavaScript함수를 사용하는 것입니다.

```js
function SimpleComponent(props) {
  return <h1>Hello Function Component, I am {props.name}</h1>;
}
```

이 함수는 데이터를 가진 props (props는 속성을 나타내는 데이터입니다)라는 객체 인자를 받은 후, React엘리먼트를 반환합니다.

**이것이 함수형 컴포넌트입니다.**

ES6 Class문법을 사용하여 클래스형 컴포넌트도 정의할 수 있습니다.

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Class형에는 몇 가지 추가기능이 있습니다.
**함수 컴포넌트와 클래스 컴포넌트 둘 다 몇 가지 추가 기능이 있으며** 이에 대해서는 다음에 자세히 설명하겠습니다.

# 컴포넌트 렌더링

React 엘리먼트는 사용자 정의 컴포넌트로 나타낼 수 있습니다.

```js
const element = <Welcome name="Sara" />;
```

`name="Sara"`라고 된 부분이 있죠? 그 부분을 우리가 **props를 전달한다** 라고 합니다.

즉, props를 전달함으로서 다음과 같은 로직이 가능한것이죠.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById("root"));
```

# 컴포넌트 합성

컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있습니다.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

React 앱에서는 버튼, 폼, 다이얼로그, 화면 등의 모든 것들이 흔히 컴포넌트로 표현됩니다.

# 컴포넌트 추출

컴포넌트를 추출하는 과정은 컴포넌트를 여러 개의 작은 컴포넌트로 나누는 과정을 의미합니다.

이 과정을 과감히 해버리세요! 다음 코드를 봅시다.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img
          className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

음... 이게 React를 쓰는건지 HTML을 쓰는건지 잘 모르시겠죠?

그래서 컴포넌트를 추출하는 과정을 통해 좀 더 직관적인 코드로 변경해보겠습니다.

img태그부터 추출해보겠습니다.

```js
function Avatar(props) {
  return (
    <img className="Avatar" src={props.user.avatarUrl} alt={props.user.name} />
  );
}
```

그러면 Comment코드상에선,

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

이렇게 치환될 수 있겠죠.

그 다음 UserInfo컴포넌트도 만들어 보겠습니다.

```js
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">{props.user.name}</div>
    </div>
  );
}
```

이제 Comment가 더욱 단순해질 수 있겠죠?

```js
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

이 작업이 굉장히 귀찮고 지루할 수 있습니다. 하지만 재사용 가능한 컴포넌트를 만들어 놓는 것은 더 큰 앱에서 작업할 때 두각을 나타냅니다.

**UI 일부가 여러 번 사용되거나 (Button, Panel, Avatar), UI 일부가 자체적으로 복잡한 (App, FeedStory, Comment) 경우에는 별도의 컴포넌트로 만드는 게 좋습니다.**

![image](https://media.vlpt.us/images/devgosunman/post/f0f69596-9dc9-4533-ba90-e12fd55a8c62/react%20state.jpg)

# props는 읽기 전용입니다.

무슨 말인지 한번 볼까요?

```js
function sum(a, b) {
  return a + b;
}
```

위의 함수는 **순수 함수**라고 합니다.

순수 함수에 대해서는 [여기](https://velog.io/@chdb57/%E3%85%87%E3%85%87%E3%85%87%E3%85%87%E3%85%87%E3%85%87%E3%85%87%E3%85%87)를 참조해보시길 바랍니다.

**모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.**

애플리케이션 UI는 동적이며 시간에 따라 변합니다. 그래서 위 규칙을 위반하지 않고 사용자 액션, 네트워크 응답 및 다른 요소에 대한 응답으로 시간에 따라 자신의 출력값을 변경할 수 있는 방법은 `State`입니다.

이제 자세히 한번 알아보도록 할까요?

![image](https://blog.kakaocdn.net/dn/b7Ing6/btqDrkNbvBs/Mi1pUyMUSRYYLmE6zvjAG0/img.png)

# State and Lifecycle

이전에 째깍거리는 시계를 랜더링 한거 기억나시죠? 출력값을 변경하기 위해서 새로 엘리먼트를 랜더링하는 작업을 해주었습니다.

```js
ReactDOM.render();
```

일단 `Clock`이라는 컴포넌트를 만들어서 캡슐화를 진행해줍시다.

```js
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(<Clock date={new Date()} />, document.getElementById("root"));
}

setInterval(tick, 1000);
```

이렇게 진행하면 되겠죠?

하지만 우리가 구현하고 싶은건

```js
ReactDOM.render(<Clock />, document.getElementById("root"));
```

딱 이코드 한번만 실행하고 싶습니다.

이럴때 `state`를 사용해야 할 차례입니다.

**State는 props와 유사하지만, 비공개이며 컴포넌트에 의해 완전히 제어됩니다.**

# 함수에서 클래스로 변환하기

state를 사용할려면 class형 컴포넌트를 사용해야 합니다.function형 컴포넌트에는 state를 사용할 수 없습니다. (React hooks를 쓰면 그게 가능해집니다.)

다음 코드를 한번 살펴볼까요?

```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
function tick() {
  ReactDOM.render(<Clock date={new Date()} />, document.getElementById("root"));
}

setInterval(tick, 1000);
```

이러면 함수형 컴포넌트를 클래스형 컴포넌트로 변환이 완료되었습니다.

# 클래스에 로컬 State 추가하기

class형 컴포넌트에 constructor를 정의해 주신다음에 다음과 같은 코드를 작성해주세요.

```js
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

이 과정이 state를 선언하는 과정입니다.
super(props)이 부분은 모든 class형 컴포넌트는 super(props)를 해주어야 합니다. (상속되어지는 관계이기 때문이죠)

그 다음 this.state = {...} 이 부분이 state를 선언하는 부분입니다.

date라는 속성에 new Date()를 하게 됨으로써 현제 시간을 data라는 state에 담게 되는것이죠.

**최종 코드는 다음과 같습니다.**

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock />, document.getElementById("root"));
```

하지만 실행해보면 안움직이죠?

당연합니다! **왜냐하면 매초 스스로 움직이라는 코드를 작성하지 않았으니까요!**

한번 해보도록 하겠습니다.

# 생명주기 메서드를 클래스에 추가하기

Clock이 처음 DOM에 랜더링 될때마다 타이머를 설정할려고 합니다.
또한 DOM이 삭제될때마다 타이머를 해제할려고 합니다.

여기, 좋은 기능이 있습니다.

```js
  componentDidMount() {
  }

  componentWillUnmount() {
  }
```

이 기능을 사용하면 쉽게 랜더링 될 때, 삭제될 때를 확보할 수 있습니다.

이러한 메서드들을 **생명주기 메서드라고 합니다.**

```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date(),
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock />, document.getElementById("root"));
```

다음과 같이 작성해주세요.

코드가 이해가지 않는 분들을 위한 설명타임이 있겠습니다.

`componentDidMount`는 컴포넌트가 랜더링 될 시기를 의미합니다.
그러면

```js
componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }
```

다음과 같은 코드는 **컴포넌트가 마운트 될 때 매초 tick이라는 함수를 실행한다는 의미입니다.**

`componentWillUnmount`는 컴포넌트가 삭제될 시기를 의미합니다.

```js
componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

다음과 같은 코드는 interval된 타이머 함수를 컴포넌트가 삭제될 때 제거하겠다는 의미입니다.

# State 업데이트는 비동기적일 수도 있습니다.

이 부분에서 state사용에 오류가 나는 경우가 많이 있습니다.

this.props와 this.state가 비동기적으로 업데이트될 수 있기 때문에 다음 state를 계산할 때 해당 값에 의존해서는 안 됩니다.

예를 한번 들어볼까요?

```js
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

이 업데이트는 실패할 수 있습니다.

이를 수정하기 위해 객체보다는 함수를 인자로 사용하는 다른 형태의 setState()를 사용합니다. 그 함수는 이전 state를 첫 번째 인자로 받아들일 것이고, 업데이트가 적용된 시점의 props를 두 번째 인자로 받아들일 것입니다.

즉, 다음 형식으로 작성하면 됩니다.

```js
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment,
}));
```

이전 state와 업데이트가 적용된 props를 받고 진행을 할겁니다.

> 물론 화살표 함수 말고 그냥 function키워드 함수도 가능합니다.

![image](https://media.vlpt.us/images/daybreak/post/4dfb762a-30f3-48ed-a380-4260f8c7e39f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-07-09%2016.39.35.png)

이 부분 정확히 짚고 넘어가주세요!
