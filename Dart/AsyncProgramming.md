# 비동기 프로그래밍 (Async Programming)

-> CPU 사용하는데 효율적으로 사용 가능

-> 서버 요청시 CPU 낭비를 줄임



## 1. delayed

```dart
void main() {
  addNumbers(1,1);
  addNumbers(2,2);
}

void addNumbers(int n1, int n2){
  print("계산 시작 : $n1 + $n2");
  
  // 서버 시뮬레이션
  // delayed - 지연되다
  // 1번 Parameter - 지연할 기간(얼마나) Duration
  // 2번 Parameter - 지연 시간이 지난 후 실행할 함수
  // 2초 뒤에 실행됨.
  Future.delayed(Duration(seconds:2), (){
    print('계산 완료: $n1 + $n2 = ${n1+n2}');
  });
  
  print("함수 완료");
}

```

<result>

계산 시작 : 1 + 1

함수 완료

계산 시작 : 2 + 2

함수 완료

계산 완료: 1 + 1 = 2

계산 완료: 2 + 2 = 4



## 2. await

```dart
void main() {
  addNumbers(1,1);
  addNumbers(2,2);
}

void addNumbers(int n1, int n2) async {
  print("계산 시작 : $n1 + $n2");
  
  // 서버 시뮬레이션
  // await - 다음 코드 실행하지 마라, 기다리는 동안 다음작업 실행
  await Future.delayed(Duration(seconds:2), (){
    print('계산 완료: $n1 + $n2 = ${n1+n2}');
  });
  
  print("함수 완료");
}
```

<result>

계산 시작 : 1 + 1

계산 시작 : 2 + 2

계산 완료: 1 + 1 = 2

함수 완료 : 1 + 1

계산 완료: 2 + 2 = 4

함수 완료 : 2 + 2



addNumbers 함수도 순서대로 실행하고 싶으면?

```dart
void main() async {
  await addNumbers(1,1);
  await addNumbers(2,2);
}

Future<void> addNumbers(int n1, int n2) async {
  print("계산 시작 : $n1 + $n2");
  
  // 서버 시뮬레이션
  // await - 다음 코드 실행하지 마라, 기다리는 동안 다음작업 실행
  await Future.delayed(Duration(seconds:2), (){
    print('계산 완료: $n1 + $n2 = ${n1+n2}');
  });
  
  print("함수 완료");
}
```

<result>

계산 시작 : 1 + 1

계산 완료: 1 + 1 = 2

함수 완료

계산 시작 : 2 + 2

계산 완료: 2 + 2 = 4

함수 완료



## 3. return 값

그냥 return 해주면 Future에 쌓여서 나온다. 단, await 필수!



## 4. Stream

데이터가 흐르고 있음. -> 값을 무한하게 받을 수 있음

함수형 프로그래밍으로 데이터 가공 가능

Future은 완료될 때 값을 한 번만 받을 수 있음



1. 스트림 기본 사용법

```dart
import 'dart:async';

void main() {
  final controller = StreamController();
  // Listner 여러개 쓰기 위해 asBroadcastStream 사용
  final stream = controller.stream.asBroadcastStream();
  
  final streamListener1 = stream.where((val) => val % 2 == 0).listen((val){
    print('Listener 1: $val');
  });
  final streamListener2 = stream.where((val) => val % 2 == 1).listen((val){
    print('Listener 2: $val');
  });
  
  controller.sink.add(1);
  controller.sink.add(2);
  controller.sink.add(3);
  controller.sink.add(4);
  controller.sink.add(5);
}


```

<result>

Listener 2: 1

Listener 1: 2

Listener 2: 3

Listener 1: 4

Listener 2: 5



2. 함수로 사용

```dart
import 'dart:async';

void main() {
  playAllStream().listen((val){
    print(val);
  });
}

Stream<int> playAllStream() async* {
  // Future의 await와 같음
  // 첫번째 함수의 stream이 모두 끝나야지 다음 함수 실행
  yield* calculate(1);
  yield* calculate(1000);
}

Stream<int> calculate(int n) async* {
  for(int i=0; i<5; i++){
    yield i * n;
    
    // thread는 지속되고 있음
    await Future.delayed(Duration(seconds: 1));
  }
}


```










