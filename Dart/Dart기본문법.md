# Dart

## 1. 기본 문법

### 1) Type

```dart
// variable -> type을 오른쪽 값으로 유추, Type fix, 타입 바꿀 수 없음
var variable = 'Hello';

// var type = String
print(variable.runtimeType);

// 정수, integer
int number1 = 10;

// 실수, double
double number2 = 2.5;

// Boolean
bool isTrue = true;

// String
String name = 'Hello';
print('${name}');
print('$name');

// dynamic
dynamic name2 = 'World';
dynamic number3 = 10;
name2 = 2; // dynamic type은 타입을 바꿀 수 있음
```

### 2) Nullable, Non-nullable

* nullable: null이 될 수 있다.
  
  ```dart
  String? name1 = '안녕' // 물음표를 붙여 name1이 null값이 될 수 있음을 나타냄
  print(name1!); // 느낌표는 절대로 null이 아님을 의미
  name1 = null;
  ```

* non-nullable: null이 될 수 없다.
  
  물음표를 붙이지 않은 모든 타입들을 null 값을 가질 수 없다.

### 3) final, const

```dart
// 변수 값 변경 불가능, 타입 생략 가능
final name1 = '안녕';
const name2 = 'Hello';

// 코드가 실행 되는 순간의 시간
final DateTime now1 = DateTime.now(); 
// const는 빌드타임의 값을 알고 있어야하므로 에러발생
const DateTime now2 = DateTime.now(); 
```

### 4) Operator

1. 산술 연산자 +, - , /, *, %...

```dart
double? number = 4.0;
number = null;

number ??= 3.0; // number가 null이면 선언된 숫자로 바꿔라
```

2. 비교 연산자 < > <= => == !=...

3. 타입 비교

```dart
int number =1;
print(number is int); // true
print(number is String); // false
print(number !is int); // false
print(number !is String); // true
```

4. 논리 연산자 &&, || ...

# 

## 2. 타입

1. **List**

```dart
List<int> numbers = [1, 2, 3, 4, 5, 6]; 

print(numbers[0]); // index 사용
print(numbers.length); // list 길이 6
numbers.add(7);
numbers.remove(7);
print(numbers.indexOf(2)); // 1
```

2. **Map**

```dart
Map<String, bool> isHarryPotter = {
    'Harry Potter': true,
    'Ron Weasley': true,
    'Ironman' : false,
}

// 값 추가
isHarryPotter.addAll({
    'Hermione Granger':true,
    'Spiderman' : false,
});
isHarryPotter['Hulk'] = false;

// 값 변경
isHarryPotter['Spiderman'] = true;
print(isHarryPotter['Ironman']); // false

// 값 제거
isHarryPotter.remove('Harry Potter');


print(isHarryPotter.keys); // key만
print(istHarryPotter.values); // value만
```

3. **Set**

```dart
final Set<String> names = {
    'flutter',
    'flutter', // 자동으로 중복 제거
    'Hello',
    'World',
};

names.add('Hi');
names.remove('Hello');
print(names.contains('flutter')); // true
```

## 3. 조건문

1. If문

```dart
if(number % 3 == 0){
    ...
}else if(number % 3 == 1){
    ...
}else{

}
```

2. Switch-case

```dart
switch(number % 3){
    case 0:
        break;
    case 1:
        break;
    default:
}
```

## 4. Loop

1. for-loop

```dart
for(int i=0; i<10; i++){
    ...
    if(i==5){
        continue;
    }
}

for(int n in numbers){
    ...
}
```

2. while loop

```dart
while(total < 10){
    ...
    if(..){
        break;
    }
}

do{
    ...
}while(total < 10);
```

## 5. Enum

```dart
enum Status{
    approved,
    pending,
    rejected,
}

void main(){
    Status status = Status.pending;
}
```

왜 enum 타입? 정확히 enum 안 타입만 존재한다는 것을 알려주기 위해서 (타입 강제)

## 6. 함수

```dart
void main(){
    addNumbers1(10, 20, 30);
    addNumbers2(10);
    int result1 = addNumbers3(x: 10, y: 20);
    int result2 = addNumbers4(10, y:20);
}

// 세 개의 숫자(x, y, z)를 더하고 짝수인지 홀수인지 알려주는 함수
// positional parameter: 순서가 중요한 파라미터
addNumbers1(int x, int y, int z){
    int sum = x + y + z;
}

// optional parameter: 있어도 되고 없어도 되는 파라미터
addNumbers2(int x,[int y = 20, int z = 30]){
    int sum = x + y + z;
}

// named parameter: 이름이 있는 파라미터 (순서가 중요하지 않음)
int addNumbers3({
    required int x,
    required int y,
    int z = 30, // required 없으면 optional
}){
    int sum = x + y + z;
    return sum;
}

// arrow function
int addNumbers4(int x,{
    required int y,
    int z = 30,
}) => x + y + z;
```

## 7. Typedef

```dart
void main(){
    int result1 = calculate(10, 20, 30, add); // 60
    int result2 = calculate(10, 20, 30, subtract); // -40
}

typedef Operation = int Function(int x, int y, int z);

// return 타입과 파라미터가 모두 일치하는 함수 생성
// 더하기
int add(int x, int y, int z) => x + y + z;
// 빼기
int subtract(int x, int y, int z) => x - y - z;

int calculate(int x, int y, int z, Operation operation){
    opeartion(x, y, z);
}
```
