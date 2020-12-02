#### before_action
- 컨트롤러에 정의된 메소드가 실행되기 전에 특정 처리할 때 사용
- action controller의 filter 안에 분류되는 기능 

```ruby
before_action: 메소드명 
```

- 위와 같이 기술하면 해당 컨트롤러에 있는 모드 메소드가 타깃이 됨 
- index, show 메소드가 있고 show에서만 실행하고 플 땐 except, only 같은 옵션 사용 

```ruby
before_action :메소드어쩌고, except: :index # index 빼고 실행 
before_action :메소드어쩌고, only: :show # show 만 실행 
```

#### 복수의 메소드 지정하고 싶을 때 
- index, show 일 때만 실행하고 싶을 때 
(심볼, 문자열 둘 다 가능) 
```ruby
before_action :메소드 어쩌고, only: [:index, :show]
before_action :메소드 어쩌고, only: ["index", "show"]

before_action :메소드 어쩌고, only: %i[index show]
before_action :메소드 어쩌고, only: %w[index show]
```

#### 특정 조건일 경우 해당 액션 실행 시 if, unless 옵션 사용 가능 

```ruby
before_action :메소드 어쩌고, if: :메소드명
```
#### proc
- proc 지정하는 것도 가능
- proc 사용시 메소드가 아닌 하나의 코드 지정 가능 
- 짧은 로직이라면 proc 사용하는 것이 가독성 높임 

```ruby
before_action :메소드어쩌고, if: proc{ user_signed_in? && current_user.id == 1 }

```

#### lambda

```ruby
before_action :메소드어쩌고, if: -> { user_signed_in? && current_user.id == 1 }
before_action :메소드어쩌고, if: proc{ user_signed_in? && current_user.id == 1 }

```

출처 : https://negabaro.github.io/archive/rails-before_action


