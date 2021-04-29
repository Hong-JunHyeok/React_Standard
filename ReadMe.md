# ⚛️React.js Standard

> ### ⚠️ 이 글은 React.js 공식 자습서에 의존하고 있는 글입니다.

아래의 사진은 공식 자습서에서 설명하고 있는 문구입니다.
![image](https://user-images.githubusercontent.com/48292190/116520103-3c85c200-a90d-11eb-8f19-a33faeaadd10.png)

**그만큼 쉬우신 거지~**

![무야호](https://blog.kakaocdn.net/dn/biT2IR/btqZ4AhxqLX/TQCSmdNKu1ZtDaHYVbNcBK/img.png)

그럼 한번 시작해볼까요?

# 🤨시작하기에 앞서...

리액트의 공식 자습서에서는 리액트를 이용해서 간단한 게임을 만드는데, 게임을 만들고 싶지 않아도 한번 해보는게 도움이 된다고 합니다...**공식 문서에서 강조하는 내용이니만큼 집중해서 해보겠습니다!**

⭐️ 이번 예제를 통해 배우는 내용은

- React의 기본(components, props, state)
- 일반적인 테크닉
- 깊은 통찰력

등을 배울 예정입니다.

> 🔥 자습서의 코드를 복사 붙여넣기 하는거보다, 직접 써보면서 하는 방식을 추천드립니다!

우리가 최종적으로 만들 게임은 [여기](https://codepen.io/gaearon/pen/gWWZgR?editors=0010) 있습니다.

**참고로 class형 컴포넌트를 사용하더라구요... 요즘에는 function형 컴포넌트를 많이 사용한답니다!** 그래도 class형도 알면 좋으니 한번 따라해보도록 하죠!

### 😝 틱택토 게임 해보셨나요?

했든 안했든 우리가 만들 게임이기 때문에 한번쯤은 플레이 해보는것을 추천드립니다!

[틱택토게임 직접 해보기](https://www.google.com/search?q=%ED%8B%B1%ED%83%9D%ED%86%A0+%EA%B2%8C%EC%9E%84&rlz=1C5CHFA_enKR950KR950&oq=%ED%8B%B1%ED%83%9D%ED%86%A0+%EA%B2%8C%EC%9E%84&aqs=chrome.0.0l10.2290j0j4&sourceid=chrome&ie=UTF-8)

### 🥶 리액트를 배우기 전에 필요한 지식

우리가 리액트를 하기 전에 넘어야할 산이 있습니다! (사실 그렇게 높은 산은 아니예요)
바로 **HTML** , **JavaScript**입니다.
완전 잘 할 필요는 없습니다. 그냥 기본만 알고있으면 충분히 할 수 있습니다!

(함수, 객체, 배열, 가능하다면 클래스 같은 프로그래밍 개념을 알고있어야합니다.)

### React란?

리액트는 선언적이고 효율적인 JavaScript 라이브러리입니다.
**컴포넌트**라고 불리는 작고 고립된 코드의 파편을 이용하여 복잡한 UI를 구성합니다.

```jsx
import React from "react";
import "./styles.css";

class ShoppingList extends React.Component {
  render() {
    return (
      <div>
        <h1>{this.props.name}'s Shopping List</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

export default ShoppingList;
```

쇼핑리스트라는 컴포넌트를 만들어서 복잡?한 UI를 단순화시킬 수 있습니다.

우리는 컴포넌트를 사용하여 React에게 화면에 표현하고 싶은 것이 무엇인지 알려줍니다.

**데이터가 변경될때 React는 효율적으로 업데이트를 하고 다시 렌더링합니다.**

🤨 아직 효율적에 대해서 아직은 생각하지 맙시다...우리는 리액트에 기능에 좀 더 집중하도록 하자구요.

우리가 return{} 문 안에 html과 유사하게 생긴 코드를 볼 수 있을텐데 왜 **유사하다**라고 했냐면 `JSX`라는 문법입니다... html이 아닌것이지요!

그럼 JSX가 html로 변환하는 과정은 어떻게 이루어질까요?
다음과 같이 동작합니다.

```js
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

좀 더 자세히 볼까요?

![image](https://user-images.githubusercontent.com/48292190/116552443-fdb73280-a933-11eb-9499-54e3ad76f87e.png)

😊 결국엔 리액트도 JS라는게 다시하번 느껴지죠?

JSX 내부의 중괄호 안에 어떤 JavaScript 표현식도 사용할 수 있습니다. 

무슨말인지 자세히 알아보도록 할까요?

우리가 JSX를 html태그만 사용했었는데 DOM컴포넌트도 렌더링할 수 있지만, Custom React Component도 사용할 수 있습니다.

무슨소리인지 잘 모르시겠다구요? 자세히 알아보도록 합시다.

![image](https://user-images.githubusercontent.com/48292190/116553859-897d8e80-a935-11eb-9d2c-8fd6dcc54092.png)

이렇게 동작하게 되는것이죠!

## 🤫 초기코드 살펴보기
공식 자습서에서 설명하는 코드인 [여기](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)에서 한번 코드를 살펴보도록 하겠습니다.

`src/index`를 열어주세요

코드를 살펴보면 세 가지의 React 컴포넌트를 확인할 수 있습니다.
- Square
- Board
- Game

`Square`컴포넌트는 button을 렌더링하고,

`Board`컴포넌트는 사각형 9개를 렌더링합니다. 

마지막으로 `Game` 컴포넌트는 게임판을 렌더링하며 나중에 수정할 자리 표시자 값을 가지고 있습니다. 


## Props를 통해 데이터 전달하기

> ### ⚠️여러분은 예제 사이트(미완성 된 코드)에서 내용을 추가하면 됩니다.

**코드를 절대로! 복사 붙여넣기 하지 마세요! 그냥 따라치면서 익힙시다.**

Square에 value prop을 전달하기 위해 Board의 renderSquare함수 코드를 작성해봅시다.

```js
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
``` 

이제 값을 표시하기 위해 render함수에서 {this.props.value}를 추가해줍시다!

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

![image](https://user-images.githubusercontent.com/48292190/116555543-7c619f00-a937-11eb-860e-a01b45d9ffe4.png)

그럼 다음과 같이 각 Square에 value가 잘 전달된것을 볼 수 있습니다!

이제 Props의 전달입니다! 

`Board`컴포넌트에서 -> `Square`컴포넌트로 **부모 컴포넌트에서 자식 컴포넌트로** 값을 전달한것이지요!

## 사용자와 상호작용 하는 컴포넌트 만들기

`Square`컴포넌트를 클릭하면 "X"가 체크되도록 해보겠습니다!

그러면 `click`했을때에 어떠한 동작을 해주어야겠죠?

어떻게 하는지 보도록 하겠습니다.

```js
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => {
          alert("click");
        }}>
        {this.props.value}
      </button>
    );
  }
}
```

`onClick`이라는 속성을 button컴포넌트에 주도록 합시다.

그러면 함수를 받게되는데 그때 alert하는 로직을 작성해주게 되는겁니다.

그렇게 어려운 내용은 아니지요?

Square 컴포넌트를 클릭한 것을 **“기억하게”** 만들어 “X” 표시를 채워 넣으려고 합니다.

음...**"기억하게"**라고 하니까 감이 안오죠?

무언가를 “기억하기”위해 component는 **state**를 사용합니다.

새로운 개념이 나왔습니다! **state**

