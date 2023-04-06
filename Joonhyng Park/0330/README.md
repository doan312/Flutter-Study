## 플러터 스터디 TIL 3월 

###  2023년 3월 30일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230330 | Dart  |  

### cascade Notation

```


 void main() {

var nico = player(name : 'nico', xp: 1200,team 'red');
nico.name = 'las';
nico.xp = 120000000;
nico.team = 'blue';
}
```
* 여기서
```


 void main() {

var nico = player(name : 'nico', xp: 1200,team 'red')
..name = 'las';
..xp = 120000000;
..team = 'blue';
}
```
* 이런식으로 ..들은 var의 nico를 가르킨다.

### enums

```
var nico = player(name : 'nico', xp: 1200,team 'red') 
 
```
* team 'red'를 'rad'라고 쓰는 오타가 존재할 수 있는데 이 오타를 해결하는게 enums이다.
* enum을 만들기 위해서는  

* enum Team {red,blue}를 써주면
```
..team = 'blue';
```
```..team = team.blue 
```
* 으로 써줘서 실수를 줄인다. 

### abstract class

* 추상화 클래스는 다른 클래스들이 직접 구현해야하는 메소드들을 모아놓은 청사진이다.

``` 
abstract class Human{
  void walk();

}
```
* human이라는 클래스는 walk라는 메소드를 가지고 walk라는 메소드는  void를 반환해야한다. 
* 추상화클래스는 다른 클래스들이 어떤 청사진을 가지고 있어야 하는지 정의해주기 때문에 유용하다.
