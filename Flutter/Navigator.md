# Navigator

pop, push 시 Stack과 같은 형태로 되어있음.

## Argument 전달하기

* 생성자로 전달

* pop에 담아서 전달 (async, await) 사용

* settings의 arguments로 전달

*route_one.dart*

```dart
ElevatedButton(
  onPressed: () {
  Navigator.of(context).push(
    MaterialPageRoute(
      builder: (_) => RouteTwoScreen(),
      settings: RouteSettings(
        arguments: 789,
      ),
    ),
   );
  },
 child: Text('Push'),
)
```

*route_two.dart*

```dart
final arguments = ModalRoute.of(context)!.settings.arguments;
```



## Named Route

main.dart에서 각 스크린으로 주소를 매핑해준 뒤, 사용할 수 있다.

*main.dart*

```dart
void main() {
  runApp(
    MaterialApp(
      initialRoute: '/',
      // home: HomeScreen(),
      routes: {
        '/': (context) => HomeScreen(),
        '/one': (context) => RouteOneScreen(),
        '/two': (context) => RouteTwoScreen(),
        '/three': (context) => RouteThreeScreen(),
      },
    ),
  );
}
```

* two -> three using named route

*two.dart*

```dart
ElevatedButton(
  onPressed: () {
    Navigator.of(context).pushNamed('/three', arguments: 999);
  },
  child: Text('Push Named'),
)
```

pushNamed를 사용할 땐, parameter로 argument 값을 다른 페이지로 전송할 수 있다.



## Push 메소드

* **pushReplacement(builder)**
  
  현재 라우터를 지우고 push, 현재 라우터 대체

* **pushAndRemoveUntil**
  
  (route) 파라미터로 모든 라우터를 받음. (route) => false로 삭제함.

```dart
ElevatedButton(
  onPressed: () {
    Navigator.of(context).pushAndRemoveUntil(
      MaterialPageRoute(builder: (_) => RouteThreeScreen()),
        // 홈스크린만 남김.
        (route) => route.settings.name == '/',
      );
    },
  child: Text('Push and Remove Until'),
)
```

* Push를 사용하면, App Bar에 자동으로 뒤로가기 버튼이 생김.



## Pop 메소드

* **maybePop()**
  
  더이상 뒤로갈 페이지가 없으면 실행되지 않음. canPop() == true;

* **canPop()**
  
  false - pop을 할 수 없음. true - pop을 할 수 있음.

* 만약 시스템에서 제공하는 뒤로가기를 누른다면?
  
  * 라우터가 사라질 때의 이벤트를 이용해서 막는다!
  
  * **WillPopScope 사용**
  
  ```dart
  WillPopScope(
      onWillPop: () async {
          // true - pop 가능
          // false - pop 불가능
          final canPop = Navigator.of(context).canPop();
          return canPop;
      }
  )
  ```
  
  
  
  
