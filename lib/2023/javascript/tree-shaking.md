# Tree Shaking에 관하여

Tree Shaking은 친숙한 개념이긴한데, 오늘 코드리뷰를 하다가 몰랐던 부분이 있어서 정리하고자 이렇게 글을 쓴다.   

<br>

## Tree Shaking 개념
Tree Shaking은 JavaScript ES6의 모듈 시스템을 사용할 때, 사용하지 않는 코드를 제거해주는 기능이다. 즉 모듈 번들러에서 번들을 할 때 사용하지 않는 코드를 제거함으로써 번들 크기를 줄이는 코드 최적화 기술이라고 할 수 있다.   

대부분의 모듈 번들러에서는 Tree Shaking을 자동으로 지원한다. 하지만 수동으로 설정해야 할 수도 있는데 `package.json`에 `"sideEffects": false`를 추가해주면 해당 패키지의 모든 모듈이 side effect가 없다고 가정하고 Tree Shaking을 수행한다.

<br>

## 그러면 서버쪽 코드는 Tree Shaking이 되지 않는가?
서버쪽 코드는 일반적으로 모듈 번들러를 사용하지 않는다. 그래서 Tree Shaking과 같은 최적화 기술을 사용할 필요가 없을 수 있다. 하지만 서버 쪽에서도 번들링을 하는 경우가 있고 때때로 웹팩을 이용하거나, Lambda를 사용하는 경우에 Tree Shaking을 사용해서 번들 크기를 최적화 할 수 있다고 한다. 그러니 자신의 프로젝트에서 서버쪽 코드를 확인하고 Tree Shaking이 필요한지 불필요한지 파악하여 적절하게 활용하면 좋을 것 같다.

<br>

## 참고 링크
- [Tree Shaking 을 통한 모듈 용량 최적화](https://techblog.wclub.co.kr/posts/0001.tree-shaking/Tree%20Shaking%20%EC%9D%84%20%ED%86%B5%ED%95%9C%20%EB%AA%A8%EB%93%88%20%EC%9A%A9%EB%9F%89%20%EC%B5%9C%EC%A0%81%ED%99%94)
