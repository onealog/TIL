# <img> 태그의 `src` 속성으로 API 엔드 포인트를 사용하는 방법

보통 `<img>` 태그 안에 `src` 속성을 사용할 때 레포에 있는 이미지를 사용한다. 그런데 업무에서 내부 이미지 말고 API 엔드 포인트를 통해 백엔드에서 이미지를 받아와야 하는 경우가 있다.
이걸로 삽질을 조금해서 간단하게 기록하려고 한다.

<br>

```js
// 아래와 같은 형태의 img 태그가 있다고 할 때,

<img src="{host}/api/thumb">


// Express.js 에서는 아래와 같이 처리한다.

app.get('/api/thumb', (req, res) => {
  // ...

  res.redirect('https://cdn.litt.ly/images/QbHSJonHT45aDntAucXQbmuAboHJmg9U?s=360x360&f=webp');
});
```

<br>

다른 방법도 있을 것 같긴한데, 일단은 이렇게 해보고 또 다른 방법이 있다면 나중에 기록해야지.
