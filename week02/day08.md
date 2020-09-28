#### Rails Active Record Association 
##### 관계 유형들 
| DB를 클래스처럼 만들어서 객체화해 사용한다. Model에서 이루어진다. 
- belongs_to B B 객체의 예에 속해있다. 
- has_one B B객체의 예를 하나 갖는다. 
- has_many B B 객체의 예를 여러개 갖는다. 
- has_one : through B B 객체의 예를 통해 하나 갖는다.
- has_and_belongs_to_many B B 객체의 예에 속해 있으면서 동시에 B 객체의 예를 많이 갖는다. 


https://rubykr.github.io/rails_guides/association_basics.html#has_many

Model 에러 아래와 같이 지정을 하면 view에서 지정한 변수로 불러낼 수 있다. 

- petner.rb
```ruby
has_many :user_pings
...
```
- _petner.html.erb

```ruby
<% if petner.user_pings.present? %>
...
```

이로써 petner가 user_pings 등 여러개의 객체를 갖게 된다.<br>
<br>
model에서 테이블을 객체로 지정해주기 이전에 위의 코드는 UserPings 라는 테이블에서 petner_id 를 찾기 위해서 아래와 같이 작성해야했다. 
```ruby 
<% if UserPings.where(petner_id: petner.id).present? %>
```


#### rails에서 새 페이지 생성 
- staffs/journal

```bash 
rails g staffs_index journal 
```

#### rails에서 image url 다루는 방법

```ruby
include ImageLinkable
```
image_linkable.rb에서 각 image url들에 대한 메서드들을 만든다.<br>
메서드들 간의 연결고리를 잘 살펴보자..


#### 오늘 한 일 
돌봄일지 페이지 생성 
