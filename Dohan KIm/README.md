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

###  2023년 3월 27일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/27 | maps,sets  | ------         | https://dart.dev/ |   |



* List : 데이터의 순서가 있고 중복을 허용함(배열, Array)
* Set : 데이터의 순서가 없고 중복을 허용하지 않음
* Map : 키(Key)와 값(Value)로 구성된 클래스로서 키는 중복을 허용하지 않고 값은 중복을 허용함

### Map
#### map이란 js에 object, python에 dictionary와 같다.
```dart
void main(){
	var player = {
    	"name":"jisoung",
        "age": 17,
        "isLoveFlutter": true,
   };
}
```
* 다음과 같은 코드가 있을 때 우리는 var로 선언한 변수의 타입을 지정해야 한다.
그러면 어떻게 타입을 지정해 줄 수 있을까? Map을 사용하면 손쉽게 지정해 줄 수 있다.

```dart
void main(){ 
	Map<string, dynamic> player = {
    	"name":"jisoung",
        "age": 17,
        "isLoveFlutter": true,
   };
}
```
* Map안에 List를 넣어줄 수도 있다.
```dart
void main(){
	Map<List<int>, bool> player = {
    	[1,2,3,4,5]: true,
        [6,7,8,9,10]: false,
   };
}
```
### sets
#### sets란 List와 비슷한 개념이지만 한가지 차이가 있다.
바로 모든 아이템은 유니크하다는 것이다.
```dart
void main(){
	Set<int> setNumbers = {1,2,3,4,5};
   	List<int> listNumbers = [1,2,3,4,5];
	setNumbers.add(1);
    listNumbers.add(1);
    print(setNumbers);
    print(listNumbers);
}
```
* 결과는 다음과 같다.
```dart
{1, 2, 3, 4, 5}
[1, 2, 3, 4, 5, 1]
```
* dart에서 List는 python의 List와 같고
dart에 Set은 python의 tuple과 비슷하다.
### Collection For
* dart의 유용한 기능중 하나다.
전에 Collection If와 같이 배열안에 For문을 넣을 수 있는 기능이다.
대표적으로 UI를 만들 때 유용하게 사용된다.
예제를 보자.
```dart
void main(){
	var persons = ['chanhong', 'hyeonseok', 'jisoung'];
    var newPerson = [
    	'person: nico',
        'person: lynn',
        for(var person in persons) "person: $person"
    ];
    print(newPerson);
}
```
* 결과는 다음과 같다.
```dart
[person: nico, person: lynn, person: chanhong, person: hyeonseok, person: jisoung]
```

###  2023년 3월 28일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/27 |  naemd, optional,QQ | ------         | https://dart.dev/ |   |

