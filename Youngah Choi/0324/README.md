## 플러터 스터디 TIL 3월 

###  2023년 3월 24일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/24 | final, late, const  | Dart 자료형, const, final, late 수식어  | https://dartpad.dev |


### final
```dart
void main() {
    String name = ‘nico’;
}
```
* **final** : 값을 재할당하지 못하는 변수를 만들어준다. 한 번 정의된 변수를 수정할 수 없게 만들려면 final로 선언한다. 딱 한 번만 할당할 수 있다.

<br>

```dart
void main() {
    final name = ‘nico’;
    name = ‘nico’;  // final을 사용하면 수정할 수 없기에 에러
}
```

* 더 구체적으로 사용하는 방법 :`final String name = ‘nico’;`
 컴파일러는 알아서 타입을 추론하기에  `final name = ‘nico’;`만 입력해도 된다. 

<br>

### late 수식어
* **late** : final이나 var 앞에 붙일 수 있는 수식어
* 초기 데이터 없이 변수를 선언할 수 있게 해준다. 즉, 변수를 만드는데 데이터가 없는 것이다. 그 이후 API 요청으로 데이터를 받은 다음 그 데이터를 나중에 변수에 넣는 방식이다. 
* 아직 정의되지 않은 late 변수에는 접근할 수 없다.

```dart
void main() {
    late final String name;  // 정확하게 하려면 late final에 String을 붙인다.
    name = ‘nico’;
}
```
* 데이터 없이 변수를 만들어주고 API에서 데이터를 받아 변수에 넣어준다.

#### late 수식어 장점
```dart
void main() {
    late final String name;
    // do something, go to api
    print(name);
}
```
1. 실수를 막아준다. `print(name);`을 할 때 name이 late 변수이기에 `name = ‘nico’;`를 하지 않은 상태일 때는 값을 넣기 전에는 접근하지 않아야 한다고 알려준다. name 안에 아무것도 없기에 접근할 수 없다. 

2. name 안에 어떤 데이터를 넣어야만 사용할 수 있다. flutter로 data fetching을 할 때 유용하다.

3. API에서 얻어온 값을 사용해야 할 때 한 번만 할당할 수 있는 변수를 먼저 만들고 데이터는 나중에 넣어줄 수 있다. 

4. flutter로 API에서 데이터 가져오는 일을 할 때 합리적이다. 정의하려는 것이 있는데 데이터는 아직 없는 경우에 데이터는 나중에 넣고 그 이후 그 변수를 사용한다.
```dart
void main() {
    late final String name;
    name = ‘nico’;
    print(name);
}
```
* 순서 : API에 요청 - API에서 값 전달 - late 변수에 넣기

<br>

### const
* **const** : 컴파일할 때 값을 알고 있는 변수를 만드는 방법으로, 컴파일할 때 알고 있는 값에 사용한다. 그 예로 *max_allowed_price* 등 앱스토어에 앱을 올리기 전에 알고 있는 값에 사용한다.

* **Dart에서 const** : compile-time constant를 생성

* **Javascript, typescript에서 const** : Dart의 final과 비슷하다.

```dart
void main() {
    const name = ‘nico’;
    name = ‘12’;  // 수정될 수 없다. 
}
```
* compile-time constant : const는  compile-time에 알고 있는 값이어야 한다.

```dart
void main() {
    const API = ‘1122’;  // 수정될 수 없고 컴파일 될 때 그 값을 알고 있다. 하드 코딩된 것으로 코드 안에 있는 것이고 복사 붙여넣기가 된 것이다. 
}
```
`const API = fetchApi();`로 수정, 이는 compile-time constant가 아니다. API에서 받아와야 하는 값이기 때문에 컴파일러는 API 변수의 값을 모른다. 따라서 const가 아니라 final로 바꿔야 한다. 

<br>

#### const와 final의 차이점
* **final** : 런타임 중에 만들어질 수 있다. 즉, 사용자가 앱을 실행하면서 변수를 만들 수 있다. 
* **const** : 컴파일 하기 전에 const의 값을 알고 있어야 한다. 

<br>

### 복습
* **final/var** : 어떤 값인지 모르고, 그 값이 API로부터 오거나 사용자가 화면에서 입력해야 하는 값에 사용
* **null safety** : 잘못된 상태의 변수를 참조하는 것을 막아준다.

<br>

### Dart의 자료형
* Dart의 거의 전부가 object로 이루어져 있고 function도 object이다. 이것이 Dart가 객체 지향 언어로 불리는 이유이다.
* 자료형 - 우클릭 - Go to type definition : int와 double에 우클릭한 경우에는 num이라는 클래스에서 파생한 것임을 확인할 수 있다.
* **num** : int형과 double형 모두 될 수 있는 경우에 사용

<br>

### List
```dart
void main() {
    var numbers = [1, 2, 3, 4];
}
```
* `var numbers = [1, 2, 3, 4];`에서 ,로 리스트의 끝을 마무리하면 자동으로 다음처럼 된다.
```dart
void main() {
    var numbers = [
        1,
        2,
        3,
        4,
    ];
}
```
* `var numbers = [1, 2, 3, 4];`에 마우스를 대면 `List<int> numbers`라고 적힌 것을 확인할 수 있다. `var numbers = [1, 2, 3, 4];` 또는 `List<int> numbers =  [1, 2, 3, 4];`로 코드를 작성해도 똑같이 동작한다.
* `numbers.first` : list의 첫 번째 요소를 가져다준다.
* `numbers.last` : list의 마지막 요소를 가져다준다. 마지막 요소를 가져와야 하는데 요소가 몇 개인지 모를 때 last로 얻어올 수 있다.

#### Dart에서 List
* collection if와 collection for를 지원한다. 
* **collection if** : if로 존재할 수도 안할 수도 있는 요소를 가지고 만들 수 있다.
```dart
void main() {
    var giveMeFive = true;
    var numbers = [1, 2, 3, 4,];
    if(giveMeFive) {
        numbers.add(5);
    }
}
```
위의 코드를 collection if를 사용하면 더 간단하게 가능하다.
```dart
void main() {
    var giveMeFive = true;
    var numbers = [1, 2, 3, 4, if(giveMeFive) 5,];
    print(numbers);
}
```
> 출력 : [1, 2, 3, 4, 5] 

<br>

### String interpolation
* **String interpolation** : text에 변수를 추가하는 방법
```dart
void main() {
    var name = ‘yeonga’;
    var greeting = ‘Hello everyone, my name is $name, nice to meet you’;
    print(greeting);
}
```
> 출력 : Hello everyone, my name is yeonga, nice to meet you 

* 달러 기호 뒤에는 반드시 변수를 사용한다. 따옴표는 큰따옴표와 작은따옴표 모두 관계없다.
* 변수가 이미 존재할 때 사용하는 방식이다.
```dart
void main() {
    var name = ‘yeonga’;
    var age = 20;
    var greeting = ‘Hello everyone, my name is $name, I\’m ${age + 2}’;
    // I’m을 사용하게 되면 ‘의 수가 맞지 않아 오류가 나기에 escape 기호를 사용해준다.
    print(greeting);
}
```
> 출력 : Hello everyone, my name is yeonga, I’m 22 

* 단순히 변수 값을 담는 경우 : $ 뒤에 변수 이름 작성
* 계산을 실행하는 경우 : $ 뒤에 중괄호 {} 사이에 계산할 내용을 작성하면 Dart가 이를 계산하여 그 결괏값을 text로 치환한다.