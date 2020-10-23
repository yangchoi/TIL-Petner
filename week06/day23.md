### url에 뜨는 review id를 해시로 숨기는 작업 (인코딩/디코딩) 
> param으로 보내줄 땐 인코딩 <br>
> param으로 받을 땐 디코딩 
1. 먼저 view에 있는 id값을 인코딩해준다 ( 단, id는 integer값이므로 인코딩해주기 위해 string으로 형변환 해준다)<br>
2. view의 id값은 파람으로 controller에 오게 되는데, 이때 id값은 이미 인코딩된 상태가 된다. <br>
3. 그렇기 때문에 url이 id값에 따라 데이터를 가져와 페이지를 내보내야하기 때문에 디코딩을 해준다. <br>
4. 여기서 디코딩 된 id값이 현재 사용자가 누른 review card의 detail page<br>
5. next, previous 페이지의 경우엔 디코딩된 current_id 값을 받아 따로 인코딩을 해준다. <br>

**>> 추가**
> 그런데 여기서 디코딩이 안되거나 nil이 넘어오거나 하는 여러 변수가 생길 수 있기 때문에 예외처리를 해준다. <br>
> 예외처리는 redirect_to root_path로 해서 보여줄 페이지가 없으면 root 페이지로 넘어가게 해놓았다. <br>

<br>
(참고 : review_detail_controller.rb , _review_card.html.erb)
<br>
- Base64

string > byte : 인코딩 <br>
byte > string : 디코딩 


### rails
- string으로 형변환 : .to_s
<br>
- 예외 처리 : begin .. rescue 
begin이 자바에서 try 같은 키워드, rescue에서 예외처리를 해준다. 

### sidekiq
ruby on rails에서는 비동기 작업 처리로 사이드킥을 주로 사용 <br>
사이드킥은 등록된 작업을 레디스 큐에 저장해놓고 워커들에서 가져가 처리하는 방식으로 동작 <br>
의도치 않게 실행되어선 안되는 작업이 큐나 예약 작업에 등록되는 경우가 종종 있는데 <br>
이런 경우 사이드킥의 api를 사용해 특정 작업들만 삭제해 줄 필요가 있음 

### Redis(remote dictionary server) 
키-값 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템 
- redis에서 사용할 수 있는 5가지의 데이터형 : string, lists, sets, sorted sets, hashs

### 새로 알게된 부분 
- sidekiq
- 캐싱 
- Base64 
- 파람으로 보내줄 땐 인코딩됨

#### 개선점 
  - 좀 더 차례차례 코드가 흘러가는 방향을 보자.
  - 대충 어림짐작 하지 말 것.
  - 모르는 것은 그날 그날 공부 
  
#### 오늘 한 일 
- welcome 페이지의 review 부분에 detail page로 들어갈 시 url에 id값을 해시로 숨기는 작업 
(리뷰 수가 보이게 되므로)
- welcome 페이지의 journal 부분 틀 생성 

#### 내일 할 일
- welcome 페이지의 journal 부분 이미지 위치 파악해서 가져오기 
- journal 완성
- welcome 페이지의 review 부분의 화살표를 review card 바깥으로 내보내기 (리뷰 가림) 

