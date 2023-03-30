## 플러터 스터디 TIL 3월 

###  2023년 3월 8일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230324 | Dart  |  변수 생성, Dynamic, null safety | https://nomadcoders.co/dart-for-beginners/lectures/4096 |   |

### Dart에서 변수를 어떻게 만드는가

*  void main() {
  var name = "니꼬";
} 
 var에 변수이름 + 데이터  
* void main() {
  string name = "니꼬";
  name = 'nico';
} 
string name과 같이 같은  변수의 타입을 선언한다.  

### Dynamic이란 무엇인가

* 여러가지 타입을 가질 수 있는 변수에 쓰는 키워드
* void main() {
  var name;
  name ='nice';
  name = 12;
  name = true
}
위 코드의 변수 타입은 dynamic이다.

* 변수의 타입은 var을 써도 dynamic을 써도 상관없다.
### Dynamic의 장점 
* 데이터의 타입이 궁금할때 "데이터."을 작성하면 많은 메서드가 나오면서 데이터 타입을 알 수 있다.
### null safety
* 개발자가 null값을 참조할수 없게 하는 것

* null 값을 참조한다면 런타임 에러가 뜸
* 사용자가 내 앱을 쓸 때 뜨는 에러가 런타임 에러이다
* 컴파일전에 이 에러를 잡기위해 null safety가 존재 
* void main() {
    String? nico = 'nico;
    nico = null;
    if(nico!=null) {
        nico?.isNotEmpty;
    }
    }
    * 변수  타입뒤에 ?을 넣어줌으로써 변수가 null이 될 수도 있다는 걸 알려줌 
    또는 nico.isNotEmpty의 nico에 ?을 넣어 null이 아니라면 isNotEmpty를 달라고 요청
* 어떤 변수,혹은 데이터가 null이 될 수 있음을 명시하는걸 말함 --> 어떤 데이터가 null일때 참조하지 않도록 
* dart의 변수는 기본적으로 nullable이 아님
