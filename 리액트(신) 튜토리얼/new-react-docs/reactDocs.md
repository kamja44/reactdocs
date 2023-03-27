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
