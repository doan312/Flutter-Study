## 플러터 스터디 TIL 3월 

###  2023년 3월 29일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/29 | class, constructors  | class, constructors, named constructor parameters  |  |   


### Typedef
* **typedef** : 자료형이 헷갈릴 때 도움이 될 alias를 만드는 방법, Map, Set처럼 *간단한 데이터의 alias를 만들 때 사용한다.* 
* List를 반대로 뒤집어 return하는 함수
```dart
typedef ListOfInts = List<int>;  
ListOfInts reverseListOfNumbers(ListOfInts list) {  // List<int> 대신 ListOfInts 사용 가능
	var reversed = list.reversed;
	return reversed.toList();
}
void main() {
	print(reverseListOfNumbers([1, 2, 3]));
}
```
결과 `[3, 2, 1]`
* 구조화된 data의 형태를 지정하고 싶다면 class를 만들어야 한다. 

### class
* class에서 property를 선언할 때는 타입을 사용하여 정의한다. 
* class를 생성할 때에는 타입을 꼭 명시해줘야 한다.
* Dart의 class에서는 this 사용할 필요가 없고, class method 내에서는 같은 이름의 variable이 있어서 어쩔 수 없이 사용하는 것이 아니면 this를 사용하지 않는 것을 권고한다. 
```dart
class Player {
	String name = 'nico';
	int xp = 1500;
}
void main() {
	var player = Player();  // new를 붙일 필요 없다.
	print(player.name);
}
```
결과 `nico`
* player의 name을 바꾸지 못하도록 하려면 final을 추가하면 된다. 따라서 `final String name = 'nico';`로 수정한다. 
```dart
class Player {
	final String name = 'nico';
	int xp = 1500;
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player();
	player.sayHello();
}
```

### Constructors
* argument로 player의 name과 xp를 전달하여 새로운 player를 생성할 수 있도록 한다. 
```dart
class Player {
	late final String name;
	late int xp;
	Player(String name, int xp) {
		this.name = name;
		this.xp = xp; 
	}
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player("nico", 1500);
	player.sayHello();
	var player2 = Player("lynn", 2500);
	player2.sayHello();
}
```
결과 `Hi my name is nico` `Hi my name is lynn`
* constructor method의 이름은 class의 이름과 같아야 한다. 
* class에 parameter(argument)를 넘겨주면 받아서 정해진 자리에 할당한다. 
```dart
class Player {
	final String name;
	int xp;
	Player(this.name, this.xp);
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player("nico", 1500);  // positional arguments
	player.sayHello();
	var player2 = Player("lynn", 2500);
	player2.sayHello();
}
```
결과 `Hi my name is nico` `Hi my name is lynn`
* name과 xp의 타입을 작성해뒀기에 생성자에서 타입을 적어주지 않고 this로 작성해도 된다. 

### Named Constructor Parameters 
```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;
	Player(this.name, this.xp, this.team, this.age);
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player("nico", 1500, 'red', 12);  // positional arguments
	player.sayHello();
	var player2 = Player("lynn", 2500, 'blue', 12);
	player2.sayHello();
}
```

<br>

* positional parameters -> named constructor parameters 방법
 ```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;
	Player({required this.name, required this.xp, required this.team, required this.age});
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player(
		name: "nico", 
		xp: 1500, 
		team: 'red', 
		age: 12,
	);  
	player.sayHello();
	var player2 = Player(
		name: "lynn", 
		xp: 2500, 
		team: 'blue', 
		age: 12,
	);
	player2.sayHello();
}
```
* name이 null일 수도 있다는 에러를 해결하기 위해 변수 앞에 required를 붙여준다. 
* 데이터가 많은 class를 만들 때에도 각각을 key와 value 쌍으로 작성하면 된다. 