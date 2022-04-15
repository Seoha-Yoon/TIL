# PageView

## PageView

* 스크롤로 화면을 바꿀 수 있는 뷰.

```dart
Scaffold(
      body: PageView(
        children: [
          Image.asset('asset/img/image_1.jpeg'),
          Image.asset('asset/img/image_2.jpeg'),
          Image.asset('asset/img/image_3.jpeg'),
          Image.asset('asset/img/image_4.jpeg'),
          Image.asset('asset/img/image_5.jpeg'),
        ],
      ),
    );
```

## 함수형 프로그래밍 사용

```dart
Scaffold(
      body: PageView(
        children: [1, 2, 3, 4, 5]
            .map(
              (e) => Image.asset(
                'asset/img/image_$e.jpeg',
                // 이미지 전체화면 (비율에 맞게 늘려줌)
                fit: BoxFit.cover,
              ),
            )
            .toList(),
      ),
    );
```

## Timer

* Future와 사용법이 같음

* state init 시 생성, dispose 시 소멸 설정

```dart
Timer? timer;

@override
void initState() {
  super.initState();
  timer = Timer.periodic(Duration(seconds: 1), (timer) {});
}

// 위젯이 삭제될 때, 메모리 소비 방지
@override
void dispose() {
  if (timer != null) {
    timer!.cancel(); // timer 끝!
  }
  super.dispose();
}
```

## PageController

* PageController 선언

```dart
PageController controller = PageController(
  initialPage: 0,
);
```

* PageView에 controller 넣어주기

```dart
body: PageView(
      controller: controller,
```

* 2초마다 이미지 바꾸기

```dart
timer = Timer.periodic(Duration(seconds: 2), (timer) {
    int currentPage = controller.page!.toInt();
    int nextPage = currentPage + 1;

    if (nextPage > 4) {
      nextPage = 0;
    }

    controller.animateToPage(nextPage,
        duration: Duration(milliseconds: 400), curve: Curves.linear);
  });
```
