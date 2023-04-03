# 그리디 알고리즘(Greedy Algorithm) - 알고리즘 패턴 학습(JS)

그리디 알고리즘은 매 순간마다 최적이라고 생각되는 선택을 하여 최종 결과를 찾는 알고리즘이다. 이 알고리즘은 전체적인 **최적해**를 보장하지 않지만, 대부분의 경우 최적해와 유사한 결과를 얻을 수 있다.   

> 최적해? : 문제의 조건을 만족하는 가장 좋은 해답

## 예시

가장 많이 사용되는 그리디 알고리즘은 **동전 거스름돈** 문제이다.   
예를 들어, 거스름돈으로 500원, 100원, 50원 ,10원 동전이 있을 때, 1260원을 거슬러주는데 필요한 동전의 최소 개수를 구해보는 문제가 있다고 하자. 이때, 그리디 알고리즘을 사용하면 아래와 같이 풀 수 있다.   

1. 가장 큰 동전부터 사용하여 거스름돈을 만들어 나간다.
2. 현재 선택한 동전으로 거스름돈을 만들 수 있을 때까지 선택한 동전을 계속 사용한다.
3. 만약 선택한 동전으로 거스름돈을 만들 수 없다면, 다음으로 큰 동전을 선택한다.

```js
  function getChange(amount, coins) {
    let change = [];
    let coinIndex = 0;

    while (amount > 0) {
      if (amount >= coins[coinIndex]) {
        change.push(coins[coinIndex]);
        amount -= coins[coinIndex];
      } else {
        coinIndex++;
      }
    }

    return change;
  }

  const coins = [500, 100, 50, 10];
  const amount = 1260;

  console.log(getChange(amount, coins)); // [500, 100, 100, 100, 50, 10]
```
