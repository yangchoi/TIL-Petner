### 오늘 한 일 
- 예쁜 돌봄 사진에 아이템끼리 가려져 좋아요 버튼이 눌러지지 않는 현상 수정 
- 단순히 width를 늘려서 해결함
- 후에 item 안의 요소를 카운트 해서 몇개 이상이면 줄바꿈을 수행하는 식으로 수정하도록 (하다가 안되어서 급하게 width 늘리고 커밋..)

- 여전히 에쁜 돌봄 사진 로딩 속도 줄이는 작업 중 
- 이제 와서 든 생각이지만 사진 크기에 따라 로딩 속도가 영향을 받는건 그리 크지 않은 것 같음
- 그렇게 치면 돌봄 일지 페이지도 로딩이 빨라야하는데 그다지 빠르지 않음 (사진들이 다 작음) 
- 뭔가 다른 요소를 좀 생각해볼 필요가 있어 보임.. 
- sidekiq도 코드를 짜보았는데 실행이 잘 되지 않아서 내일 노라에게 다시 물어볼 것 
- 작업이 더뎌지고 있음, 모르는 건 바로바로 물어보자.. 


____

### 체리픽 
- 원하는 커밋만 고를 수 있음 
- 작업물은 변동이 있으면 바로바로 커밋을 하는게 좋을 듯 함 
- 너무 오랫동안 커밋을 안하면 좀 헷갈림
- glum도 제때 제때 해주자 


_________________

### sidekiq


1. app/workers에 worker cnrk 

```ruby
class HardWorker
  include Sidekiq::Worker

  def perform(name, count)
    # do something
  end
end
```
- perform 메소드는 심플하고 String, integer, boolean과 같이 JSON에 지원받는 기본형이어야함 
- 복잡한 루비 객체는 작동하지 않음 

2. 실행될 작업을 만듦

```ruby
HardWorker.perform_async('bob', 5)
```
- perform_async은 perform의 인스턴스 메소드 
- 미래에 실행될 작업도 만들 수 있음 

```ruby
HardWorker.perform_in(5.minutes, 'bob', 5)
HardWorker.perform_at(5.minutes.from_now, 'bob', 5)
```

3. 사이드킥 실행
```ruby
bundle exec sidekiq
```

