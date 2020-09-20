### DB
- created_at : 최초레코드 생성시 찍히는 날짜 <br>
- updated_at : 갱신 때 마다 찍히는 날짜 

#### DB에서 university 컬럼을 
### Ruby 

#### active record 


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
### 켜진 서버 확인하기 
```bash
ps -ef
ps -ef | grep rails
ps -ef | grep ruby
```

#### 코드 수정이 있을 시엔 루비 터미널에서 reload! 를 한 후에 돌려본다

#### ruby 터미널에서 SpendingService 클래스의 import_csv 메서드 돌려보기 
```ruby
SpendingService.new.import_csv
```

### DB 동기화 
```bash
rails sync:db
```
루비 터미널 밖에서 함 

### Git 
#### pr시 
- git pull upstream master 를 glum으로 줄여서 사용가능 <br>
- branch 이름을 작업 내용에 부합하게 작성 <br>
- commit message를 구체적으로 작성 <br>
- description은 작성한 commit message를 풀어 쓴 정도로 작성 (문장으로도 가능) 

#### git-flow


### 오늘 일
- 지출통계 csv 갱신할 때 수치 오류 제거 <br> 
import한 csv 파일에서 date(csv col)값이 없으면 새로 생성(new), 있으면 update 시키는 작업 <br>

- if 문에서 아래와 같이 date 컬럼의 유무를 확인 
```ruby
if Spending.where(date: row['date']).present? 
```
- 만약 date가 있다면 created_at을 desc로 order하여 그 첫번째 값을 date로 뽑아 spending에 담는다 
```ruby
spending = Spending.where(date: row['date']).order(created_at :desc).first
```
그리고 그 spending을 update해준다 <br>
update는 그 자체로 save를 한다.

```ruby
spending.update(date:row['date'], 
                        facebook:row['facebook'],
                        naver:row['naver'],
                        facebook:row['facebook'],
                        google:row['google'],
                        search_ads:row['search_ads'],
                        kakao:row['kakao'],
                        viral:row['viral'],
                        outsourcing:row['outsourcing'],
                        others:row['others'],
                        total:row['total'])
```

만약 date값이 없다면 그대로 Spending.new를 해준다

```ruby 
 t = Spending.new
 t.date = row['date']
 ...
 t.save
```

- petner admin 페이지 필터에 university 항목 추가하기 

렌더링된 파일은 파일명 앞에 언더바를 붙인다 <br>

예시 )
app>views>staffs>petners>index.html.erb 의 index.html.erb 파일에서 <br>
```ruby
<%= render 'filter', counts"@counts%>
```
를 렌더링하면 아래와 같은 파일명으로 만들어야한다.<br>
_filter.html.erb


