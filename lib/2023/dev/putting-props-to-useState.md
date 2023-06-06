# props를 useState에 전달하기

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
