### CSRF (crorss-site request forgery) Token
- 사용자 세션에 임의의 난수값을 저장하고 사용자의 욧청마다 해당 난수값을 포함시켜 전송 
- 이후 back end 에서 요청을 받을 때 마다 세션에 저장된 토큰값과 요청 파라미터에서 전달되는 토큰값이 같은지 검증. 

### 캐시 
- rails에서 css/js 파일 및 이미지 파일을 저장할 수 있는 방법은 크게 public, assets 폴더가 있는데 <br>
이 둘의 차이는 캐싱의 영향 유무임. 
- 캐시 : 어떤 웹 사이트 접속시 그 사이트의 이미지 파일, css, js 등을 기억하는데 한 번 기억하면 다음 접속시에 좀 더 빠르게 접속이 가능하게 됨



_____________


## ruby 

### before_action 
액션 내 동작되는 코드를 공통적으로 사용되는 코드로서 하나로 묶음 <br>
가령 id 탐색을 게시물 열람/ 수정/ 삭제 시 공통으로 수행한다면 각 액션에서 탐색하지 않고 <br>
before_action으로 묶어 해당 액션이 사전에 액션이 시작되기 전에 어떠한 액션을 거치게 만들 수 있음 

```ruby
before_action :set_post, only: [:show, :edit, :update, :destroy]

def ..
end
..

private
	def set_post
		@post = Post.find(params[:id])
end
  
```
set_post 앞에 private을 선언한 것은 캡슐화로, <br>
before_action을 거쳐간 경우가 아니면 외부에서 접근할 수 없도록 막아놓은 것

### ruby 코드 스타일 

#### 중첩된 조건문 

- 중첩해서 조건문이 연속해서 나오는 상황 피하기, 
- 로직 흐름 값이 유효하지 않은 경우 즉시 return, enxt, break 등으로 이탈하도록 
<br>
- 나쁜 예 
```ruby
def compute_thing(thing)
  if thing[:foo] 
    update_with_bar(thing)
    if thing[:foo][:bar]
      partial_compute(thing)
    else
      re_compute(thing)
    end
  end
end
```
- 좋은 예 
```ruby
def compute_thing(thing)
  return unless thing[:foo]
  update_with_bar(thing[:foo])
  return re_compute(thing) unless thing[:foo][:bar]
  partial_compute(thing)
end
```
- else 나 elsif로 넘어가지 않고 return 등으로 이탈시키는 구문 : guard clause
- 조건문이 중첩되는 상황을 회피 

#### scope 사용의 예 
- 좋지 않은 예 

- app/controllers/users_controller.rb
```ruby
class UsersController < ApplicationController 
  def index
    @users = User.where(active: true).order(:last_login_at)
  end
end
```
- 위의 컨트롤러 코드는 재사용성이 떨어지고 테스트가 어려움
- User라는 모델에 어떤 필드가 있고 어떤 값을 가지고 있는지 컨트롤러가 알고 있다는 것은 좋지 않음 

- 수정 
- 모델 내 데이터와 관련된 query method 는 모두 감추는 메소드를 모델에 추가함 (scope 사용) 
- app/models/users.rb
```ruby
class User < ActiveRecord::Base
  scope :active. -> { where(active: true) }
  scope :by_last_login_at, -> { order(:last_login_at) }
end
```

- app/controllers/users_controller.rb
```ruby
class UsersController < ApplicationController
  def index
    @users = User.active.by_last_login_at
  end
end
```
- 모델과 관련된 것은 모델 내부에서 처리하도록 하고, 컨트롤러는 가장 high-level 로직만 다루도록


### 생성자는 클래스 이름 대신 "initialize"

### 자바와 비교한 루비 (차이점)
https://www.ruby-lang.org/ko/documentation/ruby-from-other-languages/to-ruby-from-java/


### 메서드 액세스 
- public : 공개
- private : 명시적 수신 없이 메서드를 호출할 수 있음, self 만이 private 메서드 호출의 리시버로 허용됨 
- protected : 밖에서 호출했을 때 주의해야한다는 것, 클래스나 하위 클래스 인스턴스에서 호출할 수 있고 다른 인스턴스를 리시버로 사용할 수 있음 


### ActiveStorage
- 레일즈의 aws의 클라우드 서비스 연동
