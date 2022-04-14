# StatefulWidget

## Widget

* 위젯은 모두 불변이라 변경 시 기존 위젯을 삭제하고, 새로운 위젯을 생성한다.



## StatelessWidget

* Constructor -> build

* 라이프사이클 한 번 동안 한 번의 빌드만 실행됨



## StatefulWidget

* Constructor -> createState

<img title="" src="file:///var/folders/lf/rtm5_zvx4612t2g0hlkznr7m0000gn/T/TemporaryItems/NSIRD_screencaptureui_72iVoE/스크린샷%202022-04-14%20오후%209.31.15.png" alt="스크린샷 2022-04-14 오후 9.31.15.png" width="522">

* stful 로 자동 생성 가능

* state를 설정한 위젯 클래스 내의 값을 가지고 오고 싶으면 widget.을 사용하면 된다.

* Widget이 존재하는 State를 보고 변경된다.





## Gesture Detector

: Gesture Detector가 감싸고 있는 위젯 내 모든 행동 감지,

```dart
@override
  Widget build(BuildContext context) {

    return GestureDetector(
      onTap: () {
        setState(() {
          number++; // 변경 값이 화면에 나타남.
        });
      },
      child: Container(
        width: 50.0,
        height: 50.0,
        color: widget.color,
        child: Center(
          child: Text(number.toString()),
        ),
      ),
    );
  }
```


