#### 오늘 한 일
- 결제 페이지 생성 및 완성 

#### 막힌 부분 
- 배치 작업 중 중복결제 부분에 model에서 생성된 scope인 duplicates를 view에 적용시키는 것 


#### model에서 만들어진 scope 가져다 쓰기
- 중복 필터를 적용시켜야하는 상황에서 model 쪽 코드를 보니 duplicates 라는 scope가 만들어져 있는 상황,
- 이 scope는 duplicates 라는 이름으로 중복 제거된 데이터를 불러오는 쿼리를 가지고 있다. 

```ruby
scope :duplicates, lambda {
    where(suggestion_id:
          Payment.select(:suggestion_id)
                 .group(:suggestion_id, :status)
                 .where(status: 1)
                 .having("count(*) > 1"))
                 .order(suggestion_id: :desc)
  }
```

- view 에서는 아래와 같이 scope를 명시해 줄 수 있다. 
- 이후 url로 넘어간다. 

```ruby
<%= link_to staffs_payments_path(:scope => "duplicates"), class: "ui button", id: "duplicates" do %>
          중복결제 (<%= Payment.duplicates.count %>) 
<% end %>
```
- 위의 코드까지 작성하면 중복 결제 라는 버튼을 눌렀을 때 중복 결제가 된 리스트가 뜨지 않는다. 
- 직접 필터링에 적용시켜야한다. 
- controller에 가서 q에다 해당 scope를 적용시킨다. 

```ruby
@q = @payments.duplicates.ransack(filter_column) if(params[:scope] == "duplicates")
```

- params에서 scope 중 duplicates 라는 값을 적용시키는 q를 만든다. 
- 필터링을 하는 q 변수에 scope를 직접 적용시키면 해당 scope가 적용된 list가 view에 나타난다. 

