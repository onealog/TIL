# 응답 헤더 가져오는 명령어 `curl -I`

오늘 회사에서 재밌는 명령어를 알게 되었다. `curl -I`라는 명령어이다. `curl`이란 명령어에 `-I`를 붙인 뒤 URL을 입력하면 해당 URL의 서버로 요청을 보낸 후 응답 헤더를 가져올 수 있다.   
다음과 같이 사용할 수 있다.   

<br>

```
$ curl -I https://naver.com

HTTP/2 301
server: NWS
date: Sun, 21 May 2023 12:32:30 GMT
content-type: text/html
location: http://www.naver.com/
vary: Accept-Encoding,User-Agent
referrer-policy: unsafe-url
```

<br>

`curl` 명령어는 평소에 사용하지 않아서 잘 몰랐는데, URL을 통해 데이터를 전송하거나 받을 수 있는 다목적 명령줄 도구라고 한다.   
CPO님이 이번에 내가 참여한 WebP 지원 프로젝트에서 기존 `jpeg` 확장자와 `webp` 확장자의 크기를 비교하기 위해 `curl -I`라는 명령어를 사용했는데 신기해서 놓치지 않고 나도 써먹었다. 기록을 위해 여기 남긴다.   
참고로, 아래처럼 사용했고 테스트로 가져왔는데 해당 이미지는 `webp` 확장자가 **42.15%** 나 용량이 적다. 트래픽 비용이 얼마나 절감될지 기대가 된다.   

<br>

![curl-i](/assets/2023/web/curl-i.png)
