# 정규표현식 Lookbehind

정규표현식 중에 [lookbehind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Regular_expressions/Lookbehind_assertion)라는 녀석이 있다. 이 녀석을 가져온 이유가 무엇이냐면, 실무를 하다 종종 마주쳤기 때문이다.   
웹 프로그래머라면 크롬을 자주 사용하고 디버깅 또한 크롬을 통해 하는 것이 일반적이다. 그런데 이럴 경우 가끔씩 뒤통수를 맞기도 하는데 상대적으로 점유율이 낮은 파이어폭스나 사파리에서 트집을 잡는다. "야 그거 여기서는 안되는데?" 하고 말이다.   

<br>

lookbehind는 특정 단어를 찾아서 조물조물 해줄 때 사용했었는데, 배포 이후에 사파리에서 터졌던 경험이 있다. 그 당시에 뭐가 원인인지 모르다가 결국 lookbehind 때문인 것을 알게 되었다.   
지금 [Can I use](https://caniuse.com/?search=lookbehind)를 확인해보니, 그래도 많이 버전이 올라온 듯하다. 예전에는 사파리, iOS가 한참을 못 미쳤는데 말이다.

![lookbehind-2](/assets/2023/web/lookbehind.png)

<br>

어쨌든 결론은 크롬 말고도 다른 브라우저에 관심 좀 가져주자. 우린 웹 프로그래머니깐.
