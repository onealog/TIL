# 빈도수 세기 - 알고리즘 패턴 학습(JS)

취업 후 실무에 집중하다 보니 알고리즘 테스트를 손 놓은지 오래 돼서 오랜만에 풀어보았다.그런데.. 이게 무슨 일인가. 간단한 문제도 생각보다 오래 걸리는 게 아니던가. 그래서 취준할 때를 생각하며, 테스트도 조금씩 풀어보고 개념들을 복기하면서 정리해보려고 한다.   
그 첫 번째는 **빈도수 세기**이다.

> 빈도수 세기란 말 그대로 **특정 문자열, 배열 등이 주어졌을 때 요소들의 빈도수를 체크하여 푸는 방식**이다. 간단한 예제를 통해 빈도수 세기를 알아보고 **알고리즘 효율성**에 대해서도 알아보도록 하자.

<br>

## 예제

> **두 개의 배열이 주어질 때 첫 번째 배열의 요소들이 두 번째 배열에 모두 포함하고 있으면 `true`, 한 개라도 틀리면 `false`를 리턴하는 함수를 만들어보자.**

먼저 우리가 `흔히 생각하는 방법`으로 풀이를 진행하려한다.

<br>

### 흔히 생각하는 방법

```js
function sameArray(arr1, arr2) {
  for (let i = 0; i < arr1.length; i++) {
    // arr1의 요소들이 arr2에 있는지 확인. 있으면 해당 index, 없으면 -1 호출.
    const index = arr2.indexOf(arr1[i]);

    if (index !== -1) {
      // index가 있는 경우에 arr2의 해당 값을 0으로 만들어 체크 표시.
      arr2[index] = 0;
      continue;
    }

    return false; // 없으면 바로 false 리턴.
  }

  return true; // 모든 순회가 끝나면 모두 있다는 뜻이므로 true 리턴.
}

sameArray([1, 2, 3], [3, 2, 1]); // true
sameArray([4, 4, 1], [1, 4, 4]); // true
sameArray([4, 4, 1], [1, 1, 4]); // false
```

<br>

세세한 로직은 다르겠지만 아마 보통 이런식으로 풀지 않을까 생각한다. 푸는 방법이야 사람마다 다르고 뭐가 틀리다, 맞다 할 건 당연히 아니다. 하지만 위 풀이에서 주의 깊게 보아야할 부분이 있는데...

<br>

```js
function sameArray(arr1, arr2) {
  for (let i = 0; i < arr1.length; i++) {
    const index = arr2.indexOf(arr1[i]);
    // ...
```

<br>

바로 이 부분이다. 뭔가 아쉬운 게 없는가?   
생각해보자.

<br>

### Array.prototype.indexOf()

`indexOf`는 특정 배열의 값을 찾아 `index`를 반환하는 메서드이다. 없을 경우에는 `-1`을 반환한다. 즉 모든 값을 순회하여 맞는 값이 있으면 `index`를 반환한다는 점에서 시간 복잡도는 `O(n)`을 가진다.   

결론적으로 위 풀이에서 시간 복잡도는 `O(n^2)`을 가진다. 시간 복잡도 `O(n)`을 가지는 `for`문 안에 또 `O(n)`의 시간 복잡도를 가지는 `indexOf`라는 메서드가 들어갔기 때문이다.

**주어진 배열의 요소가 3개가 아니라 백만 개, 천만 개일 경우 시간 복잡도 `O(n^2)`에 의해 기하급수적으로 복잡도는 올라갈 것이다.**   

**이걸 좀 더 효율적으로 바꾸는 방법이 없을까?**

<br>

### O(n)의 시간 복잡도로 다시 풀어보기

**빈도수 세기 문제는 `O(n)`의 시간 복잡도로 효율적으로 풀 수 있다.**   

위 문제의 경우에도 `O(n)`으로 풀 수 있으며, 특히 빈도수 세기 문제는 **객체를 활용하여 시간 복잡도를 효율적으로 가져갈 수 있다.**

```js
// 시간 복잡도: O(n)
function sameArray(arr1, arr2) {
  const collection = {};

  for (const n of arr1) {
    // arr1을 순회하면서 빈 객체에 값을 하나씩 넣는다.
    if (!collection[n]) {
      collection[n] = 1;
    } else {
      collection[n]++;
    }
  }

  for (const n of arr2) {
    // arr2를 순회하면서 객체에 해당 값이 없으면(또는 0이면) false를 리턴, 있으면 -1을 해준다.
    if (!collection[n]) {
      return false;
    } else {
      collection[n]--;
    }
  }

  return true;
}

sameArray([1, 2, 3], [3, 2, 1]); // true
sameArray([4, 4, 1], [1, 4, 4]); // true
sameArray([4, 4, 1], [1, 1, 4]); // false
```

<br>

코드가 상대적으로 조금 길어지긴 했지만, 위 풀이 경우에는 시간 복잡도 `O(n)`을 가져 더 효율적이다. 중첩된 `for`문을 가지는 게 아니라 각각의 `for`문이기 때문이다. `(O(2n) => O(n))`
