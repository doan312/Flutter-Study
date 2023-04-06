## 플러터 스터디 TIL 4월 

###  2023년 4월 4일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 04/04 | Flutter 설정  | Flutter 환경 설정  |  |   

* Flutter - Visual Studio Code에서 디버깅 환경을 제공해준다.
* `cmd - flutter create toonflix - cd toonflix - code .` 입력

### Widget
```dart
import 'package:flutter/material.dart';

void main() {
    runApp(const MyApp());  
}
```
* runApp() 함수는 void 함수이므로 아무것도 return하지 않는다. 하나의 argument를 필요로 하는데, 그것이 Widget이라는 타입이다.
* flutter에서 Widget - 레고 블럭이라고 생각할 수 있다. flutter의 모든 것은 widget이기 때문이다. 존재하는 위젯을 모두 사용하진 않기 때문에 모두 외울 필요는 없다. 

* text가 가운데 위치해 있다는 말은 이 text가 Center라고 불리는 다른 Widget 안에 있다는 의미이다.

* 프로그래밍 언어 관점에서 Widget - Widget을 만든다는 것은 class를 만드는 것이다.
```dart
import 'package:flutter/material.dart';

void main() {
    runApp(MyApp());  // root
}

class App extends StatelessWidget
{
    @override  // 부모 클래스의 method를 override한다는 의미
    Widget build(BuildContext context) {
        // TODO: implement build
        throw UnimplementedError();
    }
}
```
* App이라는 이름의 class를 Widget으로 만들기 위해서는 flutter SDK에 있는 3개의 core Widget 중에 하나를 상속(extend)받아야 한다. 
* StatelessWidget를 상속받으려면 build라는 method를 구현해야 한다.
* 모든 Widget은 build method를 구현해야 한다는 계약을 맺는다.

#### build method
* build method - Widget의 UI를 만드는 것이다. flutter가 실행하고 build method가 return하는 것을 화면에서 보여준다. 
* build method - BuilldContext type의 context라는 parameter를 받아온다. Widget을 return한다.
* App Widget - 앱의 root, 시작점이다. 모든 화면과 버튼 등이 App Widget으로부터 온다.
* root Widget - 다음 둘 중에 하나를 return해야 한다. materialApp(구글)이라는 Widget을 return하거나 cupertinoApp(ios)이라는 Widget을 return해야 한다. flutter는 구글이 만들어서 materialApp 스타일이 훨씬 보기 좋다.
* 나만의 앱을 만들려고 해도 기본 UI 설정과 같은 재료를 선택해줘야 하기 때문에 materialApp과 cupertinoApp 중 하나를 꼭 선택해야 한다.
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {
  @override // 부모 클래스의 method를 override한다는 의미
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Text('Hello World!'),
    );
  }
}
```
* 검은 화면만 출력된다. 화면이 scaffold라는 것을 가져야 한다. 

#### scaffold
* scaffold는 화면의 구조를 제공해준다. 
* 모바일 앱의 모든 화면은 scaffold가 필요하다.
* scaffold는 navigation bar를 구현할 수 있게 해주고 bottom tab bar, 상단 버튼, 화면 중앙 정렬 등을 해준다.
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {
  @override // 부모 클래스의 method를 override한다는 의미
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(body: Text('Hello World!'),
      ),
    );
  }
}

```
* ,를 붙여주면 포맷팅을 해준다.
* 왼쪽 위에 출력이 되지만 살짝 잘려서 보인다.
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {
  @override // 부모 클래스의 method를 override한다는 의미
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello flutter!'),
        ),
        body: Text('Hello World!'),
      ),
    );
  }
}
```
* 왼쪽 상단에 `Hello flutter!`와 `Hello World!`가 출력된다.

* 가운데로 텍스트를 배치하면 다음과 같다. Center Widget은 child를 가지고 있고, child가 Text로 된다.
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(App());
}

class App extends StatelessWidget {
  @override // 부모 클래스의 method를 override한다는 의미
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello flutter!'),
        ),
        body: Center(
          child: Text('Hello World!'),
        ),
      ),
    );
  }
}
```
* Widget을 사용할 때마다 class를 인스턴스화하고 있는 것이다.
* Text class는 화면에 보여주고 싶은 텍스트를 필요로 한다. 그것만 required고 나머지는 required가 아니다.

```dart
class Player {
    String? name;

    Player({required this.name})
}
```
* ?을 추가하면 Player가 name을 가질 수도, 가지지 않을 수도 있다는 것을 의미한다. 따라서 아무 파라미터 없이도 Player를 만들 수 있다.