## 플러터 스터디 TIL 3월 

###  2023년 3월 23일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 03/23 | Dart 변수 | Dart 변수, Dynamic, null safety  | https://dartpad.dev |   |


### Dart에서의 변수 선언
* var 키워드 사용

* var 키워드를 사용하지 않고 명시적으로 변수의 type을 지정

#### var 키워드
* var 키워드와 변수 이름, 저장하고 싶은 데이터를 작성한다.
```
void main() {
    var name = '영아';
}
```
* 변수의 type을 구체화할 필요가 없는 이유 : Dart 컴파일러가 name이 String인 것을 알기 때문이다.
* 변수 업데이트가 가능하다. 단, 값을 업데이트 할 때는 변수의 본래 type과 일치해야 한다.
* 변수를 수정할 때는 같은 type으로 지정해야 한다. 
```
void main() { 
    var name = '영아'; 
    name = 1;  // 정수형이기에 string과 맞지 않아서 작동하지 않는다.
} 
```
#### 명시적으로 변수 Type 지정
```
void main() {
    String name = '영아';
    name = 'yeonga';
}
```
* 데이터의 type만 유지한다면 변수 업데이트가 가능하다.

##### 각각의 변수 선언 방법을 사용하는 경우
* var 키워드 사용 : 함수나 메소드 내부에 지역 변수를 선언할 때 사용한다. 컴파일러가 타입을 알고 있기에 일일이 지정할 필요 없다.
* 변수 타입 지정 : 클래스에서 변수나 property를 선언할 때 사용한다.
 
### Dynamic
* dynamic : 여러 가지 타입을 가질 수 있는 변수에 사용하는 키워드
* 변수를 선언할 때 변수에 아무것도 지정해주지 않고 마우스 커서를 가져다 대면 type이 dynamic이라고 표시된다.
```
void main() {
    var name;  // dynamic name;으로도 가능
    name = '영아';
    name = 'yeonga';
    name = 2;
    name = true;
}
```
* 변수의 type이 dynamic이면 위의 코드 모두 가능하다.
```
void main() {
    dynamic name;
    if(name is String) {}
```
* Dart가 변수의 type을 모를 때는 method가 많지 않다. 그러나 조건문인 if문의 {} 안에서는 name의 타입이 String인 것을 알기에 자동완성이 되는 옵션이 많다.

#### dynamic이 필요한 이유
1. 변수가 어떤 type인지 알기 어려운 경우가 있기 때문이다.
2. dynamic으로 돌아가는 것이 유용한 경우도 있기 때문이다.

#### dynamic의 특징 
1. dynamic 변수로 작업을 할 것이라면 먼저 type을 확인해야 한다.
2. dynamic은 정말 필요한 경우에만 사용해야 한다. 

### null safety
* null safety : 개발자가 null 값을 참조할 수 없도록 하는 것으로, 컴파일 전에 런타임 에러를 잡아준다. 코드에서 null 값을 참조하면 런타임 에러가 뜨게 된다.
* 런타임 에러 : 사용자가 앱을 사용하던 중에 뜨는 에러
#### null
* null : 아무것도 있지 않음을 뜻한다. 이 값을 참조할 때 문제가 발생한다. 이를 Dart에서는 null safety로 해결한다. dart에서는 어떤 변수가 null이 될 수 있음을 정확히 표시해야 한다.
```
// without null safety
bool isEmpty(String string) => string.length == 0;
// string을 받아서 true나 false를 리턴하는 함수, string의 length가 0인지 판별
main() {
    isEmpty(null);
}  // 런타임 에러 발생 (NoSuchMethodError)
```
* NoSuchMethodError 이유 : String을 보내는 곳에 null을 보내서 null을 보내준 뒤에 string의 length라는 속성에 접근한다. 이때 string이 null인데 null에는 length라는 속성이 없기 때문에 에러가 발생한다. 


```
void main() {
    String nice = 'nico';  // String만 가능, nullable로 하려면 ?를 넣어야 한다.
    nico = null;
}
```
* 위의 코드는 nico가 오직 string이어야만 하기 때문에 불가능하다.  

#### nullable
```
void main() {
    String? nice = 'nico';
    nico = null;
}
```
* nico가 String과 null 둘 다 가능하다는 것을 Dart가 알기에 에러가 사라진다.

```
void main() {
    String? nice = 'nico';
    nico = null;
    nico.length;  // nico가 null일 수도 있다고 알려준다. 그래서 length라는 값 사용 전에 확인한다.
    if(nico != null) {  // nico가 null이 아닐 경우
    nico.isNotEmpty;
}
```

#### Dart의 null safety
* 어떤 변수 혹은 데이터가 null이 될 수 있음을 명시하는 것, 어떤 데이터가 null일 때 참조하지 않도록 도와준다.

* 기본적으로 모든 변수는 non-nullable이므로 null이 될 수 없다.
* 어떤 변수를 nullable로 즉, String도 null도 될 수 있게 하려면 String 뒤에 ?만 넣어주면 된다. 그렇게 하면 이 변수가 null이 될 수도 있다는 것을 Dart가 알기에 이 변수를 사용하기 전에 확인을 해야 한다. 그러나 시간이 오래 걸린다.
* API에서 데이터를 받아올 때 null safety를 볼 수 있다. 하지만 대부분의 경우에 변수가 null인지 걱정할 필요 없다.

##### 단축 문법

```
void main() {
    String? nice = 'nico';
    nico = null;
    nico?.isNotEmpty; 
    // nico?으로 이 값이 존재하는지 확인하고 이후의 연산을 진행한다.
}
```
* nico가 null이 아니라면 isNotEmpty 속성을 달라고 요청한다.