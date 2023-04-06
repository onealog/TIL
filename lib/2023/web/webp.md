# WebP - 이미지 포맷

오늘은 WebP에 대해 작성을 해보려고 하는데, 회사의 다음 프로젝트에서 WebP를 활용하기 위해서이다.

<br>

## WebP란?
- 구글이 만든 이미지 포맷
- WebP의 무손실 이미지*는 PNG에 비해 크기가 [26%](https://developers.google.com/speed/webp/docs/webp_lossless_alpha_study?hl=ko#results) 작다.
- WebP의 손실 이미지*는 JPEG에 비해 크기가 [25~34%](https://developers.google.com/speed/webp/docs/webp_study?hl=ko) 작다.

> *무손실 이미지?
> - 이미지 압축시, 이미지의 품질을 유지하면서 압축하는 방식
> - 대표적으로 PNG, GIF가 있다.

> *손실 이미지?
> - 이미지 압축시, 이미지의 품질 저하를 감수하면서 압축하는 방식
> - 대신 무손실 이미지 파일 보다 크기를 더 작게 만들 수 있다.
> - 대표적으로 JPEG가 있다.

<br>

## WebP 지원 브라우저(23.4 기준)

- Can I use - ([링크](https://caniuse.com/webp))

![WebP 지원 브라우저](/assets/2023/web/webp.png)

<br>

## 웹사이트 이미지 포맷 사용 통계(23.4 기준)

- 매일 업데이트가 되는 듯 하다. ([링크](https://w3techs.com/technologies/overview/image_format))

![웹사이트 이미지 포맷 사용 통계](/assets/2023/web/webp2.png)
