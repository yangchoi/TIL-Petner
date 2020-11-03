### 라우터 개념 다시 공부하기 

```ruby
  resources :journal_likes, as:staffs_journal_likes, only[:show] do
    member do 
      put:vote
    end
  end
```

--> vote_staffs_journal_likes_url 생성됨 <br>
--> journal_like_controller.rb 에서 vote 메서드 사용 가능 


### 좋아요 버튼 만들기 작업


### table 싹 비우기 
> 테이블명.destroy_all
