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
