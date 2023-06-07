# props를 useState에 전달하기

- 읽은 블로그 : https://www.philly.im/blog/putting-props-to-use-state

<br>

React에서 `props`로 받은 값을 `state`에 초기화하는 상황일 때를 생각해보자. 흔하게 사용하는 방법이고, 그 자체로 문제가 되지 않는다. 하지만 여기에는 잠재적인 문제가 있다.   
다음 예시를 살펴보자.

```js
import React, { useState } from 'react';

const persons = [
  {
    id: 1,
    name: 'Jaewon',
    email: 'oneadev@gmail.com',
  },
  {
    id: 2,
    name: 'Han',
    email: 'han@abc.com'
  },
];

function App() {
  const [selected, setSelected] = useState(persons[0]);

  return (
    <div>
      {persons.map((person) => (
        <button
          type='button'
          key={person.id}
          onClick={() => setSelected(person)}
        >
          {person.id === selected.id ? person.name.toUpperCase() : person.name}
        </button>
      ))}
      <DetailView initalEmail={selected.email} />
    </div>
  );
}

function DetailView({ initalEmail }) {
  const [email, setEmail] = useState(initalEmail);

  return (
    <div>
      <input
        type='text'
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button type='button' onClick={() => alert(email)}>
        Apply
      </button>
    </div>
  );
}
```

해당 코드는 원하는대로 정상 작동하지 않는다. 왜 그럴까?   

<br>

## useState 초기값
리렌더 시는 useState hook의 초기값이 항상 버려진다. 초기값은 오직 컴포넌트가 마운트 될 때만 사용된다.   

Han을 클릭했을 때 DetailView 컴포넌트는 리렌더가 된다. 이것은 Han의 이메일이 초기값으로 state에 담기지 않는 것을 의미한다.   
이것으 다루기 위한 3가지 방법이 있다.

<br>

다음 3가지 방법은 [여기](https://www.philly.im/blog/putting-props-to-use-state)에서 자세히 설명하고 있다.

1. DetailView 컴포넌트 조건부 렌더
2. State 끌어올리기
3. key 속성을 이용한 완전히 제어되지 않는 컴포넌트

<br>

## 해결 방법이 아닌 것
여기서 다음과 같이 `useEffect`를 사용하여 해결하려고 하는 경우가 있다. 이 경우는 참고한 글에서 안티 패턴이라고 소개하고 있다.

```js
function DetailView({ initialEmail }) {
  const [email, setEmail] = useState(initialEmail);

  useEffect(() => {
    setEmail(initialEmail);
  }, [initialEmail]);

  return (...);
}
```
