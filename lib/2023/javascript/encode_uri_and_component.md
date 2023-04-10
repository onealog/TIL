# encodeURI()와 encodeURIComponent()의 차이

업무를 하면서 링크 일부를 인코딩을 할 일이 많은데, 그때마다 `encodeURIComponent()`를 사용한다.
그런데 문득 encodeURI()와 encodeURIComponent()의 차이가 뭔지 궁금해서 찾아보았고, 까먹기 전에 기록을 해두려고 한다.

<br>

## encodeURI()
`encodeURI()` 함수는 URI의 전체를 인코딩한다. 또한 [아래 해당하는 문자는 인코딩 하지 않는다](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI#description).

<br>

```
A–Z a–z 0–9 - _ . ! ~ * ' ( )

; / ? : @ & = + $ , #
```

<br>

`encodeURIComponent()` 함수는 URI 구성 요소 중 일부를 인코딩한다. 그리고 [다음과 같은 문자는 인코딩하지 않는다](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent#description).

<br>

```
A–Z a–z 0–9 - _ . ! ~ * ' ( )
```

<br>

## 예시
```js
encodeURI('https://www.youtube.com/watch?v=9c_ReztGVEg') // 'https://www.youtube.com/watch?v=9c_ReztGVEg'

encodeURIComponent('https://www.youtube.com/watch?v=9c_ReztGVEg') // 'https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D9c_ReztGVEg'
```

<br>

## 정리하면
`encodeURI()`는 전체 URI를 인코딩하고, `encodeURIComponent()`는 URI의 일부를 인코딩할 때 쓴다.
