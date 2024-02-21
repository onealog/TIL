# Data를 가져올 때 StatelessWidget VS StatefullWidget

다음 2가지의 예시가 있다.

```dart
# 1)
class Screen1 extends StatelessWidget {
  Screen1({super.key});

  final Future<Model1> data1 = ApiService.getData1();

  // ...
}
```

```dart
# 2)
class Screen2 extends StatefulWidget {
  String title, id;

  Screen2({
    super.key,
    required this.title,
    required this.id,
  });

  @override
  State<Screen2> createState() => _ScreenState();
}

class _ScreenState extends State<Screen2> {
  late Future<Model2> data;

  @override
  void initState() {
    super.initState();
    data = ApiService.getData2(widget.id);
  }

  // ...
}
```

<br>

똑같이 `ApiService`에서 `Data`를 `Fetching`하는 `getData` 함수를 이용하여 비동기 처리를 하는 로직인데, 차이점이 있다.   
1번은 `StatelessWidget`으로 간단하게 가져오는 반면, 2번은 `StatefullWidget`과 동시에 `initState`를 필요로 한다.   

<br>

그 이유는 간단하다. 1번의 경우 전달할 `argument`가 전혀 없다. 하지만 2번의 경우 `widget.id`를 전달해야 하기 때문에 `StatefullWidget`에서 `initState`를 필요로 하는 것이다.