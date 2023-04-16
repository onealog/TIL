# `useEffect` vs `useLayoutEffect`

`useLayoutEffect`는 한번도 써본적이 없어서 도대체 이녀석은 무슨 역할을 하는지 궁금해 하다가 알아보기로 했다.   
`useEffect`와 `useLayoutEffect`는 비슷한 기능을 가지고 있지만 **실행 시점이 다르다**는 차이를 가지고 있다.   

<br>

## `useEffect`

`useEffect`는 컴포넌트가 렌더링되고 난 후, DOM에 업데이트가 일어난 후 비동기적으로 실행된다. `useEffect`를 사용하면 컴포넌트가 업데이트되거나 화면이 다시 그려질 때마다 실행된다. 대개 `useEffect`를 사용하여 외부 API 호출, 타이머, 이벤트 등을 처리한다. 렌더링 작업을 차단하지 않기 때문에 일반적으로 빠른 반응성을 제공한다.

<br>

### `useEffect` 예시
```js
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

<br>

## `useLayoutEffect`
`useLayoutEffect`는 실행 시점이 `useEffect`와 다른데, 컴포넌트가 렌더링된 후, DOM 업데이트가 일어나기 전에 동기적으로 실행된다. 이러한 이유로 `useLayoutEffect`는 렌더링 이전에 수행해야 하는 작업에 사용된다. `useLayoutEffect`를 사용하면 DOM 요소의 속성을 변경하거나 DOM 노드를 측정하는 등의 작업을 할 수 있다. 일반적으로 `useLayoutEffect`는 `useEffect`와 동일한 일을 수행하지만, 렌더링 작업을 차단하여 일시적인 지연이 발생할 수 있다.

<br>

### `useLayoutEffect` 예시
```js
import { useState, useLayoutEffect } from 'react';

function Example() {
  const [width, setWidth] = useState(0);

  useLayoutEffect(() => {
    function updateWidth() {
      setWidth(window.innerWidth);
    }
    window.addEventListener('resize', updateWidth);
    updateWidth();
    return () => window.removeEventListener('resize', updateWidth);
  }, []);

  return <p>Window width: {width}px</p>;
}
```

## 정리
- `useEffect`는 브라우저가 컴포넌트를 그리고 난 후 실행되기 때문에 브라우저가 화면에 그리는 것과 상관 없는 비동기적인 작업에 적합하다.
- `useLayoutEffect`는 브라우저가 컴포넌트를 그리기 전에 실행되기 때문에 렌더링 전에 동기적인 작업에 적합하다.
