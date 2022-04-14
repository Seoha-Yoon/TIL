# Web View

## Web View

* **pub.dev**: flutter open source platform
  
  * pubspec.yaml 파일에 추가
  
  ```yaml
  dependencies:
    flutter:
      sdk: flutter
    cupertino_icons: ^1.0.2
    webview_flutter: ^3.0.2
  ```

* package 불러와서 사용하면 됨

*screen/main_screen.dart*

```dart
class HomeScreen extends StatelessWidget {
  const HomeScreen({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        body: WebView(
      initialUrl: '원하는 url',
      // 자바 스크립트 사용 가능하게 - default는 사용 못함
      javascriptMode: JavascriptMode.unrestricted,
    ));
  }
}
```

* **Controller**

: Controller를 사용해서 위젯이 웹뷰를 제어할 수 있도록 할 수 있음.

```dart
body: WebView(
          // controller 주입
          onWebViewCreated: (WebViewController controller) {
            this.controller = controller;
          },
          initialUrl: homeUrl,
          javascriptMode: JavascriptMode.unrestricted,
        ));
```

## App bar

Scafford에 app_bar 위젯만 추가하면 만들 수 있음

```dart
appBar: AppBar(
          title: Text('Blog'),
          centerTitle: true,
          backgroundColor: Colors.orange,
        ),
```

이 때, android와 ios의 title default 위치가 다르므로 위치를 강제해주는게 좋다.

* actions: Appbar에 위젯들을 추가할 수 있음

```dart
actions: [
            IconButton(
                onPressed: () {
                  // 눌렀을 때 실행되는 함
                },
                icon: Icon(
                  Icons.home,
                ))
          ],
```

## Http 설정

* ios

```plist
<dict>
    <key>NSAllowsLocalNetworking</key>
    <true/>
    <key>NSAllowsArbitraryLoadsWebContent</key>
    <true/>
</dict>
```

* android

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.ex">        
    <uses-permission android:name="android.permission.INTERNET"/>

   <application
        android:label="web_view"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher"
        android:usesCleartextTraffic = "true">
```


