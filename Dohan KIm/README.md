## 플러터 스터디 TIL 3월 

###  2023년 3월 22일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/22 | dart의 기초  | dart란 무엇인가          | https://dart.dev/ |   |


 ```dart
 void main() {
    print('hello world');
 }

 ```
 * main함수 및 세미콜론 필수!

#### dart의 특성 (강의내용과는 별개)
* OOP(Object Oriented Programming)언어
  
* Interface를 가진 단일 상속되는 Class를 가진 언어
  
* isolates 기능을 통해 single-thread 언어임에도 불구하고 동시에 여러 프로세스를 동작 가능


###  2023년 3월 23일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/23 | dart의 자료형  |   ------        | https://dart.dev/ |   |


#### var
* dart에서는 변수를 var 키워드 또는 명시적 타입을 사용해 만든다.
```dart
void main(){
	var name = "nico"
}
void main(){
	String name = "nico"
}
```
*  다른 타입 변수는  서로 대입할 수 없다.
* 보통함수나 메소드 내부에 지역변수를 지정할 때는 var를 사용하고class에서 변수나 프로퍼티를 선언할 때는 명시적 타입을 사용한다.
#### dynamic
* 만약 변수를 선언할 때 아무런 값을 지정하지 않거나, 타입을 선언하지 않으면 자동적으로 dynamic 타입을 가진다.
```dart
dynamic name;
```
```dart
void main(){
	var name; // <--- dynamic 타입을 가진다.
}
```
####  Nullable
* null safety는 개발자가 null 값을 참조할 수 없게 하는 것이다.
```dart
bool isEmpty(String string) => string.length == 0;

main(){
	isEmpty(null);
}
```
* 실행시 NoSuchMethodError를 실행한다. 바로 String을 보내야 할 곳에 null을 보냈기 때문이다.
null에는 length라는 속성이 없기 때문이기도 하다.

* 이와 같은 에러는 컴파일러에서 잡을 수 있는 에러가 아니다.
이런 상황이 발생하지 않도록 null를 삭제하기에는 null 값은 유용하다.

* dart에서는 변수가 null이 될 수 있음을 명확히 표시해야한다.
```dart
void main(){
	String name = "nico";
    name = null;
}
```
* 이 코드는 에러가 난다. name이 null 값을 참조할 수 있다고 알려주지 않고 null 값을 참조하기 때문이다.
```dart
void main(){
	String? name = "jisoung";
    name = null;
    if(nico != null){
    	nico.isNotEmpty;
    }
}
```
* 이 코드는 에러가 나지 않는다. 차이점이 보이는가? 바로 ?를 사용해 이 변수에는 null이 참조될 수 있음을 알려주는 것이다. 만약 ?를 붙인 변수는 이 변수가 null인지 아닌지 확인해야 한다.


###  2023년 3월 24일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/22 |  final, const, late, list, string($)|     ------       | https://dart.dev/ |   |

### final and const
* 둘은 값을 한 번 지정하게 되면 바꿀 수 없다는 공통적인 속성을 가지고 있다.

하지만 다른점이 존재하는데 가장 큰 차이점은 생성 시점이라고 볼 수 있다.
### final
```dart
void main() {
	final name = 'nico';
	name = 'nico';
}
```
* 이미 한번 'nico'라는 값이 들어갔으므로 수정 불가 그렇기에 error 발생 

```dart
void main() {
	final name = 'nico';
}
```
* 그래서 이렇게 수정해야함. 그리고 다른점은 const의경우 선언부에서 무조건 값을 부여해주어야하지만 final은 선언 시 값을 부여하지 않고 이후 최초 1번 값을 부여해줄 수 있다.
그래서 선언부의 코드만으로는 컴파일러가 해당 변수의 값을 알 수 없기 때문에 const처럼 앱 실행 시 메모리에 넣어 관리할 수 없다.

### const
  
```dart
void main() {
    const name = ‘nico’;
    name = ‘12’;  
}
```
* 마찬가지로 수정 불가
  
