### DB
- reated_at : 최초레코드 생성시 찍히는 날짜 <br>
- updated_at : 갱신 때 마다 찍히는 날짜 

### Ruby 

#### 출력 pp
* pp whatever <br>
  
  
#### 변수 
- @instances variables <br>
  각 인스턴스에서만 참조할 수 있는 변수 <br>
  객체 밖에서 접근 시 attr_accessor 메서드 사용
- :symbol <br>
  변하지 않는 개체 
- $variable <br>
  전역 변수 


### rails 터미널로 작업하기 
```bash
rails c
```

## 코드 수정이 있을 시엔 루비 터미널에서 reload! 를 한 후에 돌려본다


### DB 동기화 
```bash
rails sync:db
```

### 오늘 일
중복 컬럼 제거하기 


