# Random Number Project

## Const Constructor

* Widget을 const로 선언하면, 앱이 실행하는 동안 단 한번만 빌드 실행

* 효율성이 높아진다. 리소스 사용을 줄인다.

* 변수값을 넣을 시에는 사용하지 못한다.



## 버튼 사이즈 정하기

* **SizedBox** - width: double.infinity

* **Container** - width: double.infinity

-> Container보다 SizedBox는 사이즈만 조정하는 곳에만 사용되므로 단순하다.

* **Row with Expanded** - 버튼을 row로 감싼 뒤 Expanded로 감싸주기



## Color

lib/constant/color.dart에 계속 사용할 컬러들을  const로 미리 저장해놓음

```dart
const Color PRIMARY_COLOR = Color(0xFF2D2D33);
const Color RED_COLOR = Color(0xFFEA4955);
const Color BLUE_COLOR = Color(0xFF549FBF);
```



## Padding

양 옆 간격 띄우기

* EdgeInsets.zero - 패딩 0

* EdgeInsets.all - 상하좌우 모두

* EdgesInsets.fromLTRB - 상하좌우 다른값

* EdgesInsets.only - named parameter 이용

* symmetrics - horizontal(좌우), vertical(상하)





## Map으로 인덱스활용하기

```dart
final numbers = [123, 456, 789];

/*
(MapEntry(index:value), ...)
*/
print(numbers.asMap().entries);
```

asMap().entries를 이용해서 해당 value의 index를 key값을 통해 알 수 있다.





## 난수 생성하기

dart.math의 Random 클래스 이용

rand.nextInt(int maxvalue);

```dart
final rand = Random(1000);

```



## 화면 이동 (Navigation)

* 다른 화면으로 이동하기

```dart
onPressed: () {
    Navigator.of(context).push(
        MaterialPageRoute(
            // build 함수와 같음
            builder: (BuildContext context){
                return SettingsScreen();
            },
        ),
    );   
},
```

* 뒤로가기

```dart
onPressed: () {
    Navigator.of(context).pop() 
},
```

* 데이터 전달하기

*send_page.dart*

: pop에 value를 담아 보냄

```dart
onPressed: () {
    Navigator.of(context).pop(value) 
},
```

*receive_page.dart*

: 미래에 받을 값이기에 async로 선언, push에 generic을 이용해 결과값의 타입 지정 가능

: 이때 Navigator를 통해서 들어오는 값은 null일 가능성이 있기 때문에, null 처리를 꼭! 해줘야 한다.

```dart
onPressed: async () {
    final result = await Navigator.of(context).push<int>(
        MaterialPageRoute(
            // build 함수와 같음
            builder: (BuildContext context){
                return SettingsScreen();
            },
        ),
    );   
},
```



* 변수 전달하기

*send_page.dart*

생성자를 통해서 변수 값 전달

```dart
onPressed: async () {
    final result = await Navigator.of(context).push<int>(
        MaterialPageRoute(
            // build 함수와 같음
            builder: (BuildContext context){
                return ReceiveScreen(value: value, );
            },
        ),
    );   
},
```

*receive_page.dart*

initState 단계에서 변수 갱신. state가 생성될 때!

```dart
@override
void initState() {
  super.initState();
  value = widget.value.toDouble();
}
```



## Slider

slider를 통해 maxNumber를 지정해주는 역할

```dart
Slider(
    value: maxNumber,
    onChanged (double val){
        maxNumber = val;
    }
)
```

위와 같은 코드를 작성하면 슬라이더가 빌드되지 않아 움직이지 않는다. 값은 바뀐다.

setState안에서 값을 바꿔야지 슬라이더가 움직인다.

```dart
Slider(
    value: maxNumber,
    onChanged (double val){
        setState((){
            maxNumber = val;
        });
    },
),
```


