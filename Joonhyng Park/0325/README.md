## 플러터 스터디 TIL 3월 

###  2023년 3월 25일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230325 | Dart  |  final,late,num,list,collection if,string interpolation | https://nomadcoders.co/dart-for-beginners/lectures/4103|   |


### Final 변수 타입

``` void main() {
  final name = 'nico';
  name = 'nico';
}
```
* final은 변수를 선언하고 그 변수를 다시 수정할 수 없게 만들어준다.

### late 수식어

``` void main() {
  late final String name;
  //do something, go to api
  name = 'nico';
}
```
* final이나 var 앞에 붙여줄 수 있는 수식어 
* 초기 데이터없이 변수를 선언할 수 있게 해준다 
* api의 요청으로 데이터를 받아들이고 그 데이터를 변수에 넣는다 

### 기본 데이터 타입 
``` 
num x = 1.1;
```
* num 자료형은 int 또는 double 일 수도있다.

### list
``` void main() {
  var numbers = [1,2,3,4];
   numbers.first;
}
```
* number first - > 첫번째 요소 호출

### collection if
``` 
void main() {
  var givemefive = true;
  var number = [1,2,3,4,
  if (givemefive) 5,
  ]
};

if (givemefive) {
  numbers.add(5);

}
```
* givemefive가 true라면 요소 5를 추가할 수 있다.

### String interpolation 

* text에 변수를 추가하는 방법

``` 
void main () {
  var name = 'nico';
  var age = 10;
  var greeting = "Hello every one my name is $name and i am {$age + 2};
  print (greeting);
    }
    ```

    *달러 기호 + 변수이름으로 표현할 수 있다.