```dart
Get.to(const FirstPage());
```
* 위의 코드와 같이 인스턴스를 생성하는 코드를 만났을 때 일반적인(const가 아닌) 인스턴스화 시 무조건 새로운 인스턴스를 생성한다. 하지만 const로 선언된 변수 또는 위젯의 경우 생성을 앱이 시작될 때 메모리에 같이 등록하여 해당 생성 시점에 실질적으로 새로 생성되는것이 아닌 기존에 메모리에 올라가있던 인스턴스를 매번 재사용하게 된다.
#### const의 장점
* setState 등 상태 변경에서 새로운 인스턴스를 생성하고 기존의 인스턴스는 메모리에 남게 되어 일정 시점에서 GC에 의해 지워지는데 빈번한 생성은 메모리 효율을 저하시킬 수 있다. 하지만 const를 통한 재사용 시 이러한 사용하지 않는 인스턴스가 메모리에 남게되는 메모리 낭비를 효율적으로 관리할 수 있다.
  
#### final과 const의 차이점
* final은 실행중에 값이 결정됩니다.
* final은 이 파일이 실행될 때 해당 위치에서 값이 결정됩니다.
* const는 컴파일시에 값이 결정됩니다.
* const는 이 파일을 컴파일할 때 기계어로 번역될 때 값이 결정됩니다.


#### late
* late 변수는 late 키워드를 사용하여 선언할 수 있습니다. 예를 들어, 아래와 같이 late 변수를 선언할 수 있습니다. final 혹은 var 앞에 붙여 사용합니다.
  
```dart
void main(){
  late final String name;
}
```
* late 변수는 인스턴스가 생성된 후에 값을 할당할 수 있습니다.

```dart
void main(){
  late final String name;
  name = 'nico'
}
```

```dart
void main(){
  late final name;
  name = 'nico'
  print(name);
}
```
* 'nico'출력됨.
#### late의 장점
* late 변수는 초기화를 지연하는 기능을 가지고 있어, 일부 값만 초기화하고 나머지 값은 나중에 초기화할 수 있다는 장점을 가지고 있습니다.

 

* late 변수는 클래스의 인스턴스 변수나 메소드의 매개변수에도 사용될 수 있습니다.

 

* late 변수는 final 변수와 달리 값을 할당하지 않은 상태로 인스턴스를 생성할 수 있으며, 인스턴스가 생성된 후에도 값을 변경할 수 있습니다.

 

* 하지만 late 변수는 특정 상황에서만 사용할 수 있는 기능으로, 인스턴스가 생성될 때부터 값을 할당해야 하는 경우에는 final 변수를 사용하는 것이 좋습니다.
  
#### tip
* Dart에서 late 변수는 인스턴스가 생성된 후에 값을 할당할 수 있도록 하며, 초기화를 지연하는 기능을 가지고 있지만 특정 상황에서만 사용하는 것이 좋습니다.

###  dart의 자료형
### var
* Dart는 변수를 정의할 때 var를 사용합니다. 문자열도 넣을 수 있고, 숫자를 넣을 수도 있고, 실수를 넣을 수도 있습니다.
뿐만 아니라 list(배열)를 넣을 수도 있습니다.
* 클래스 안이나 메서드 안에 위치하는게 아니라 최상단에 위치가 가능합니다.
* 1급 객체로 함수의 파라미터로 전달도 가능하며, 메모리에 떠서 로딩이 가능합니다.
  
