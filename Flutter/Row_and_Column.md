# Flutter - Row and Column

* Column과 Row는 여러개의 child를 가질 수 있어서 많이 사용됨

* **SafeArea**: 상태바 제외하고 위젯이 위치할 수 있도록 해줌

## Column and Row

* **MainAxisAlignment**: 주축 정렬
  
  * start - 시작
  
  * end - 끝
  
  * center - 가운데
  
  * spaceBetween - 위젯과 위젯 사이가 동일하게
  
  * spaceEvenly - 위젯을 같은 간격으로 배치 but 빈 간격으로 시작
  
  * spaceAround - 끝과 끝의 간격을 반으로 + spaceEvenly

* **CrossAxisAlignment**: 반대축 정렬
  
  * baseline - 글자 정렬
  
  * start - 시작
  
  * end - 끝
  
  * center - 가운데 (기본값))
  
  * strech - children 안의 값들을 강제로 부모 컨테이너 길이로

*container를 전체 화면 크기로 하는 법*

```dart
width: MediaQuery.of(context).size.width,
height: MediaQuery.of(context).size.height,
```

* **MainAxisSize**: 주축 크기 변경 
  
  * min - 주축 크기 최소로 (위젯들이 최소한으로 차지하는 사이즈)
  
  * max - 주축 크기 최대로 (defalut) 

## Expanded, Flexible

: 무조건 Column과 Row 안에서 사용해야함.

* **Expanded** - 최대한으로 남아있는 모든 사이즈를 차지하라
  
  * 여러 Child에 사용하면, 남아있는 사이즈를 1/n 한다.
  
  * **flex**: 나머지 공간을 분배하는 비율

* **Flexible** - 남아있는 공간을 차지하되, child의 크기보다 크면 나머지 공간을 버림.
