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
####dynamic
* 만약 변수를 선언할 때 아무런 값을 지정하지 않거나, 타입을 선언하지 않으면 자동적으로 dynamic 타입을 가진다.
```dart
dynamic name;
```
```dart
void main(){
	var name; // <--- dynamic 타입을 가진다.
}
```
#### Nullable
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


