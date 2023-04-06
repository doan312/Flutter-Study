## 플러터 스터디 TIL 3월 

###  2023년 3월 31일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230331 | Dart  | 

### interitance

```dart
class Human { //human이라는 클래스 생성
    final String name; //human 클래스에는 name을 가지고있음(이름)  
    Human (this.name); //생성자함수
    void sayHello() { //sayHello라는 메서드 생성
        print("Hi my name is $name");
    }


}
enum Team {blue, red}

class Player extends Human {
    final Team team; // 아무도 수정 못하게 final 

    Player({
        required this.team; //named arguement를 사용하는 player 함수 생성
        required String name

        @override
        void sayhello () {
            super.sayHello();
            print('and I play for ${team}');

        }
    }) : super(name : name); // super라는 키워드를 통해 부모 클래스와 상호작용을 할 수있게 해줌
    // player 생성자에서 온 name은 그 즉시 super 생성자로 전달됨 
    // super클래스는 확장한 부모 클래스를 의미 =



}  //Human 클래스에 있는 모든 것들을 Player 클래스에 넣을 것이다 그러니 extends를 확장을 해줌


void main() {
    var player = Player(team; Team.red,
    name : 'nico'); // player 생성자 함수에 있는 name을 Human을 전달해준다.
   

}

```
* human 클래스의 생성자 함수 호출은 human의 생성자 함수가 human에 name이라는 변수를 넣어주기 때문에 Player에도 생성자 함수를 호출해줘야한다.

### Mixins

* 생성자가 없는 클래스를 말함

```dart

clas Strong {
    final double strenghtLevel = 1500.99;
}
class QuickRunner {
    void runQuick() {
    print("ruuuuuuuuuuuuuuuuuuuun");
    }
}
