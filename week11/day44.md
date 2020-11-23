###  레일즈의 polymorphic association
- ActiveRecord의 polymorphic association (다형성 관계)


```ruby
class Person < ActiveRecord::Base
  has_one :address, :as => :addressable
end

class Company < ActiveRecord::Base
  has_one :addres, as => :addressable
end

class Address < ActiveRecord::Base
  belongs_to :addressable, :polymorphic => true
end

```
위의 코드는 기본적으로 Address 클래스가 임의의 모델과 belongs_to 관계를 맺게 함 <br>
위의 코드를 아래의 코드와 같다고 가정해본다. 

```ruby
class Address < ActiveRecord::Base
  belongs_to :person
  belongs_to :company 
end
```
그러면 이 address 테이블은 모든 외래키를 갖게 됨 <br>
하지만 하나의 address는 하나의 person, compnay에 속하는 것이지 둘 모두에 속할수는 없음 <br>
따러서 이 외래키들 중 오직 하나의 값을 취해야함 

#### 현재 레일즈 공식 문서에서는 has_one, has_many에 대한 as 키워드 매개 변수를 참조해 "다형성 인터페이스" 지정 

다형성 인터페이스를 생각할 때 루비의 << 메시지 라인처럼 생각 <br>
이 메시지를 배열, 문자열, IO 스트림등과 같은 여러가지 다른 객체에게로 보낼 수 있음<br>
그 객체들은 모두 이 메시지를 수신할 때 무엇을 해야하는지 이미 알고 있기 때문 <br>

<br>

<< 를 모든 다른 클래스가 구현하고 있는 일종의 인터페이스라고 생각 

<br>

Person과 Company가 Address 를 상속하도록 예시를 만듦 
```ruby
class Address < ActiveRecord::Base
end
class Person < Address
end
class Compnay < Address 
end
```

이제 Person 이나 Company 는 Address가 아니기 때문에 다형성 인터페이스 대신 수퍼클래스 이름을 사용할 수 있음

```ruby
class Addressable < ActiveRecord::Base
end
class Person < Addressable
end
class Company < Addressable
end
```

Person과 Company 객체는 addressable 임 <br>
이제 Address 클래스는 아래와 같이 됨

```ruby
class Addressable < ActiveRecord::Base
  has_one :address
end
```


https://medium.com/@Fred.it/%EB%B2%88%EC%97%AD-%EB%A0%88%EC%9D%BC%EC%A6%88%EC%9D%98-polymorphic-association-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-d13ee23695ab 의 글을 정리 
