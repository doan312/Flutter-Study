## 플러터 스터디 TIL 3월 

###  2023년 3월 31일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/31 | Inheritance, Mixins  | Inheritance, Mixins  |  |   


### Inheritance
* **Inheritance**(상속)
```dart
class Human {
	final String name;
	Human(this.name);  // constructor
	void sayHello(){
	print("Hi my name is $name");
	}
}
enum Team {blue, red}
class Player extends Human {
	final Team team;
	// named argument 사용하는 Player constructor
	Player({
		required this.team, 
		required String name}) : super(name);  // :을 적고 super 생성자 호출
}
void main() {
	var player = Player(team: Team.red, 
	name: 'nico');
}
```
* `super` 키워드를 통해 확장을 한 부모 클래스와 상호작용할 수 있게 한다. super에 name을 전달하면 이 클래스를 전달한 name과 함께 호출하게 된다. 
* super 클래스는 확장한 부모 클래스를 의미한다. 

```dart
class Human {
	final String name;
	Human(required this.name); 
	void sayHello(){
	print("Hi my name is $name");
	}
}
enum Team {blue, red}
class Player extends Human {
	final Team team;
	Player({
		required this.team, 
		required String name}) : super(name: name);  // 확장한 부모 클래스의 super method를 호출
		@override  // Human에서 온 sayHello()를 직접 만든 method로 override(대체)
		void sayHello() {
			super.sayHello();  // super로 부모 클래스 접근
			print('and I play for ${team}');
		}
}
void main() {
	var player = Player(team: Team.red, 
	name: 'nico');
	player.sayHello()
}
```
* super : 확장(상속)한 부모 클래스의 property에 접근하게 하거나 method를 호출할 수 있게 한다. 확장한 부모 클래스가 생성자를 포함하고 있는데 그 클래스를 다른 곳에서 사용하려면 필요한 값을 전달해야 하고 부모 클래스의 생성자를 호출해야 한다. 

### Mixins 
* **Mixin** : **생성자가 없는 클래스**를 의미한다. 클래스에 프로퍼티를 추가할 때 사용한다. 여러 클래스에 재사용이 가능하다. 
```dart
class Strong {
	final double strengthLevel = 1500.99;
}
class QuickRunner {
	void runQuick() {
		print("run!");
	}
}
enum Team {blue, red}
class Player with Strong, QuickRunner, Tall // 상속받지 않고도 다른 클래스의 property와 method를 긁어온다.
{ 
	final Team team;
	Player({
		required this.team, 
		required String name}) : super(name: name);
		@override
		void sayHello() {
			super.sayHello();
			print('and I play for ${team}');
		}
}

class Tall {
	final double height = 1.99;
}
void main() {
	var player = Player(team: Team.red, 
	name: 'nico');
	player.sayHello()
}
``` 
#### extend와 Mixin
* extend : 확장한 클래스가 부모 클래스가 된다. 자식 클래스는 부모 클래스를 super로 접근할 수 있고 그 순간에는 부모 클래스의 인스턴스가 된다. 
* Mixin : with 키워드를 사용하여 Mixin 내부의 property와 method를 가져온다. 

