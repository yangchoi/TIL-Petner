https://github.com/pureugong/rails-style-guide/blob/master/README-koKR.md

#### 라우팅 
- RESTful 리소스에 더 많은 액션을 추가할 필요가 있다면, memeber/collection 라우트 사용 
- 여러 memeber/collection 라우트를 정의해야한다면 블록 구문
- 액티브 레코드 모델간의 관계를 더 분명하게 표현하기 위해 중첩 라우트 사용 

```ruby 
class Post < ActiveRecord::Base
  has_many :comments
end

class Comments < ActiveRecord::Base
  belongs_to :post
end

#routes.rb
resources :posts do 
  resources :comments
end
```

#### 컨트롤러 
- 컨트롤러는 단지 뷰 레이어를 위한 데이터를 전달하는 역할
- 어떠한 비즈니스 로직을 포함해서도 안됨
- 모든 비즈니스 로직은 마땅히 모델 안에서 구현되어야함 
- 각 컨트롤러 액션은 (원칙적으로는) 초기 검색과 생성을 제외하고 단 하나의 메소드만을 호출해야함 
- 하나의 컨트롤러와 하나의 뷰 사이에서 두개 이상의 인스턴스 변수들 공유하지 않음 



### self 
- 현재 또는 기본 객체를 가리킴
- 클래스 안에서 쓰면 현재 클래스를 말함
- 메서드 안에서 쓰이면 현재 메서드를 사용하고 있는 객체를 말함
- 특히 클래스 메서드 표현할 때 많이 쓰임 

```ruby
class Test
  def self.print
    puts "Test"
  end
end
```
Test.print 라고 실행해도 self 를 이용해 Test 가리키고 있으므로 
결과는 성공적으로 "Test" 출력

```ruby
class Test
  def print
    puts "Test"
  end
end
```
위의 코드에서 Test.print 를 한다면 
private method "print" called for Test:Class(NoMethodError) 

즉, self 를 사용하여 만든 메소드는 클래스메소드가 되는 것이고 
self 를 사용하지 않는 메소드는 인스턴스 메소드가 되어 클래스를 인스턴스로 만든 후에 사용할 수 있는 것 

self 는 현재 클래스 이외에도 현재 모듈 가리킴

```ruby
module Test
  def self.print
    puts self
  end
end

#print => Test
```



________________________________________________________________________________________________________________________


#### 오리타입 
- 특정 클래스에 종속되지 않은 퍼블릭 인터페이스 
- 여러 클래스를 가로지르는 이런 인터페이스는 클래스에 대한 값비싼 의존을 메시지에 대한 부드러운 의존으로 대치시킴


