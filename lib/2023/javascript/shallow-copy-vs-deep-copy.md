# 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)

들어가기 앞서, 예전에 자바스크립트 공부할 때는 학습한 내용인데 실무에서 생각보다 마주칠 일이 많이 없어서 깜빡깜빡할 때가 많다.   
그래서 자바스크립트에 관한 중요한 개념이나 놓치고 있는 것들을 조금 정리하면서 다시 복기하는 시간을 가지면 좋을 것 같다.   
처음으로 가져온 것은 얕은 복사와 깊은 복사이다.   

<br>

## 얕은 복사는 뭐고, 깊은 복사는 뭔가?
일단 둘 다 객체를 복사한다는 공통점을 갖고 있다. 하지만 차이가 있다. 얕은 복사는 객체를 복사할 때 프로퍼티들을 새로운 객체로 복사하지만 내부 참조타입(배열, 객체)은 참조값을 그대로 가져온다. 즉 원본 객체와 복사본이 같은 값을 참조하게 되는 것이다. 반대로 깊은 복사는 객체를 복사할 때 내부 참조타입도 모두 새로운 메모리에 복사하여 모든 값을 완전히 복제한다. 예시를 통해 알아보자.

<br>

## 얕은 복사(Shallow Copy)

얕은 복사는 원본 객체의 내부 참조타입의 참조값을 그대로 가져온다. 따라서 복사본에 해당 참조타입의 변경사항이 원본 객체에도 영향을 미친다.

```js
const originObj = {
  name: 'Jaewon',
  age: 32,
  hobbies: ['climbing', 'eat', 'reading'],
};

// 또 다른 얕은 복사는 `const shallowCopy = { ...originObj }`가 있다.
const shallowCopy = Object.assign({}, originObj);
shallowCopy.hobbies.push('coding');

console.log(originObj.hobbies); // ['climbing', 'eat', 'reading', 'coding']
```

<br>

## 깊은 복사(Deep Copy)

깊은 복사는 원본 객체 내부의 내용들을 새로운 메모리에 복사한다. 따라서 복사본의 변경사항이 원본 객체에 영향을 미치지 않는다.

```js
const originObj = {
  name: 'Jaewon',
  age: 32,
  hobbies: ['climbing', 'eat', 'reading'],
};

// 또 다른 깊은 복사는 lodash의 `_.cloneDeep(originObj)`이 있다.
const deepCopy = JSON.parse(JSON.stringify(originObj));
deepCopy.hobbies.push('coding');

console.log(originObj.hobbies); // ['climbing', 'eat', 'reading']
console.log(deepCopy.hobbies); // ['climbing', 'eat', 'reading', 'coding']
```

<br>

## 정리

- 얕은 복사를 사용하고 싶을 때는 원본 객체가 단순값이거나, 중첩된 객체나 배열이 없는 경우 사용하자.
- 깊은 복사를 사용하고 싶을 때는 원본 객체가 중첩된 객체나 배열이 있는 경우 사용하자.
