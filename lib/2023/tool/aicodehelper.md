# VS Code 안에서 사용하는 ChatGPT - AICodeHelper

오늘도 강력한 툴을 하나 알게 되어 소개 + 기록용으로 쓴다. 이름은 **AICodeHelper**다.   
자세한 내용은 아래 소개하는 유튜브 영상에서 확인할 수 있다.   

<br>

AICodeHelper는 VS Code 익스텐션이고, 설치 후에 ChatGPT의 API를 연결하면 사용할 수 있다.   
맥 기준으로 아래 단축키를 사용하여 해당 익스텐션을 활용할 수 있다.   
```
[Shift + Ctrl + Option] + Z : 주석 달기
[Shift + Ctrl + Option] + R : 리팩터링
[Shift + Ctrl + Option] + C : 코드리뷰
[Shift + Ctrl + Option] + G : 자연어 > 코드
[Shift + Ctrl + Option] + M : 개발외 질문
```

내가 작성한 코드가 있다면 해당 코드를 드래그한 후에 위 단축키를 누르면 설명대로 ChatGPT가 동작한다.   
해당 코드를 분석해 주석을 달아주고(`Shift + Ctrl + Option` + `Z`), 리팩터링을 해주고(`~` + `R`), 코드리뷰를 해준다(`~` + `C`).   
또한 자연어로 말을 하면 코드로 바꿔주고(`~` + `G`), 개발외 질문에 대한 답을 해준다(`~` + `M`).   
한마디로 ChatGPT를 VS Code에서 사용할 수 있게 해주는 툴이다.   

<br>

제약이라 한다면 `gpt-3.5-turbo`를 활용하고 있어서 사용할 때 마다 토큰별로 금액이 청구된다([ChatGPT Pricing 참고](https://openai.com/pricing)).   
하지만 금액 자체가 많이 들지 않아서 크게 문제가 된다고 생각하지는 않는다. 오히려 이를 통해 창출되는 가치가 더 크다고 생각한다.   
아직 실무에 직접적으로 사용해보진 않았지만, 왠지 잘 활용한다면 엄청난 가치가 될 수 있을 거라 생각한다.   

<br>

## 소개 영상
[AICodeHelper](https://youtu.be/SQPLPPb_LuE)
