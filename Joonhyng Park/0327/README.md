## 플러터 스터디 TIL 3월 

###  2023년 3월 27일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230327 | Dart  |  set,list,function,collection for,etc. |  |   |

### Set
```
 void main() {
  Set<int> numbers = {1,2,3,4};
  numbers.add(1);
   
}

```
* set은 list와 기능은 유사함
* Set은 numbers.add(1)가 사용되도 적용되지않는다.
### list
``` void main() {
  List<int> numbers = [1,2,3,4];
numbers.add(1);
numbers.add(1);
numbers.add(1);
print(numbers);
}
```
### function
```
void sayHello(String name) {
  print("Hello $name nice to meet you! ");

}
void main() {

  print(sayHello(nico));

}

```

* return 대신에 far arrow syntax 사용 가능
### collection for
``` 
void main() {
  var oldfriends = ['nico','lynn'];
  var newFriends = [  
    'lewis',
    'ralph',
    'darren',
    for(var friend in oldFriends)  "♥ $friend",
  ];
  print(newfriends);
} 
```
* newfriends 안의 oldfriends 리스트에 변형주면서 연결된 리스트 출력 
* 상당히 코드를 줄임 
### object 
* 기본적으로 어떤 자료형이든 될 수 있음

### Maps
```
void main() {
  map<List<int,bool>player = {
    [1,2,3,5] : true
  };  
} 
```
* key로 integer List, value로는 bool 생성 어떤 key든 value든 명시할 수있다.
* map도 method와 property를 가지고있는데 
기능들은 찾아보면 됨 
 