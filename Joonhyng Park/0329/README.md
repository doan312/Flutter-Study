## 플러터 스터디 TIL 3월 

###  2023년 3월 8일 플러터 스터디 공부 
| 날짜       | 제목               | 설명                                | 링크                                                                             |
| ---------- | ------------------ | ----------------------------------- | -------------------------------------------------------------------------------- |
| 20230329 | Dart  |     |

### Typedef

* list를 반대로 뒤집어서 return하는 function 
 ```
 list<int> reverseList0fNumbers(List<int> list) {
    var reversed = list.revered;
    return reversed.tolist();

 }
 ```
 * typedef은  자료형에 alias를 붙일수있게한다.
 
### class
```
class player {
    late final string name = 'nico'; //late은 변수들의 값을 나중에 받아올거라는걸 의미함 선언은 여기서 했지만
     late int xp = 1500;  
     string team;
     int age;
    player({this. name,this.xp,this.team,this.age}) //this.들에 중괄호를 쳐주면 간단하게 정리가능 -->> var player = player{
        name: "nico",
        xp : 1200',
        team - 'blue',
        age = 21,
             };
             var player2 = player(
                name: "Lynn",
                xp : 2500,
                team = 'blue',
                age = 12
             )



     {
     //   this.name = name;
        this.xp;                 //값은 나중에 받아온다
    }

    }
    void sayHello() {
        print("Hi my name is $name");

    }
    
void main() {
    var player = Player("nico",1500,'red',12); //player 인스턴스 생성
    player.sayhello();
    var player2 = player("Lynn",2500,'blue',12);
    player.sayhello();
    player.name = 'lalala' //player 이름 바꾸기
    print(player.name);

}


```