#### var과 dynamic의 차이점
```dart
ain() {
  // var과 dynamic의 차이는?
  // 4번 라인 실행시에 10이 num에 들어갔기 때문에 타입이 고정되어 버립니다.
  var num = 10;
  num = '안녕';

  // 8번 라인 실행시에 20이 sum에 들어갔지만 타입이 고정되지 않습니다.
  dynamic sum = 20;
  sum = "안녕";
}
```
### Object
* Object를 만들 때 사용하는데 Dart에서는 Map이라고 하는 자료형입니다.
```dart
var user = {
  "id" : 1,
  "username" : "test"
};

void main() {
  
  print(user);
  // 찾을 때 키 값을 넣으면 원하는 값만 찾을 수 있습니다.
  print(user["id"]);
```
* user Object와 user의 id 값만 출력되는 것을 확인할 수 있습니다.
### bool
* bool은 true와 false 값을 가지는 자료형으로 if 조건문과 잘 맞습니다.
```dart
bool isRunning = true; 

void main(){
  print(isRunning);
}
```
### list
* 리스트는 데이터를 순차적으로 담을 수 있는 인덱싱 가능한 자료구조이다. 배열을 대체할 수 있다.
* 서브클래스로 Fixed-length list와 Growable list가 있는데, 말 그대로 Fixed-length list는 길이가 고정된 list이고, Growable list는 아이템에 따라 길이가 조정된다.
```dart
void main() {
    var numbers = [1, 2, 3, 4];
}
```
* list안에서 ,로 마무리를 하면 자동으로 다음처럼 배열된다.
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
#### 크기 고정 리스트 (fixed length list)
* 크기가 고정된 리스트는 런타임 동작 시에 길이를 바꿀 수 없다.
```dart
var my_list = new List(3);	// 크기 3짜리 리스트를 만듦
var your_list = List<int>.filled(5, 0);	// 모든 원소가 0으로 초기화된 크기 5짜리 리스트를 만듦
```
#### 가변 리스트 (growable list)
* 가변 리스트는 런타임 동작 시 길이를 바꿀 수 있다.
```dart
var my_list2 = [1, 2, 3];	// 값과 함께 리스트를 초기화함
var my_list3 = new List();	// 길이가 0인 리스트를 만듦
var my_list4 = new List.empty(growable: true);
var my_list5 = List<int>.filled(5, 0, growable: true);
```
* 사실 new List(3)처럼 숫자만 달랑 주는 게 아니라면 그 어떤 리스트 생성자라도 가변 리스트로 만들 수 있긴 하다. 바로 growable 옵션을 true로 주는 것이다. List.filled도 마찬가지다.

