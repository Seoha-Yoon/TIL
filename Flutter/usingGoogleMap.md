# 구글 지도 사용하기

## 환경 세팅

1. pub.dev 에서 플러그인 복사해서 dependency에 추가

2. 이용할 때 필요한 사항 체크 후 파일 수정
   
   * API 키 가져오기
   
   * 위치 권한 설정

## GoogleMap 위젯 사용하기

* mapType을 통해 지도 종류 고를 수 있음.

* *initialCameraPosition*: 처음 화면 킬 때 뜨는 위치 설정
  
  * LanLng 클래스로 설정 가능

* *circles*: 지도에 원을 그릴 수 있음. 이 때 Set으로 값을 받기 때문에 circle의 id를 다 다르게 설정해주어야함.

* *markers*: circle과 같음.

## Geolocator 위치권한 설정하기

[Geolocator Docs]((https://pub.dev/documentation/geolocator/latest/))

* **FutureBuilder**
  
  * future 파라미터에 Future를 리턴해주는 함수 넣기
  
  * snapshot을 통해 future에 있는 함수의 리턴값을 받을 수 있음.
    
    * snapshot.data: return값
    
    * snapshot.connectionState: 함수 상태
      
      * done - future에 아무 함수도 없을 때
      
      * waiting - 함수 실행 중
      
      * done - 함수 실행 끝

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: FutureBuilder(
      future: checkPermission(), 
      builder: (BuildContext context, AsyncSnapshot snapshot) 
        return // 화면
  );
}
```

*checkPermission 함수*

```dart
Future<String> checkPermission() async {
  final isLocationEnable = await Geolocator.isLocationServiceEnabled();

  if (!isLocationEnable) {
    return '위치 서비스를 활성화 해주세요.';
  }

  LocationPermission checkPermission = await Geolocator.checkPermission();

  if (checkPermission == LocationPermission.denied) {
    checkPermission = await Geolocator.requestPermission();

    if (checkPermission == LocationPermission.denied) {
      return '위치 권한을 허가해주세요.';
    }
  }

  if (checkPermission == LocationPermission.deniedForever) {
    return '앱의 위치 권한을 세팅에서 허가해주세요.';
  }

  return '위치 권한을 허가되었습니다';
}
```

* 권한 요청과 같은 경우는 유저가 선택하는 미래의 값을 받아서 사용하므로 async 사용

* Geolocator.isLocationServiceEnabled(): 위치 서비스 활성화 되어있는지 확인

* Geolocator.checkPermiission(): 위치 권한 확인
  
  * LocationPermisson: 앱에선 4가지 상태 사용
    
    * denied: 권한 거절, 다시 요청 가능
    
    * deniedForever: 권한 거절, 다시 요청 불가능
    
    * whileInUse, always



## Geolocator 이용해서 현재위치 가져오기

```dart
final location = await Geolocator.getCurrentPosition(
 desiredAccuracy: LocationAccuracy.lowest,
);
```

* 이때, default desiredAccuracy는 best다.. 그런데 작동하지 않아서 accuracy를 낮췄더니 잘 작동했다.

* 이에 대한 이유는 조금 더 알아봐야할 것 같다.


