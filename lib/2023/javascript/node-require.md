# node 명령어로 특정 js 파일을 실행할 때 path 설정

오늘 업무를 하면서 안 사실.   
`node`` 명령어로 특정 `js`파일을 실행할 때 어떻게 실행하느냐에 따라서 해당 `js` 안에 파일을 불러오는 경로를 변경해줘야 한다.   

## 2가지의 경우 예시
1. `node lib/user/run.js`를 했을 때, `run.js` 안에 코드에서 특정 경로의 파일을 불러 올 때 `"./lib/user/fonts/...` 이런 식으로 사용해야 한다.
2. 직접 `user` 디렉터리로 들어가 `node run.js`를 하면 위 경로를 `"./fonts/...` 이런 식으로 사용해야 한다.

## 해결 방법
- 위 처럼 사용해도 되나, 모두 절대 경로로 바꿔주면 위의 2가지 경우 모두 아래처럼 사용할 수 있다.

```js
const pathA = __dirname + '/fonts/...';

// 또는
const path = require('path');
const pathB = path.join(__dirname, '/fonts/...');
```

### 리드님의 답변
다음 안 사실을 팀 채널에 공유했는데, 리드님이 답변한 게 있다.
- 파일의 절대 경로를 구하는 거라면 `join` 보다는 `resolve`가 조금 더 안전하다. 단순히 합치기만 하는 `join`과 달리 `resolve`는 상대 경로도 정리해주는 등 처리해주는 게 조금 더 있다.
- 그리고 ESM에서는 `__dirname`이 없는데 이럴 때는 `import.meta.url`로 현재 파일명을 구하고 `dirname`을 사용해서 동일한 값을 얻을 수 있다.
