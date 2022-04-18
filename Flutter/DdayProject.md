# D-day Project

## Asset 추가

* pubspec.yaml 에 이미지 및 폰트 추가

```yaml
fonts:
  - family: parisienne
    fonts:
      - asset: asset/font/Parisienne-Regular.ttf

  - family: sunflower
    fonts:
      - asset: asset/font/Sunflower-Light.ttf
      - asset: asset/font/Sunflower-Medium.ttf
        weight: 500
      - asset: asset/font/Sunflower-Bold.ttf
        weight: 700
```



## StatefulWidget의 위치

* 가장 상위 위젯에서 관리하는 게 좋다.

* 하위 위젯에 있는 statefulwidget을 상위로 가져오려면?
  
  * 하위위젯에 상태 변경에 필요한 변수를 받는 생성자 생성
  
  * 상위위젯에서 상태 변경 후 생성자를 통해 하위위젯에 전송



## 테마 적용 (폰트)

* main.dart 파일에서 폰트 규칙을 미리 정해주면, 아무데서나 직접 폰트 이름을 사용하지 않고도 스타일을 적용할 수 있다.

*main.dart*

```dart
void main() {
  runApp(MaterialApp(
    theme: ThemeData(
      fontFamily: 'sunflower',
      textTheme: TextTheme(
        headline1: TextStyle(
          color: Colors.white,
          fontFamily: 'parisienne',
          fontSize: 80.0,
        ),
        headline2: TextStyle(
          color: Colors.white,
          fontWeight: FontWeight.w700,
          fontSize: 50.0,
        ),
        bodyText1: TextStyle(
          color: Colors.white,
          fontSize: 30.0,
        ),
        bodyText2: TextStyle(
          color: Colors.white,
          fontSize: 20.0,
        ),
      ),
    ),
    home: HomeScreen(),
  ));
}

```


