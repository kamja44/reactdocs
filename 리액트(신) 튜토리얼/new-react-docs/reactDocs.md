[리액트 Docs](#https://react.dev/learn/tutorial-tic-tac-toe)

App.js

App.js 파일에서는 컴포넌트를 생성한다.
React에서 컴포넌트는 사용자 인터페이스의 일부를 나타내는 재사용 가능한 코드의 일부이다.
컴포넌트는 어플리케이션의 UI를 render, manage, update할 때 사용된다.

```js
export default function Square(){
    return <button className="square">X<button>;
}
```

첫 번째 줄인 `export default function Square()`은 Square 함수를 정의한다.
`export`는 App.js 외부 파일에서 Square()를 사용할 수 있게 한다.
`default` 키워드는 코드를 사용하는 다른 파일에 파일의 주 기능임을 명시한다.

두 번째 줄인 `return <button className="square">X<button>;`은 버튼을 리턴한다.
JS에서 `return` 키워드는 함수의 호출자 에게 return 뒤에 오는 것을 반환한다.
`button`은 JSX의 element이다.
JSX란, JS와 HTML 태그의 조합이며, 표현하고 싶은 내용을 설명한다.
`className="square"`은 button의 prop이며, CSS 스타일 방식을 지정한다.
`X`는 버튼 안에서 보여줄 text이다.

index.js

- index.js 파일은 App.js 파일에서 만든 컴포넌트와 web browser 사이의 징검다리 역할을 한다.

# 보드 만들기

App.js 파일에 사각형을 만든다.
React 컴포넌트는 하나의 JSX element만 반환할 수 있다.

- 여러개의 JSX element를 반환하기 위해선 `<></>` fragments를 사용한다.

```jsx
export default function Square() {
  return (
    <>
      <button className="square">X</button>
      <button className="square">X</button>
    </>
  );
}
```

Square 함수를 아래와 같이 수정하여 보드판을 생성한다.

```jsx
export default function Square() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

board-row와 square className은 styles.css에 정의되어 있다.

Square() 함수를 Board() 함수로 이름 변경하기

```jsx
export default function Board() {}
```

# props를 통해 데이터 전달하기

사용자가 빈상자를 클릭하면 X가 나오게 설정한다.
React의 구성 요소 아키텍처를 사용하면 코드의 재사용이 가능하다.

- App.js 파일에 아래와 같은 Square() 함수를 생성한다.

```js
function Square(){
    return(
        <button className="square">1</button>;
    )
}
```

JSX문법을 이용하여 Square 구성 요소를 렌더링하도록 보드 구성 요소를 업데이트한다.

```js
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

`Board와 Square와 같은 component들은 항상 대문자로 시작해야 한다.`

위의 코드로 변경하면 사각형은 1만 표시한다.

- props를 이용하여 값들을 부모 component에서 자식 component로 전달할 수 있다.
  - Board component에서 Square 컴포넌트로 props를 이용하여 값을 전달한다.

Board component에서 전달한 value를 읽을 수 있게 Square component를 아래와 같이 변경한다.

```js
function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

`function Square({value})`는 Square component가 value라는 prop을 전달할 수 있음을 나타낸다.

- return문에서 value를 {}로 감싸야 JS문법이 적용된다.
  - 즉, value는 value 문자를 출력하고 {value}는 value 변수를 출력한다.
  - Board component가 Square component에 아무것도 전달하지 않았기에 빈 사각형만 나타난다.

Square component에 value props 전달

```js
export default function Board(){
    return(
        <>
            <div className="board-row">
                <Square value="1">
                <Square value="2">
                <Square value="3">
            </div>
            <div className="board-row">
                <Square value="4">
                <Square value="5">
                <Square value="6">
            </div>
            <div className="board-row">
                <Square value="7">
                <Square value="8">
                <Square value="9">
            </div>
        </>
    )
}
```

Making an interactive component

클릭했을 때 Square component를 Xㄹ ㅗ채우기

- handleClick 함수를 Square 함수 안에 선언한다.
- onClick을 JSX의 elment가 반환하는 button의 props에 추가한다.

```js
function Square({ value }) {
  function handleClick() {
    console.log("clicked!");
  }
  return (
    <button className="square" onClick={handleClick}>
      {value}
    </button>
  );
}
```

- Square를 클릭하면 console에 clicked!가 출력된다.

react의 useState component를 이용하여 component를 기억(저장)할 수 있다.
Square component의 현재 값을 저장하고, Square 클릭 시 상태를 변경한다.

useState를 사용하기 위해 react에서 import하고, Square 함수에서 value를 제거한 후, `const[value, setValue] = useState(null)`을 Square 함수에 추가한다.

```js
import { useState } from "react";

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    //....
  }
}
```

- useState의 첫 번째 매개변수
  - 값을 저장한다.
- useState의 두 번째 매개변수
  - 값을 변경한다.
- useState의 null은 value의 초깃값이다.

Square component에서 더이상 props를 사용하지 않기 때문에 Board에서 정의한 value props을 제거한다.

handleClick 함수의 console.log("clicked!")를 setValue("X")로 변경하여 Square 컴포넌트 클릭 시 X를 표시한다.

```js
function handleClick() {
  setValue("X");
}
```

setValue function을 onClick에서 호출함으로써 React에게 button 클릭 시 Square component를 리렌더링한다고 알릴 수 있다.

- Square component가 리렌더링되면 Square의 value는 "X"가 되어 Square에 X가 표시되는 걸 볼 수 있다.

각각의 Square component는 자신만의 state를 갖는다.

- 저장된 value가 각 Square마다 독립적이다.

component에 setValue(set)을 호출한다면 React는 자동적으로 자식 component의 내부까지 업데이트 한다.

Lifting state up

현재 각각의 Square component는 게임의 state를 유지하고 있다. 게임의 승자를 가리기 위해선 Board component는 어떻게든 각각의 Square components를 알아야 한다.

Board component가 Square components를 알기 위해선 Board component(부모 component)에 Square components의 state를 저장하는 것이다.

- Board component는 Square component에게 숫자를 전달할 때 처럼 prop을 전달하여 표시할 내용을 각 사각형에 알려줄 수 있다.

여러 하위 항목에서 데이터를 수집하거나, 두개의 component가 서로 통신하도록 하려면 부모 구성 요소에서 공유 상태를 대신 선언한다.
상위 구성 요소는 via props를 통해 해당 state를 자식에게 다시 전달할 수 있다.
이렇게 하면 자식 구성 요소가 서로 및 부모 구성 요소와 동기화된다.

Lifting state는 React components를 `결과의 변경 없이 코드의 구조를 재조정할`때 유용하다.

9개의 정사각형에 해당하는 9개의 null 배열로 기본값을 지정하는 사각형이라는 상태 변수를 선언하도록 보드 구성 요소를 편집한다.

```js
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
}
```

Array(9).fill(null)은 9개의 요소와 배열을 만들고 요소의 값을 null로 설정한다.
useState() 호출은 처음에 해당 배열로 설정된 제곱 상태 변수를 선언한다.
각각의 배열의 값은 사각형의 값과 일치한다.
추후에 board를 채우면 squares 배열은 아래와 같이 보인다.
`["O", null, "X","X","X","O","O",null,null]`
이제 Board component에서 value prop을 Square에 다음과 같이 보내야 한다.

```js
export default function Board(){
  const [squares, setSquares] = useState(Array(9).fill(null));
  return(
    <>
      <div className="board-row">
        <Square value={squares[0]}>
        <Square value={squares[1]}>
        <Square value={squares[2]}>
      </div>
      <div className="board-row">
        <Square value={squares[3]}>
        <Square value={squares[4]}>
        <Square value={squares[5]}>
      </div>
      <div className="board-row">
        <Square value={squares[6]}>
        <Square value={squares[7]}>
        <Square value={squares[8]}>
      </div>
    </>
  )
}
```

이후, Square component가 Board component로 부터 전달받은 value prop을 받을 수 있게 수정한다.

- 이를 위해선 Square component 구성 요소의 상태 저장 값 추적 및 onClick prop을 제거해야 한다.

```js
function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

이제 각 Square는 value prop은 "X","O",null을 가질 수 있다.

- Square 클릭 시 값을 변경해 줘야 한다.
-