### Define Function
```dart
첫 번째 케이스
(반환 자료형) 함수이름(파라미터){}

두 번째 케이스
(반환 자료형) 함수이름(파라미터) => {}
```
```dart
// 첫 번째 케이스
String sayHello(String name) {
	return "Hello $name";
}

void main(){
	print(sayHello("nico"));
}
```
```dart
// 두 번째 케이스
String sayHello(String name) => return "Hello $name";

void main(){
	print(sayHello("nico"));
}
```
### Named Parameters
```dart
String sayHello(String name, int age, String country) => return "Hello $name, age: $age, country $country";

void main(){
	print(sayHello("nico", 17, "korea"));
}
```
* 위 코em는 문제가 있다. 저 17이 무슨 의미를 하는지 korea가 무슨 의미를 하는지 알 수가 없다.
이 문제를 해결하기 위해 dart에서는 named parameters를 지원한다.
```dart
String sayHello({
	String name, 
    int age, 
    String country
}) => return "Hello $name, age: $age, country $country";

void main(){
	print(sayHello{
    	name: "nico",
        age: 17,
        country: "korea",
    });
}
```
* required을 사용하면 null safety를 적용할 수 있다.(required를 쓰면 값이 반드시 있어야 한다.)
```dart
String sayHello(
	required String name, 
    required int age, 
    required String country
) => return "Hello $name, age: $age, country $country";

void main(){
	print(sayHello{
    	name: "",nico
        age: 17,
        country: "korea",
     });
}
```
### optional positional parameter
* 파라미터에 optional을 설정하려면 ?을 타입 뒤에 붙이면 된다.
* 인자를 보내지 않아도 기본 값을 가지게 하려면 다음과 같이 하면 된다.
```dart
String sayHello(
	String name, 
    int age, 
    // default value
    [String? country = "korea"],
) => return "Hello $name, age: $age, country $country";

void main(){
	print(sayHello){
    	name: "nico",
        age: 17,
        country: "korea",
    };
}
```
### QQ Operator
#### QQ question operator
```dart
String upperName(String name) => name.toUpperCase();

void main(){
	upperName('nico');
    upperName(null); // Error!
}
```
* 위 코드는 인자 값이 null 인것을 허용하지 않는다.
다음과 같이 고칠 수 있다.
```dart
String upperName(String? name){
	if(name != null){
    	return name.toUpperCase();
    }
    return 'NONE';
}
```
* 위 코드를 더 짧게 만들 수 있다.
```dart
String upperName(String? name) => name != null name.toUpperCase() : "NONE";
```
* 하지만 dart에서는 위와 같은 코드를 더욱 짧게 할 수 있다
```dart
String upperName(String? name) => name?.toUpperCase() ?? "NONE";
```
* ??(QQ)의 뜻은 만약 왼쪽의 있는 값이 Null이라면 오른쪽 값을 return 시킨다는 것이다.
쉽게 말해서 위 코드를 보면 name.toUpperCase()를 리턴할 것이다.
그런데 만약 name이 null이여서 toUpperCase()를 실행할 수 없다면 "NONE"을 리턴하는 것이다.
name에 ?(optional)을 붙인 이유는 name이 null일 수도 있기 때문이다.
### QQ equal
```dart
void main(){
	String? name;
    // 만약 name이 null인 경우 할당한다.
    name ??= 'nico';
}
```
* QQ Operator는 flutter에서 자주 사용된다.

###  2023년 3월 29일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/22 |   | -------          | https://dart.dev/ |   |

* typedef를 이용하면 자료형을 간편하게 작성할 수 있다.
다음과 같은 코드를 typedef를 사용해서 간편하게 작성해 볼 것이다.

### Typedef
```dart
// 전
List<int> reverseListOfNumbers(List<int> list) {
	var reversed = list.reversed;
    return reversed.toList();
}
```
```dart
// 후
typedef ListOfInts = List<int>;

ListOfInts reverseListOfNumbers(ListOfInts list) {
	var reversed = list.reversed;
    return reversed.toList();
}
```
### class
* dart에서 property를 선언할 때는 타입을 사용해서 정의한다.
```dart
class Player {
	final String name = 'nico';
	final int age = 17;
	void sayName(){
		// class method안에서는 this를 쓰지 않는 것을 권장한다.
		print("Hi my name is $name")
	}
}

void main(){
	// new를 꼭 붙이지 않아도 된다.
	var player =Player();
}
```
### Constructors
* dart에서 생성자(constructor) 함수는 클래스 이름과 같아야 한다.
```dart
class Player {
	// 이럴 때 late를 사용한다.
	late final String name;
	late final int age;
	// 클래스 이름과 같아야한다!
	Player(String name){
		this.name = name;
	}
}

void main(){
	// Player 클래스의 인스턴스 생성!
	var player = Player("nico", 1500);
}
```
* 위의 생성자 함수는 다음과 같이 줄일 수 있다.
```dart
// 생략
Player(this.name, this.age);
```
* 첫 번째 인자는 this.name으로 두 번째 인자는 this.age로 갈 것이다.
### Constructors Parameters
* 클래스가 거대해질 경우 위와 같이 생성자 함수를 만드는 것은 비효율적일 것이다.
```dart
class Team {
	final String name;
	int age;
	String description;
	
	Team(this.name, this.age, this.description);
}

void main(){
	// 너무 많은 인자를 받아야 해서 햇갈린다.
	// 각 인자의 의미를 알 수가 없다.
	var myTeam = Team("nico", 17, "Happy coding is end coding");
}
  ```
  * 이 문제를 해결할려면 너무 간단하다.
