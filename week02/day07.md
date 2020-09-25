### n+1 query 
반복적으로 불필요한 쿼리가 반복될 때 단 2개의 쿼리문으로 시간을 단축시키는 방법 <br>
<b>rails의 Model 클래스에서 includes를 사용한다. </b>

```sql
petners = Petner
          .includes(:timetables)
```
<br>
<br>
예시 ) 
만약 post 내부의 comment에서 id를 통해 총 5개의 레코드를 꺼내려고 할 때 <br>
아래의 쿼리문에서는 comment 테이블에 대해 select문을 총 5번 사용해야한다. 

```sql
select * from post;
select * from comment where id = "00"; 
...
5개..
```
<br>
<br>
그런데 이것을 아래와 같이 단 두줄의 쿼리문으로 고칠 수 있다. 

```sql
select * from post; 
select * from comment where id IN (00,00....);
```
이렇게 되면 도합 6줄이었던 쿼리문이 단 두줄로 바뀌게 되는 것이다. <br>
이는 실행 속도에 차이를 미친다고 한다. 


### .& : Safe Navigation Operator
receiver 가 nil 일 때 method call 을 skip 한다.
nil을 return하고 method의 arguments를 evaluate 하지 않는다.
> 빈값을 리턴할 수 있는 메서드에 쉽게 체이닝할 수 있다.


### 오늘 할 일
user_ping 에서 마지막 접속 기록 정보 확인해 펫시터 구하기의 펫시터 목록에 넣기 <br>
