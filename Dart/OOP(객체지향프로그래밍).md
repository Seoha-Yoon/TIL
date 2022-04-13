# OOP(객체지향프로그래밍)

## 1. Class

: 모든 클래스는 Object Class를 상속 받고 있음

```dart
void main() {

  // datetime값 같은 거 예외처리 가능 -> 효율 상승에 영향을 미침
  // const로 선언 시 내용이 같은 인스턴스들은 같은 인스턴스로 취급됨.
  Idol winner1 = const Idol(
    '위너',
    ['강', '김', '송', '이'],
  );

  Idol winner2 = Idol.fromList(
    [
        ['강', '김', '송', '이'],
        '위너',
    ]
  );

}

class Idol {
  final String name;
  final List<String> members;

  // constructor
  Idol(String name, List<String> members)
      : this.name = name,
        this.members = members;

  // const로 선언 가능 (final 선언 )
  // constructor simple.ver
  const Idol(this.name, this.members);

  // named constructor Idol.생성자이름
  Idol.fromList(List values)
      : this.members = values[0],
      : this.name = values[1];

  void sayHello(){
    print('안녕하세요 ${this.name} 입니다.');
  }

  // getter
  String get firstMember{
    return this.members[0];
  }

  // setter -> final 없어야지 사용가
  set firstMember(String name){
    this.members[0] = name;
  }
}
```

* _{클래스이름, 함수 이름, 변수 이름 ...}: private으로 선언
  
  ex) _Idol



## 2. 상속 - Inheritance

```dart
void main() {
  print('----Idol----');
  Idol winner = Idol(
    name: '위너',
    membersCount: 4,
  );
  
  BoyGroup bts = BoyGroup('BTS', 7);
  bts.sayMembersCount();
}

class Idol {
  String name;
  int membersCount;

  Idol({
    required this.name,
    required this.membersCount,
  });

  void sayMembersCount() {
    print('${this.name}은 ${this.membersCount}명의 멤버가 있습니다.');
  }
}

class BoyGroup extends Idol {
  BoyGroup(
    String name,
    int membersCount,
  ) : super(name: name, membersCount: membersCount);

  @override
  void sayMembersCount(){
    print('${super.name}은 보이그룹이고, ${super.membersCount}명의 멤버가 있습니다.');
  }
}
```



## 2. Static

```dart
void main() {
  Employee em1 = Employee('em1');
  Employee em2 = Employee('em2');
  
  Employee.building = '랄라라'; // 클래스 귀속
  
  em1.printNameAndBuilding();
  em2.printNameAndBuilding();
  Employee.printBuilding();
}

class Employee {
  // static은 instance에 귀속되지 않고 class에 귀속됨
  static String? building;
  final String name;

  Employee(
    this.name,
  );

  void printNameAndBuilding() {
    print('제 이름은 $name입니다. $building 건물에서 근무하고 있습니다.');
  }

  static void printBuilding() {
    print('저희는 $building 건물에서 근무 중입니다.');
  }
}


```



## 3. Interface

```dart
void main() {
  // 이때 인터페이스가 인스턴스를 만들 수 있다?!
  // 막는 방법 -> abstract 사용
  IdolInterface test = IdolInterface("예시");
}

// interfaces
// 기능을 강제함
abstract class IdolInterface {
  String name;
  IdolInterface(this.name);
  void sayName();
}

class BoyGroup implements IdolInterface {
  String name;
  BoyGroup(this.name);
  void sayName() {
    print("제 이름은 $name 입니다.");
  }
}
```



## 4. Generic

* 제너릭: 타입을 외부에서 받을 때 사용

```dart
void main() {
  Lecture<String> lecture1 = Lecture('123', 'lecture1');
  Lecture<int> lecture2 = Lecture(123, 'lecture2');
  
  lecture1.printIdType(); // String
  lecture2.printIdType(); // int
}

class Lecture<T>{
  final T id;
  final String name;
  
  Lecture(this.id, this.name);
  
  void printIdType(){
    print(id.runtimeType);
  }
}


```


