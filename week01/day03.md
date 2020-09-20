### 오늘의 일
#### petner 페이지에 status 필터적용 

##### 문제 
- petners의 필터에서 status 선택지를 action 외엔 전부 non-action으로 처리
- petners의 _filter.html.erb 에서 선택한 status의 값이 필터값이 담긴 해시 "q" 에 파라미터로 담겨 petners_controller.rb로 넘어가 처리 <br>
- 그런데 해시 q에서 status 파라미터를 꺼낼 방법을 잘 몰랐음


#### 해결
- 로그를 보고 param(파라미터)이 어떻게 넘어오고 있는지 본다. 
```ruby
  Rails.logger.error params
  Rails.logger.error params.dig("q")
  Rails.logger.error params.dig("q", :status_eq)
```
```bash
 Parameters: {"utf8"=>"✓", "q"=>{"id_eq"=>"", "user_id_eq"=>"", "user_name_cont"=>"", "available_locations_name_cont"=>"", "university_cont"=>"", "status_eq"=>"active", "user_username_eq"=>"", "user_phone_eq"=>""}, "commit"=>"필터"}
```
위의 로그를 보면 status_eq 라는 key값이 들어오고 있으므로 그 값을 가지고 active인지 non-active 인지를 판별한다 
```ruby
filter_status = params.dig('q', :status_eq)
    if filter_status.present?
    # status_eq가 존재하는지?
      if filter_status == "active"
      # 만약 존재한다며 그 값이 active인지?
        @petners = @petners.active
        # active라면 @petners에 active를 뿌려준다 
      else
        @petners = @petners.where.not(status: 'active') 
      end
    end 
```


### gem ransack
### nill guard
