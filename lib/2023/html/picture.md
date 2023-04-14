# `<picture>` 태그에 대한 설명

회사에서 이번 프로젝트에 들어 갈 때 `<picture>` 태그를 사용할 일이 있을 것 같아서 공부를 해보았다.

<br>

## `<picture>` 태그란?
`<picture>` 태그는 HTML5에서 도입된 이미지 태그로, 웹 페이지에서 다양한 미디어 쿼리를 사용하여 여러 해상도와 환경에 맞게 다양한 이미지 리소스를 제공하는 데 사용된다. 이를 통해 웹 페이지가 빠르게 로드되고 높은 화질의 이미지를 보여줄 수 있다.`<picture>` 요소는 일반적으로 `<img>` 요소를 포함하고 있으며, `<source>` 요소를 사용하여 다양한 이미지 리소스를 제공한다. 이때 `<source>` 요소에는 이미지의 해상도, 크기, 확장자 등을 지정하는 속성들이 있다.

`<picture>` 요소 안에는 **최소한 한 개의 `<source>` 요소와 하나의 `<img>` 요소가 포함되어야 한다.** `<source>` 요소를 여러 개 사용하면 웹 브라우저는 그 중 적절한 이미지를 선택하여 사용한다. 만약 웹 브라우저가 지원하지 않는 경우, `<img>` 요소가 대신 표시된다.

`<picture>` 요소를 사용하면 웹 페이지의 이미지가 사용자의 화면 크기와 해상도에 적절하게 맞춰질 수 있다. 또한, 이미지의 선명도와 압축률 등의 특성을 고려하여 최적의 이미지를 제공할 수 있다는 점도 매우 유용하다. 따라서, 반응형 웹 디자인을 구현하는 데 매우 유용한 요소이다.

<br>

## `<img>`와 `<picture>`의 차이점
`<picture>` 태그와 `<img>` 태그의 가장 큰 차이점은 이미지 리소스의 다양성과 선택 방식에 있다.

`<img>` 태그는 한 개의 이미지 리소스만을 지정할 수 있다. 따라서, 이미지의 크기나 해상도가 사용자의 화면 크기와 맞지 않으면 이미지가 깨지거나 원래의 크기와 다르게 보이는 문제가 발생할 수 있다. 이에 반해, `<picture>` 요소는 여러 개의 이미지 리소스를 지정할 수 있다. 이때 `<source>` 요소의 조건에 따라 웹 브라우저는 가장 적절한 이미지를 선택하여 사용자에게 제공한다.

`<picture>` 요소에서는 이미지 리소스의 선택 기준을 `<source>` 요소의 속성에 따라 설정할 수 있다. 예를 들어, `<source>` 요소에서는 `media` 속성을 사용하여 사용자의 장치 환경에 따라 이미지 리소스를 선택할 수 있고, `type` 속성을 사용하여 이미지의 파일 형식을 지정할 수 있다.

또한, `<picture>` 요소에서는 `<img>` 요소와 달리 `fallback` 이미지를 설정할 필요가 없다. `<picture>` 요소에는 `<img>` 요소도 포함되어 있기 때문에, 웹 브라우저가 `<picture>` 요소를 지원하지 않는 경우에도 `<img>` 요소를 사용하여 이미지를 제공할 수 있다.

<br>

## `<picture>` 태그 예시

### 1. 미디어 쿼리를 사용한 다양한 크기의 이미지 제공

해당 코드는 화면 크기에 따라 다른 이미지 리소스를 제공한다. 화면 너비가 `1200px` 이상이면 `large-image.jpg`를, `768px` 이상이면 `medium-image.jpg`를, 그 외의 경우에는 `small-image.jpg`를 사용한다.

```html
<picture>
  <source media="(min-width: 1200px)" srcset="large-image.jpg">
  <source media="(min-width: 768px)" srcset="medium-image.jpg">
  <img src="small-image.jpg" alt="Small Image">
</picture>
```

<br>

### 2. 다양한 이미지 형식 제공

해당 코드는 이미지 형식에 따라 다른 이미지 리소스를 제공한다. 웹 브라우저가 WebP 이미지를 지원하는 경우에는 `image.webp`를 사용하고, 그 외에는 `image.jpg`를 사용한다.

```html
<picture>
  <source type="image/webp" srcset="image.webp">
  <source type="image/jpeg" srcset="image.jpg">
  <img src="image.jpg" alt="Image">
</picture>
```

<br>

### 3. WebP 이미지 지원 여부 체크

해당 코드는 웹 브라우저가 WebP 이미지를 지원하는 경우에는 `image.webp`를 사용하고, 그렇지 않은 경우에는 `fallback` 이미지로 `image.jpg`를 사용한다. 이때, `onerror` 속성을 사용하여 WebP 이미지 로드에 실패한 경우에는 `fallback` 이미지를 사용하도록 설정한다.

```html
<picture>
  <source type="image/webp" srcset="image.webp" onerror="this.onerror=null;this.src='image.jpg'">
  <img src="image.jpg" alt="Image">
</picture>
```

### 23.4.14 추가
사실상 WebP 이전에 `<picture>` 태그도 [IE에서 지원하지 않는다](https://caniuse.com/picture). 그러면 IE 브라우저일 경우에 `<picture>` 태그는 아예 노출이 안되는가? 라는 의문이 들 수 있다.   
그렇지 않다. `<picture>` 태그 안에 `<img>` 태그가 있다는 가정하에 말이다. IE에서 `<picture>` 태그를 만나면 해당 태그는 무시하고 내부에 `<source>` 태그 또한 무시한다. 그 다음 `<img>` 태그의 `src` 속성을 읽어 이미지를 노출한다. 즉 IE에도 `<picture>` 태그를 사용할 수 있다.