첫 번째는 중괄호({})를 이용하는 것이다.
```dart
class Team {
	final String name;
	int age;
	String description;
	
	Team({this.name, this.age, this.description});
}

void main(){
	// 한 눈에 볼 수 있다.
	var player = Player(
		name: "nico",
		age: 17,
		description: "Happy coding is end coding"
	)}
}
```
* 두 번째는 name parameter를 사용하는 것이다.
```dart
// 생략
Player(name:"nico", age: 17, description: "Happy coding is end coding");
```
* 하지만 여기에는 큰 문제가 있다.
변수가 null일 수도 있기 때문에 우리는 이걸 required를 이용하거나 기본 값을 줘서 처리해 줘야한다. 우리는 required를 사용할 것이다.
```dart
// 생략
Team({
	required this.name,
	required this.age,
	required this.description,
});,
```
### Named constructor
* 만약 생성자(constructor) 함수를 여러개를 만들고 싶을때
```dart
// 생략
Player.createBluePlayer({
	required String name,
	required int age,
})	: 	this.age = age,
		this.name = name,
		this.team = 'blue',
		this.xp = 0;
 ```
* 콜론(:)을 사용하면 특별한 생성자 함수를 만들 수 있다.
* 콜론을 넣음으로써 dart에게 여기서 객체를 초기화하라고 명령할 수 있다.
기존 생성자 코드와 비교해보자
```dart
// 첫 번째 case
class Player {
  late final String name;
  Player({
  	required this.name
  });
}

void main(){
  var player = Player(
    name: "jisoung",
  );
}
```
```dart
// 두 번째 case
Player({this.name, this.age, this.description});
```
```dart
// 세 번째 case
class Player {
  final String name;
  Player.createUser({
    required this.name
    }): this.name = name;
}

void main(){
  var player = Player.createUser(
    name: "jisoung",
  );
}
```
###  2023년 3월 30일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 2023/3/22 |   | -------          | https://dart.dev/ |   |
### Cascade Notation
```dart
//생략
void main(){
	var jisoung = Player(name: "jisoung", age: 17, description: "Happy code is end coding");
	jisoung.name = "nico";
	jisoung = 20;
	jisoung.description = "Best Project is End Project";
}		
```
* 위를 보면 반복되는 부분이 있다. dart에서는 이걸 간단하게 ..으로 해결할 수 있다.
```dart
//생략
void main(){
	var jisoung = Player(name: "jisoung", age: 17, description: "Happy code is end coding");
	...name = "nico"
	..age = 20
	..description = "Best Project is End Project";
}		
```
* 각 '..'들은 jisoung을 가리킨다. 매우 유용한 operator이다.
앞에 class가 있다면 그 클래스를 가리킨다.
### enums
* enum은 우리가 실수하지 않도록 도와주는 타입이다.
* dart에서 enum type을 만드는 법은 다음과 같다.
```dart
enum Team {
	red,
	blue,
}
class Player {
	String name;
	int age;
	Team team;
	
	Player({
		required this.name,
		required this.age,
		required this.team,
	});
}

void main(){
	var jisoung = Player(name: "jisoung", age: 17, team: Team.red);
	var sushi = jisoung
		..name = "sushi"
		..age = 12
		..team = Team.blue;
}
```
### Abstract(추상화)
* 추상화 클래스는 다른 클래스들이 직접 구현 해야하는 메소드들을 모아놓은 일종의 청사진이라 보면 된다.
* 추상 클래스에서는 기능을 구현하지 않는다.
```dart
abstract class Human {
	void walk();
}
```
* extends를 이용해 상속, 확장을 할 수 있다.
```dart
abstract class Human {
	void walk();
}
class Player extends Human {
	// 생략
	void walk(){
		print("working!");
	}
}
```