# DateTime, Duration

## DateTime

```dart
Datetime now = DateTime.now();

print(now);
print(now.year);
print(now.month);
print(now.day);
print(now.hour);
print(now.minute);
print(now.second);
print(now.millisecond);


// 2017년 11년 23일
Datetime specificDays = DateTime(
    2017,
    11,
    23,
)
```

* difference(Datetime d) - 기간 차이

* add(Duration d) - 기간 더하기

* ifAfter, isBefore - 이전/이후 비교

## Duration

```dart
Duration duration = Duration(seconds: 60);
print(duration); // 0:01:00.0000 (시:분:초)
print(duration.inDays); // 0
print(duration.inHours); // 0
print(duration.inMinutes); // 1
print(duration.inSeconds); // 60
print(duration.inMilliseconds) // 60000
```
