> ### ⚠️ 이 글은 React.js 공식 자습서에 의존하고 있는 글입니다.

# 🎣 Hook의 개요

![image](https://user-images.githubusercontent.com/48292190/116880733-53098180-ac5d-11eb-8165-d4e7bd18c0cf.png)

Class 기반으로 작성되던 리액트 컴포넌트는 이제 함수형 컴포넌트 만으로 기능을 구현할 수 있게 되었습니다.

기존 class형을 사용할 때보다 훨씬 깔끔한 코드가 매력적입니다.

![image](https://user-images.githubusercontent.com/48292190/116961678-f484e780-acde-11eb-95a4-a8f739c220ec.png)

처음으로 배우게 될 hook은 `useState()`입니다.

이전에 함수형 컴포넌트에서는 state를 사용하지 못한다고 했었는데, hooks를 도입함으로써 그것이 해결되었습니다.

간단한 사용 예제를 보도록 합시다.

```js
import React, { useState } from "react";

function Example() {
  // "count"라는 새로운 상태 값을 정의합니다.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

**여기서 useState가 훅입니다. Hook을 호출해 함수 컴포넌트(function component) 안에 state를 추가했습니다.**

이 state는 컴포넌트가 다시 렌더링 되어도 그대로 유지될 것입니다. (새로고침은 초기화 됩니다.)

useState는 현재의 **state 값과 이 값을 업데이트하는 함수**를 쌍으로 제공합니다.

_이 함수를 이벤트 핸들러나 다른 곳에서 호출할 수 있습니다._

여기서 setState의 class와 hooks의 차이점이 있습니다.

**이전 state와 새로운 state를 합치지 않는다는 차이점이 있습니다.**
(이 부분에 대해서는 나중에 자세히 설명하겠습니다.)

this.state와는 달리 setState Hook의 state는 객체일 필요가 없습니다. 물론 원한다면 그렇게도 가능하지만요. 이 초기값은 첫 번째 렌더링에만 딱 한번 사용됩니다.

하나의 컴포넌트에 여러가지 State Hooks을 사용할 수 있습니다.

```js
function ExampleWithManyStates() {
  // 상태 변수를 여러 개 선언했습니다!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState("banana");
  const [todos, setTodos] = useState([{ text: "Learn Hooks" }]);
  // ...
}
```

그런데

```js
const [state, setState] = useState(initialState);
```

이런식의 문법이 좀 생소하시죠? 이는 배열 구조 분해 문법입니다. [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EB%B0%B0%EC%97%B4_%EA%B5%AC%EC%A1%B0_%EB%B6%84%ED%95%B4)에서 한번 보도록 하세요.

**이 변수명은 useState API와 관련이 없습니다.**

대신에 React는 매번 렌더링할 때 useState가 사용된 순서대로 실행할 것입니다. 왜 이렇게 동작하는지는 나중에 살펴보겠습니다.

# 🤨 Hook이 무엇인가?

자꾸 hook, hook 그러는데 잘 이해가 가지 않으실거예요. 정확히 이게 뭐하는 기능인지 햇갈리신건데, **Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다.**

Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

React에서는 몇몇 내장 hooks를 제공하는데, **컴포넌트 간에 상태 관련 로직을 재사용하기 위해 Hook을 직접 만드는 것도 가능합니다.** (이를 custom hooks이라고 합니다.)

# ⚡️ Effect Hook

React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 이전에도 종종 해보셨을 것입니다. 우리는 이런 모든 동작을 “side effects”(또는 짧게 “effects”)라고 합니다.

**왜냐하면 이것은 다른 컴포넌트에 영향을 줄 수도 있고, 렌더링 과정에서는 구현할 수 없는 작업이기 때문입니다.**

이걸 `useEffect`를 사용해서 구현할 수 있습니다.

코드로 예제를 들어보도록 하죠.

```js
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount, componentDidUpdate와 비슷합니다
  useEffect(() => {
    // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

`useEffect`를 사용하면, React는 DOM을 바꾼 뒤에 “effect” 함수를 실행할 것입니다.

**Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있습니다. 기본적으로 React는 매 렌더링 이후에 effects를 실행합니다. 첫 번째 렌더링도 포함해서요.**

Effect를 “해제”할 필요가 있다면, 해제하는 함수를 반환해주면 됩니다.

해제하는 방법을 알아볼까요?

```js
import React, { useState, useEffect } from "react";

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

이 예시에서 컴포넌트가 unmount될 때 React는 ChatAPI에서 구독을 해지할 것입니다. 또한 재 렌더링이 일어나 effect를 재실행하기 전에도 마찬가지로 구독을 해지합니다.

`useState`와 마찬가지로 컴포넌트 내에서 여러 개의 effect를 사용할 수 있습니다.

이 Effect Hooks도 나중에 더욱 자세히 알아보도록 하겠습니다.

# 🤫 Hooks 사용 규칙

Hook은 그냥 JavaScript 함수이지만, 두 가지 규칙을 준수해야 합니다.

- 최**상위(at the top level)에서만 Hook을 호출해야 합니다.** 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하지 마세요.

- **React 함수 컴포넌트 내에서만 Hook을 호출해야 합니다.**
  일반 JavaScript 함수에서는 Hook을 호출해서는 안 됩니다. (Hook을 호출할 수 있는 곳이 딱 한 군데 더 있습니다. 바로 직접 작성한 custom Hook 내입니다. 이것에 대해서는 나중에 알아보겠습니다.)

![image](https://user-images.githubusercontent.com/48292190/116963067-c30e1b00-ace2-11eb-9a50-2f305e26ce9a.png)

이 규칙들은 eslint 플러그인들로 강제할 수 있습니다.

# 💡 나만의 Hook 만들기

가끔 상태 관련 로직을 컴포넌트 간에 재사용하고 싶은 경우가 생깁니다. 그럴때 내가 직접 hook을 구현해서 사용할 수 있습니다.

**친구의 접속 상태를 구독하기 위해서 useState와 useEffect Hook을 사용한 FriendStatus 컴포넌트 예시를 다시 한번 보겠습니다. 이 로직을 다른 컴포넌트에서도 재사용하고 싶다고 가정을 해봅시다.**

```js
import React, { useState, useEffect } from "react";

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

그러면 이제 나른 컴포넌트에서 뽑아서 쓸 수 있습니다.

```js
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

각 컴포넌트의 state는 완전히 독립적입니다.

**Hook은 state 그 자체가 아니라, 상태 관련 로직을 재사용하는 방법입니다. 실제로 각각의 Hook 호출은 완전히 독립된 state를 가집니다.**
<- 이 부분 중요합니다!

그래서 심지어는 한 컴포넌트 안에서 같은 custom Hook을 두 번 쓸 수도 있습니다.

Custom Hook은 기능이라기보다는 컨벤션(convention)에 가깝습니다.

이름이 ”use“로 시작하고, 안에서 다른 Hook을 호출한다면 그 함수를 custom Hook이라고 부를 수 있습니다.

네이밍을 use로 해주어야 하는 이유는 lint에서 이게 hook임을 알게하기 위해서입니다. 덕분에 오류도 찾고 버그도 해결하죠!

