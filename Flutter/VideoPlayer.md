# Video Player

* video_player dependency 추가 중 오류 발생

```
 A package may not list itself as a dependency.
```

프로젝트 이름과 dependency 이름이 같아서 난 오류.

모듈명과 다른 프로젝트 이름을 사용해야함!

## 배경 그라데이션

BoxDecoration 사용

```dart
BoxDecoration getBoxDecoration() {
  return BoxDecoration(
    gradient: LinearGradient(
      begin: Alignment.topCenter,
      end: Alignment.bottomCenter,
      colors: [
        // 색 리스트
      ],
    ),
  );
}
```

## Image Picker

파일을 가져올 때까지 기다려야 하므로 async 사용

XFile 형태로 받아온다.

```dart
final video = await ImagePicker().pickVideo(
  source: ImageSource.gallery,
);
```

## Video 재생

* initState단계에서 controller 생성.
  
  이 때, async로 생성해야하는데, initState에서는 async를 사용하지 못하므로 따로 initController 함수를 async를 만들어준다.
  
  ```dart
  initializeController() async {
    videoController = VideoPlayerController.file(
      // dart.io
      File(widget.video.path),
    );
  
    await videoController!.initialize();
  
    setState(() {});
  }
  ```
  
  * XFile을 File 형태로 바꿔준다.
  
  * setState 호출을 통해 빌드해준다.

* VideoPlayer위젯에 videoController를 넣으면 영상이 실행된다.

* 영상 비율 맞추기 -> AspectRatio 위젯으로 VideoPlayer 감싸줌



## Video 버튼 만들기 - Stack
