# Button

## **Elevated Button**

: 3D 형태

```dart
ElevatedButton(
  onPressed: () {},
  style: ElevatedButton.styleFrom(
    // 메인 색
    primary: Colors.red,
    // 글자, 애니메이션 색
    onPrimary: Colors.black,
    // 그림자 색깔
    shadowColor: Colors.green,
    // 3D 입체감의 높이
    elevation: 10.0,
    textStyle: TextStyle(
      fontWeight: FontWeight.w700,
      fontSize: 20.0,
    ),
    padding: EdgeInsets.all(32.0),
    // 테두리
    side: BorderSide(
      color: Colors.black,
      width: 4.0,
    ),
  ),
  child: Text(
    'ElevatedButton',
  ),
),
```





## **Outlined Button**

: 테두리만 있는 형태

* primary가 onPrimary 역할까지 함.

* background color로 배경색 정할 수 있음.

* elevation 넣으면 elevation button으로 사용 가능.



## **Text Button**

: Text만 있는 형태

* primary가 onPrimary 역할까지 함.



## Style Button using ButtonStyle

* MaterialStateProperty : Material의 상태에 따라서 값이 결정된다.
  
  * all : 아무때나 다 적용
  
  ```dart
  MaterialStateProperty.all(Colors.black)
  ```
  
  * resolve with : 상태에 따라서 다르게 적용
  
  ```dart
  foregroundColor: MaterialStateProperty.resolveWith(
      (Set<MaterialState> states) {
         if (states.contains(MaterialState.pressed)) {
           return Colors.white;
         }
         return Colors.red;
  }),
  ```
  
  

* **Material State**
  
  * hovered - 호버링 상태 (마우스 커서를 올려놓은 상태, 모바일 사용 불가)
  
  * focusted - 포커스 됐을 때 (텍스트 필드)
  
  * pressed - 눌렸을 때,
  
  * dragged - 드래그 됐을 때,
  
  * selected - 선택됐을 때(체크박스, 라디오박스)
  
  * scrollUnder - 다른 컴포넌트 밑으로 스크롤링 됐을 때
  
  * disabled - 비활성화 됐을 때, ex) onPressed가 null
  
  * error - 에러상태
  
  * 기본상태


