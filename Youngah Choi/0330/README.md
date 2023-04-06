## 플러터 스터디 TIL 3월 

###  2023년 3월 30일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/30 | Named constructors, Cascade Notation, enums, abstract  | Named constructors, Cascade Notation, enums, Abstract classes  |  |   


### Named Constructors
```dart
class Player {
	final String name;
	int xp;
	String team;
	int age;
	Player({required this.name, required this.xp, required this.team, required this.age});
	Player.createBluePlayer({required String name, required int age,
	}) :  // player를 초기화하는 method, 필요에 따라 다른 인자를 받게 할 수 있다.
		this.age = age,
		this.name = name,
		this.team = 'blue',
		this.xp = 0;
	Player.createRedPlayer(String name, int age) : 
		this.age = age, 
		this.name = name,
		this.team = 'red',
		this.xp = 0;
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var player = Player.createBluePlayer(
		name: "nico", 
		age: 12,
	);  // named
	player.sayHello();
	var redplayer = Player.createRedPlayer("lynn", 12,);  // positional
	player2.sayHello();
}
```

* `Player.createBluePlayer()`에서는 Player 객체를 만들고, :을 사용하여 사용자에게 받은 parameter 값으로 Player 객체를 초기화한다. 
* named parameter는 기본적으로 required 속성이 없다. 
* 콜론을 사용해 argument와 property를 1:1로 초기화하는 생성자를 만든다. 

### Cascade Notation
```dart
class Player {
	String name;  // 사용자가 이름 변경 가능하도록 설정
	int xp;
	String team;

	Player({
		required this.name, 
		required this.xp, 
		required this.team,
	});

	void sayHello() {
		print("Hi my name is $name");
	}
}	
void main() {
	var nico = Player(name: 'nico', xp: 1200, team: 'red');
	nico.name = 'las';
	nico.xp = 12000;
	nico.team = 'blue';
}
```
* `nico.name = 'las';` `nico.xp = 12000;` `nico.team = 'blue';` 코드에서 nico가 반복되는데, Cascade operator를 사용하면 다음과 같이 main() 함수를 수정할 수 있다. 
```dart
	void main() {
		var nico = Player(name: 'nico', xp: 1200, team: 'red')  // ; 삭제
		var potato = nico
		..name = 'las'  // . - nico를 가리킨다.
		..xp = 12000
		..team = 'blue';
	}
```

### Enums
* Enums : 개발자가 값을 넣을 때 잘못 적는 실수를 하지 않게 도와준다. 선택의 폭을 좁혀주는 역할을 한다. 
```dart
enum Team {red, blue}
enum XPLevel {beginner, medium, pro}
class Player {
	String name;  
	XPLevel xp;
	Team team;

	Player({
		required this.name, 
		required this.xp, 
		required this.team,
	});
	void sayHello() {
		print("Hi my name is $name");
	}
}
void main() {
	var nico = Player(
		name: 'nico', 
		xp: XPLevel.medium, 
		team: Team.red,
	);
	var potato = nico
	..name = 'las'
	..xp = XPLevel.pro
	..team = Team.blue
	..sayHello();
}
```

### abstract class
* **abstract class** : 다른 클래스들이 어떤 청사진을 가지고 있어야 하는지 정의해주기에 유용하다. method의 이름과 반환 type만 정해서 정의할 수 있다. 
* 추상화 클래스로는 객체를 생성할 수 없다. 다른 클래스들이 직접 구현해야 하는 method들을 모아 놓은 일종의 청사진(blueprint)이다. 또한, 특정 method를 구현하도록 강제한다. 

```dart
abstruct class Human {
	void walk();  // 함수가 반환하는 값 정의
}
enum Team {red, blue}
enum XPLevel {beginner, medium, pro}

class Player extends Human{  // Human 클래스를 상속받는다. 
	String name;  
	XPLevel xp;
	Team team;

	Player({
		required this.name, 
		required this.xp, 
		required this.team,
	});
	void walk() {
		print('I am walking');
	}

	void sayHello() {
		print("Hi my name is $name");
	}
}
class Coach extends Human {
	void walk() {
		print('the coach is walking');
	}
}
void main() {
	var nico = Player(
		name: 'nico', 
		xp: XPLevel.medium, 
		team: Team.red,
	);
	var potato = nico
	..name = 'las'
	..xp = XPLevel.pro
	..team = Team.blue
	..sayHello();
}
```
* Human abstract class는 이를 상속받는 모든 class가 가지고 있어야 하는 method를 정의하고 있다. 