#### 리스트 원소 접근
* 리스트 이름 다음 대괄호를 적어주고 그 안에 접근하고 싶은 인덱스 번호를 써주면 된다. 첫 번째 원소와 마지막 원소는 특별히 first, last로 접근이 가능하다.
```dart
var my_list5 = List<int>.filled(5, 0, growable: true);
my_list5[0] = 1;
my_list5[4] = 5;
print(my_list5[2]);	// 0
print(my_list5.first);	// 1
print(my_list5.last);	// 5
```
#### 리스트 원소 삽입
* 리스트에 원소를 삽입하려면 add, addAll 등의 메소드를 이용하면 된다. 하나의 값을 리스트 맨 마지막에 추가할 때는 add, 여러 개의 값을 한 번에 추가하려면 리스트에 담아 addAll 하면 된다.
```dart
my_list5.addAll([6, 7, 8]);
my_list5.add(9);
```
* 특정 위치에 원소를 삽입하고 싶다면 insert를 쓰면 된다. insert()는 첫 번째에 인덱스, 두 번째에 삽입할 데이터를 써 준다. insertAll을 해서 한 번에 여러 데이터를 삽입할 수도 있다.
```dart
my_list5.insert(3, 3);
my_list5.insertAll(1, [1, 2]);
```
#### 리스트 원소 삭제
* 먼저 어떤 값을 지우고 싶다면, remove를 사용하면 된다. remove를 사용하면 리스트의 왼쪽부터 시작해서 처음으로 등장하는 value 값을 삭제한다. remove는 bool 타입을 반환하는데, 해당하는 값이 있었고 잘 지워졌다면 true, 그렇지 않다면 false를 반환한다. 
```dart
my_list5.remove(0);	//제일 먼저 등장하는 0 삭제
``` 
* 그 다음 n번 인덱스의 원소 값이 무엇이든 그 인덱스 값을 지우고 싶다면 removeAt을 사용하면 된다. removeAt은 지운 인덱스의 원소를 반환한다.
```dart
my_list5.removeAt(3);	// 3번 인덱스의 값을 지운다. 
// 이 때 인덱스는 0번부터 시작하므로 실질적으로 4번째 원소를 지운다는 것을 기억하자
```
* 마지막 원소를 지우고 싶다면 removeLast()를 쓸 수 있다. pop과 같은 연산이다. removeLast 역시 방금 지운 원소를 반환한다.
```dart
my_list5.removeLast();
```
* 어느 범위 사이의 원소를 삭제하고 싶을 수도 있다. 그럴 때는 removeRange를 사용할 수 있다. removeRange는 start와 end 인덱스를 받아 start, end 사이의 원소를 모두 삭제한다. 아무것도 반환하지 않는다.
```dart
my_list5.removeRange(1, 3);
// 1번부터 3번 인덱스 전까지, 즉 1번과 2번 2개의 원소를 삭제한다.
```
* 리스트의 전체 원소를 삭제하고 싶다면 clear()를 사용하면 된다. 리스트 안의 원소가 지워져 리스트는 길이가 0이 된다.
```dart
my_list5.clear();
```
#### 리스트 원소 검색
* 리스트가 어떤 원소를 갖고 있는지 확인하고 싶다면, contains 메소드를 쓸 수 있다. contains(value)를 하면 value가 들어있을 때 true, 그렇지 않을 때 false를 반환한다.
```dart
my_list5.contains(0);	//true
```
* 리스트 안에 있는 원소 중 어떤 하나라도 주어진 조건을 만족하는지 알고 싶다면 any를 쓸 수 있다. 
* 다음의 코드는 my_list5의 원소 중 5가 넘는 값이 하나라도 있는지 확인하는 문장이다. 
* 이와 같이 any 안에 bool 타입을 반환하는 함수를 써서 구현할 수 있다. every도 마찬가지다. 특이한 건 함수 안의 매개변수가 하나라도 반드시 괄호 ()로 감싸줘야 한다는 사실이다.
```dart
print(my_list5.any((x) => x > 5));
print(my_list5.every((x) => x < 6));
```
* 어떤 원소가 여러 개 있는 것 같을 때, 가장 왼쪽에 있는 값을 찾을 때는 indexOf를 쓸 수 있다. 해당 원소를 가진 제일 처음 나오는 인덱스 번호가 반환된다.
```dart
my_list5.indexOf(0);
```
* 마찬가지로 뒤에서부터 찾고 싶을 때는 lastIndexOf를 쓸 수 있다.
```dart
my_list5.lastIndexOf(0);
```
### String interpolation
* 문자열에 변수나 상수를 삽입할 수 있고, 데이터 타입에 따라 중괄호를 포함한 표현식 또한 삽입할 수 있습니다. 자바스크립트의 $ 기호와 비슷한 역할을 합니다.

```dart
void main() {
  var name = "Dart";
  print("Hello, $name");
}
```
* 위 코드는 name 변수에 "Dart"라는 값을 할당하고, print 함수를 사용해 "Hello, Dart"라는 문자열을 출력합니다. $ 문자를 사용하여 변수나 상수를 문자열 내에 삽입할 수 있습니다.
>  
* 여러 개의 변수를 사용할 수도 있습니다.
```dart
void main() {
  var firstName = "Dart";
  var lastName = "Programming";
  print("Hello, $firstName $lastName");
}
```
* 위 코드는 firstName과 lastName 변수를 문자열 내에 보간하여 "Hello, Dart Programming"라는 문자열을 출력합니다.

#### 표현식을 문자열에 삽입하는 방법
```dart
void main() {
  var a = 10;
  var b = 20;
  print("a + b = ${a + b}");
}
```
* 위 코드는 a + b 표현식을 문자열 내에 삽입하여 "a + b = 30"라는 문자열을 출력합니다. ${}를 사용하여 표현식을 문자열 내에 삽입할 수 있습니다.
