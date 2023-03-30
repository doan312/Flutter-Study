## 플러터 스터디 TIL 3월 

###  2023년 3월 27일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/27 | Map, Set  | collection for, Map, Set  |  |   


### Collection for

* **collection for**
```dart
void main() {
	var oldFriends = ['nico', 'lynn'];
	var newFriends = [
		'lewis',
		'ralph',
		'darren',
		for(var friend in oldFriends) "❤ $friend",
		// oldFriends를 newFriends에 추가, string interpolation 이용
	];
	print(newFriends);
}
```
결과 `[lewis, ralph, darren, ❤ nico, ❤ lynn]`
oldFriends라는 리스트와 newFriends라는 리스트를 사용하였다. collection for를 사용하면 시간을 절약할 수 있다. `for(var friend in oldFriends) { newFriends.add()}`대신에 `for(var friend in oldFriends) "❤ $friend"`를 사용하면 된다.
 
* **collection if**  : List를 생성할 때 조건에 따라 element를 추가할 수 있다. 메뉴나 navigation bar를 만들 때 user가 로그인 했는지 나타내는 버튼을 추가하고 싶은 경우에 사용할 수 있다. 



### Map
* **Map** - JavaScript나 TypeScript의 object, python의 dictionary와 같은 것이다. 
* Dart에선 모두 class이고 모든 것이 class에서 나온다. 따라서 map도 method와 property를 가지고 있다. 

```dart
void main() {
	var player = {
		'name': 'nico', 
		'xp' : 19.99, 
		'superpower': false,
	};
}
```
var를 사용할 때는 컴파일러가 자료형을 정하기 때문에 자료형을 명시할 필요가 없다. 이 코드에서 player의 자료형은 `Map<String, Object>`이다. 이는 key와 value로 이루어진 자료구조인 Map을 만들었는데 key는 String, value는 Object라는 의미이다. Dart에서는 모든 것이 object로부터 생기기에 object는 기본적으로 어떤 자료형이든 될 수 있다. object는 TypeScript에서 any와 같다. 

* 빈 맵 생성
```dart
void main() {
	Map<int, bool> player = {
		1: true,
		2: false,
		3: true,
	};
}
```

* 복잡한 맵 생성
```dart
void main() {
	Map<List<int>, bool> player = {
		[1, 2, 3, 4, 5]: true,
	};
}
```

* containsKey() : 특정 요소가 포함됐는지 체크

* containsValue() : 특정 값을 포함하는지 체크

#### Map List 
```dart
void main() {
	List<Map<String, Object>> players = [
		{
			'name': 'nico',
			'xp': 199.999,
		}
	];
}
```
key : String, value : Object
* key와 value를 가지는 구조로 특정 형태를 가지는 object를 만들 때 API로 얻은 데이터는 class를 사용하는 것을 추천한다.


### Set
```dart
void main() {
	var numbers = {1, 2, 3, 4};
}
```
`var numbers = {1, 2, 3, 4};` 대신에 `Set<int> numbers = {1, 2, 3, 4};`로도 작성할 수 있다. 

#### Set과 List의 차이점
* Set은 순서가 있다. 
* Set에 속한 모든 아이템들은 유니크하다. 
예를 들어 `numbers.add(1);`로 numbers에 1을 추가하려고 할 때 이를 여러 번 반복하고 `print(numbers);`로 numbers를 출력해도 결과는 `{1, 2, 3, 4}`이다.  List와 같지만 모든 요소가 유니크해야 한다. 

* **Set** : 순서가 있고 요소가 항상 하나씩만 존재해야 할 경우에 사용, 중괄호 사용
```dart
void main() {
	Set<int> numbers = {1, 2, 3, 4};
	numbers.add(1);
	numbers.add(1);
	numbers.add(1);
	print(numbers);
}
```
결과 `{1, 2, 3, 4}`

* **List** : 요소의 중복이 허용되는 경우에 사용, 대괄호 사용
```dart
void main() {
	List<int> numbers = [1, 2, 3, 4];
	numbers.add(1);
	numbers.add(1);
	numbers.add(1);
	print(numbers);
}
```
결과 `[1, 2, 3, 4, 1, 1, 1]`

* Dart에서 Set : Python의 Tuple

* Dart에서 List : Python의 List