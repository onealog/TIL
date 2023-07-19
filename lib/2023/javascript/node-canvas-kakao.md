# node-canvas로 카카오 비즈보드 만들기

현재 진행중인 프로젝트가 있다. 여기서 핵심 기능은 현재 라이브 중인 광고를 카카오 비즈보드 소재로 자동으로 만들어야 한다.   
이에 [node-canvas](https://github.com/Automattic/node-canvas)를 활용하였고, 아래 간략하게 소재를 만드는 코드를 작성한다.   
canvas API([1](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API), [2](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D))를 참고하여 작성했다.   

<br>

<details><summary>
잘 아시다시피 카카오 비즈보드는 이렇게 생겼다.
</summary>

## 카카오 비즈보드
![kakao-bizboard](/assets/2023/javascript/kakao-biz-1.png)

## 가이드
![kakao-bizboard](/assets/2023/javascript/kakao-biz-2.png)
</details>

<br>

## 비즈보드 그리는 로직
```js
const { createCanvas, loadImage, registerFont } = require('canvas');

//...

const makeKakaoBizboard = async () => {
  const mainTitle = '제목';
  const subTitle = '부제목';

  // 캔버스 그리기
  const canvas = createCanvas(1029, 258);
  const ctx = canvas.getContext('2d');

  // 폰트 등록
  registerFont(path.join(__dirname, '/fonts/SpoqaHanSansBold.ttf'), { family: 'SpoqaHanSansBold' });
  registerFont(path.join(__dirname, '/fonts/SpoqaHanSansRegular.ttf'), { family: 'SpoqaHanSansRegular' });

  // 광고 제목 그리기
  ctx.font = '48px SpoqaHanSansBold';
  ctx.fillStyle = '#4C4C4C';

  const [mainX, mainY] = [47, 97];
  ctx.fillText(mainTitle, mainX, mainY);

  // 광고 제목 가로 길이 계산
  const mainWidth = Math.floor(ctx.measureText(mainTitle).width);
  // 광고 제목은 최소 길이(290px 이상) 등 요구사항이 있으므로,
  // 충족하지 못할 경우 그렸던 광고 제목을 삭제 후 다시 그리는 로직 작성

  // 광고 부제목 그리기
  ctx.font = '39px SpoqaHanSansRegular';
  ctx.fillStyle = '#777777';
  const [subX, subY] = [47, 153];
  ctx.fillText(subTitle, subX, subY);

  // 광고주명(외부 DSP명) 표기
  ctx.font = '24px SpoqaHanSansRegular';
  ctx.fillStyle = '#777777';
  ctx.fillText('데이블 광고입니다.', 102, 199);

  // 썸네일 이미지 및 AD 광고 마크 표기
  const thumbnail = await loadImage('사용할 썸네일 이미지');
  const adMark = await loadImage(path.join(__dirname, '/ad-mark.png'));
  const [dx, dy, dWidth, dHeight] = [666, 36, 315, 186];

  ctx.save();

  // 썸네일은 테두리가 round되어 있으므로 round를 만들어주는 함수를 만들어 필요한 파라미터를 넣음
  roundedRect(ctx, dx, dy, dWidth, dHeight, 11);
  ctx.clip();

  ctx.drawImage(thumbnail, dx, dy, dWidth, dHeight);
  ctx.restore();

  ctx.drawImage(adMark, 48, 175, 48, 30);

  const buffer = canvas.toBuffer('image/png', {
    compressionLevel: 3,
    filters: canvas.PNG_FILTER_NONE,
  });

  // 이후 위 buffer를 s3에 업로드하는 로직
  // canvas 이미지 및 여러 정보를 DB에 저장하는 로직
}
```

<br>


## 결과
이런식으로 회사에 보유한 광고들을 카카오 비즈보드 소재에 맞게 만들었고, 아래와 같은 이미지로 생성이 된다.
![bizboard](/assets/2023/javascript/kakao-biz-3.png)
   
기존에 만들어진 광고 제목을 카카오 비즈보드 소재에 맞게 단순히 자르다 보니 어색한 광고 제목들도 있었다. 이것들은 chatGPT를 활용하여 자연스럽게 변경했다. 관련 기록은 추후에 올리도록 하겠다.
