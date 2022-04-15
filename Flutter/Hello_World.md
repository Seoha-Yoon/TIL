# Flutter 시작 - Hello_World

* **Hot Reload**: 상태를 유지한채로 UI 변화, 단 빌드 함수에 있는 코드만 재실행

* **Hot Restart**: 상태를 유지하지않고 빠르게 재시작

* **Widget**: 실제로 화면에 나타나는 것들

*main.dart*

```dart
void main() {
  runApp(
      MaterialApp(
        home: Scaffold(
        backgroundColor: Colors.black,
      // 화면
        body: Center(
          child: Text(
            'Hello World',
            style: TextStyle(
              color: Colors.white,
              fontSize: 20.0,
            ),),),),)
  );
}
```

* **Widget Tree**
  
  MaterialApp -> Scaffold -> Center -> Text

## Splash 화면 만들기

1. Asset 추가하기
   
   * asset/img 폴더 생성해서 이미지 넣기
   
   * pubspec.yaml 파일 수정: asset/img 내의 파일들을 모두 사용하겠다.
   
   * flutter pub get 버튼 클릭

*pubspec.yaml*

```yaml
flutter:
  uses-material-design: true
  # 추가
  assets:
    - asset/img/
```

2. StatelessWidget 사용해보기

*main.dart*

```dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Text('Hello World'),
      ),
    );
  }
}
```

* child: 자식 위젯이 하나 ex) Center

* children: 자식 위젯이 여러개 ex) Row, Column
