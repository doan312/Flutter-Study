## 플러터 스터디 TIL 3월 

###  2023년 3월 8일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230324 | Dart  |  변수 생성, Dynamic, null safety | https://nomadcoders.co/dart-for-beginners/lectures/4096 |   |

### Function

``` 
string sayhello(string potato) => "Hello $potato nice to meet you!";

void main() {
  print(sayHello('nico'));
}

```
* => fat arrow syntax로 argument를 받아 곧바로 결과값을 return한다 좋은점 : 중괄호와 return을 생략한다.
* void는 콘술에 뭔가 출력하고있을뿐 함수에 아무것도 호출하고있지않다. 
* string을 return하는 함수를 메인으로 가져

### named paramiter

```
string sayhello( {
  string name = 'anon',
  int age = 99,
  String country = 'wakanda',
}) {
  return "$name $age $country";
}
void main () {
  print(sayhello());

}
```
* named argument는 만약 유저가 name age country 중 빼먹을때 null safety가 뜨게되는데 이를 막기위해 변수 이름에 ''을 달아 해결해준다.
 
 ``` 
 string sayhello( {
  string name ,
  int age .
  String country 
}) 
 void main () 
  print(sayhello(
    age : 12
    country : korea
    name : nico
  ));

``` 
* required를 이용하면 dart가 main에 선언이 안될시 따지고
* required modifyer는 main에 들어오는 값을 컴파일 하지않는다 이미 string 선언에서 같이 들어오는걸 알기때문

### optional positional parameters 

``` string sayhello (string name, int age,[string?  country],) =>
"$name, $age, $country";

void main() {
  sayhello('nico,'12');
}
```
* [string? 멤버변수]로 마지막 arguement없이 say hello가 선언 가능해짐

### QQ operator

* 이름을 대문자로 return하는 함수
``` 
string capitalizename(string? name) ==>name.touppercase();  

```
* null값인지 모르는 name을 touppercase에 줄수없다. 그래서
``` 
string capitalizename(string? name) {
  if (name != null) {
    return name.touppercase();

  }
}
```
* 이렇게 사용할 수있고 한번 더 간략하게하면
```
string capitalizename(string? name) => 
name != null ? name.touppercase() : 'anon';
```
* 아니면 
```
string capitalizename(string? name) => 
name?.touppercase() ?? 'anon';
 