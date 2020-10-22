### url에 뜨는 review id를 해시로 숨기는 작업 (인코딩/디코딩) 
- param으로 보내줄 땐 인코딩
- param으로 받을 땐 디코딩 
> 먼저 view에 있는 id값을 인코딩해준다 ( 단, id는 integer값이므로 인코딩해주기 위해 string으로 형변환 해준다)<br>
> view의 id값은 파람으로 controller에 오게 되는데, 이때 id값은 이미 인코딩된 상태가 된다. <br>
> 그렇기 때문에 url이 id값에 따라 데이터를 가져와 페이지를 내보내야하기 때문에 디코딩을 해준다. <br>
> 여기서 디코딩 된 id값이 현재 사용자가 누른 review card의 detail page<br>
> next, previous 페이지의 경우엔 디코딩된 current_id 값을 받아 따로 인코딩을 해준다. <br>

<br>
> 그런데 여기서 디코딩이 안되거나 nil이 넘어오거나 하는 여러 변수가 생길 수 있기 때문에 예외처리를 해준다. <br>
> 예외처리는 redirect_to root_path로 해서 보여줄 페이지가 없으면 root 페이지로 넘어가게 해놓았다. <br>
<br>
(참고 : review_detail_controller.rb , _review_card.html.erb)
<br>
- Base64
string > byte : 인코딩 
byte > string : 디코딩 


### rails
- string으로 형변환 : .to_s
<br>
- 예외 처리 : begin .. rescue 
begin이 자바에서 try 같은 키워드, rescue에서 예외처리를 해준다. 

### sidekiq

### 캐싱 


#### 좀 더 차례차례 코드가 흘러가는 방향을 보자.
#### 대충 어림짐작 하지 말 것.
