# Functional Programming

형변환, chaining이 특징

## 1. 형변환

```dart
void main() {
  List<String> drinks = ['콜라', '사이다', '환타'];
  
  print(drinks);
  
  // List to Map
  print(drinks.asMap());
  // List to Set
  print(drinks.toSet());
  
  
  // Map to List
  Map drinksMap = drinks.asMap();
  print(drinksMap.keys.toList());
  print(drinksMap.values.toList());
  
  // Set to List
  Set drinksSet = Set.from(drinks);
  print(drinksSet.toList());
  
}
```



## 2. map()

1. List

```dart
void main() {
  List<String> drinks = ['콜라', '사이다', '환타'];
  
  // x는 파라미터, 리스트의 모든 멤버들
  final newDrinks1 = drinks.map((x){
    return '맛있는 $x';
  });
  
  final newDrinks2 = drinks.map((x) => '맛있는 $x');
}


```

map을 사용하게 되면 다른 객체가 된다.

newDrinks1과 newDrinks2는 다르다.

2. Map

```dart
void main() {
  Map<String, String> harryPotter = {
    'Harry Potter': '해리포터',
    'Ron Weasely': '론 위즐리',
    'Hermione Granger': '헤르미온느 그레인저',
  };

  // map to map
  final result = harryPotter.map((key, value) => MapEntry(
        'Harry Potter Character $key',
        '해리포터 캐릭터 $value',
      ));
  
  // key to list
  final keys = harryPotter.keys.map((x)=> 'HPC $x').toList();
  
  // value to list
  final values = harryPotter.values.map((x) => '해리포터 $x').toList();
}
```



## 4. where()

```dart
void main() {
  List<Map<String, String>> drinks = [
    {
      'name':'사이다',
      'type':'탄산음료',
    },
    {
      'name':'콜라',
      'type':'탄산음료',
    },
    {
      'name':'오렌지쥬스',
      'type':'생과일',
    },
  ];
  
  final soda = drinks.where((x) => x['type']=='탄산음료');
  print(soda);
}

```



## 5. reduce()

```dart
void main() {
  List<int> numbers = [1, 3, 5, 7, 9];
  
  // loop
  final result1 = numbers.reduce((prev, next){
    return prev + next;
  });

  final result2 = numbers.reduce((prev, next)=>prev+next);
  
  print(result1); // 25
}
```

loop 1 : prev = 1, next = 3

loop 2 : prev = 4, next = 5

loop 3 : prev = 9, next = 7

loop 4 : prev = 16, next = 9

*return 되는 타입이 리스트의 타입이여 한다!*



## 6. fold()

```dart
void main() {
  List<int> numbers = [1, 3, 5, 7, 9];
  
  // return 타입 제너릭으로 정해줌
  // fold<type>(시작값, (prev, next));
  final sum = numbers.fold<int>(0, (prev, next) => prev + next);
}
```



## 7. cascading operater

```dart
void main() {
  List<int> odd = [1, 3, 5, 7, 9];
  List<int> even = [2, 4, 6, 8];
  
  // cascading operator
  print([...even, ...odd]); // 새로운 리스트로 생성
}
```





## 8. map to class

```dart
void main() {
  List<Map<String, String>> drinks = [
    {
      'name': '사이다',
      'type': '탄산음료',
    },
    {
      'name': '콜라',
      'type': '탄산음료',
    },
    {
      'name': '오렌지쥬스',
      'type': '생과일',
    },
  ];

  // map to class
  final parsedDrink = drinks.map((x) => Drink(
        name: x['name']!,
        type: x['type']!,
      )).toList();
  
  print(parsedDrink);
}

class Drink {
  final String name;
  final String type;

  Drink({
    required this.name,
    required this.type,
  });
  
  @override
  String toString(){
    return 'Drink $name $type';
  }
}
```


