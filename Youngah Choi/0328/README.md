## 플러터 스터디 TIL 3월 

###  2023년 3월 28일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/28 | Function, Parameters  | Function, Named Parameters, Optional Position Parameters, QQ Operator  |  |   


### Defining a Function
```dart
void sayHello(String name) {
	print("hello $name nice to meet you");
}
```
* void : 이 함수가 아무것도 return하지 않는다는 의미, 부가적인 효과만 있고 아무것도 return하지 않는다. 

* 만약 무언가 return하는 경우에는 print 대신 return을 적고 자료형도 String으로 바꿔준다. 

```dart
String sayHello(String name) {
	return "hello $name nice to meet you";
}
```
* sayHello()는 하나의 parameter를 가지는 함수이고, 그 parameter의 이름은 name이다. String을 return한다. 

* 실행되고 곧바로 return하는 function을 가질 때는 return을 지울 수 있다. 함수의 중괄호도 삭제 가능하다. 그리고 한 줄짜리 코드일 때 fat arrow syntax를 사용할 수 있다. 

* **fat arrow syntax** : 곧바로 return을 하는 것과 같은 의미

```dart
String sayHello(String name) => "hello $name nice to meet you";
```

* fat arrow syntax의 예시

```dart
num plus(num a, num b) => a + b;
```

중괄호나 return이 필요 없고, argument를 받아서 곧바로 결괏값을 return한다. 

### Named Parameters

* Dart의 function : Named Parameters라는 것을 지원한다. 

```dart
String sayHello(String name, int age, String country) {
	return "Hello &name, you are &age, and you come from &country";
}

void main() {
	print(sayHello('nico', 20, 'cuba')); 
}
```

age를 num이 아닌 int로 자료형을 사용한 이유는 num이 int도 받지만 double도 받기에 나이는 double이 아닌 int여야 하기 때문이다. 

* Named Parameters 사용

```dart
String sayHello({String name, int age, String country}) {
	return "Hello &name, you are &age, and you come from &country";
}

void main() {
	print(sayHello(
		age: 20, 
		country:'cuba',
		name: 'nico',
	));
}
```

* 파라미터가 NULL일 수도 있는데, Dart에서는 null safety를 사용하므로, 이를 해결하는 방법 첫 번째로 파라미터의 default value를 지정해준다. 이렇게 하면 null safety에 걸리지 않는다. 

* 전달해야 되는 요소들의 위치를 기억하는 대신에 함수의 정의를 보고 그대로 적어준다. 작성할 때는 순서와 관계 없이 자료형만 지켜주면  함수 호출을 할 수 있다. 

* 두 번째 방법은 **required modifier**를 사용한다. named parameter가 required라고 명시해주는 것이다. 

* required modifier를 사용해서 필수 값으로 만들 수 있다. 이를 사용하면 Dart가 이 코드를 컴파일하지 않는다. 그 이유는 Dart가 이 function은 반드시 named parameter와 함께 호출되어야 하는 것을 알기 때문이다. 사용자가 로그인할 때 이메일, 비밀번호 값에 사용할 수 있다.
```dart
String sayHello({
	required String name, 
	required int age, 
	required String country, 
}) {
	return "Hello &name, you are &age, and you come from &country";
}

void main() {
	sayHello(
		age: 12,
		country: 'cuba',
		name: 'nico');
}
```

#### parameter의 종류

1. positional : parameter의 순서가 중요하다. 따라서 사용할 때 각각의 위치를 기억해야 한다. 
2. named : 순서는 상관없고 name이 중요하다. 파라미터 리스트 전체를 중괄호로 감싸고 ,를 붙여준다. 

### Optional Positional Parameters

* Positional Parameters : 순서에 맞춰서 입력해야 한다. Positional Parameters는 required이기에 Optional Positional Parameters은 optional로 바꾸는 방법을 사용한다.
```dart
String sayHello(String name, int age, [String? country],) => 'Hello $name, you are $age years old from $country';  // country는 not required, default value 부여, 마지막 argument 보내지 않고도 sayHello 호출 가능 
void main() {
	sayHello('nico', 12);  
}
```
* name, age, country : required

* **Optional Positional Parameters** : 대괄호로 감싸주고 country가 null이 될 수 있다고 표시한다. 그리고 default value를 부여한다. 
```dart
String sayHello(String name, int age, [String? country],) => 'Hello $name, you are $age years old from $country';
void main() {
	var results = sayHello('nico', 12);  
	print(results);
}
```
결과 `Hello nico, you are 12 years old from cuba`

<br>

### QQ operator
* QQ operator : 물음표 2개
* 이름을 대문자로 return하는 함수 만들기
```dart
String capitalizeName(String name) => name.toUpperCase();

void main(){
	capitalizeName('nico'); 
}
```
* 사용자가 null도 입력할 수 있도록 String 뒤에 ?를 추가하면 Dart한테 name값이 null일 수도, 아닐 수도 있다고 하는 것이다. 
```dart
String capitalizeName(String name) {
	if(name != null) {
		return name.toUpperCase();
	}
	return 'ANON';
}

void main(){
	capitalizeName('nico'); 
	capitalizeName(null); 
}
```
* fat arrow syntax를 사용하여 더 간단하게 만들면 다음과 같다. 
```dart
String capitalizeName(String name) => name != null ? name.toUpperCase() : 'ANON';

void main(){
	capitalizeName('nico'); 
	capitalizeName(null); 
}
```
* name이 null이 아니면 name.toUpperCase()를 return, null이면 ANON을 return한다. 


#### QQ operator
* **QQ operator** : 좌항과 우항이 있고 qq가 체크하는데 좌항이 null이면 우항을 return한다. 좌항이 null이 아니면 좌항을 return한다. 
* question question operator를 사용하여 위의 코드를 더 간단하게 작성하면 다음과 같다. 
```dart
String capitalizeName(String name) => name?.toUpperCase() ?? 'ANON';

void main(){
	capitalizeName('nico'); 
	capitalizeName(null); 
}
```

* QQ equals / QQ assignment operator 
```dart
void main(){
	String? name;
	name ??= 'nico';  // name이 null이라면 값을 할당하라는 의미이다. 
	name = null;
	name ??= 'another';
	print(name);
}
```
결과 `another`
* `name = null;`, `name ??= 'another';`를 사용하지 않는 경우에는 `nico`가 결과로 출력된다. 
