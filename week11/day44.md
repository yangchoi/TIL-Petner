###  레일즈의 polymorphic association
- ActiveRecord의 polymorphic association (다형성 관계)
- 하나의 모델이 다른 여러개의 모델과 관계를 갖는 상태 

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
이제 Person과 company는 address와 has_one 관게를 가짐 <br>
이들은 이것을 addressable로부터 상속하고 있고 다형성관계는 없음 
<br>
그런데 레일즈는 단일 테이블 상속(STI)를 함 <br>
만일 person과 company 사이에 공통된 부분이 거의 없다고 가정했을 때 단일 테이블 상속을 사용한다면 <br>
어떤 행의 데이터가 person을 나타낼 시 company를 나타내는 수많은 속성 컬럼이 비어있을 것이고 그 반대 경우도 마찬가지일 것 <br>

<br>

시스템에서 addressable의 종류가 더 많아질 수록 테이블은 더 거대해짐 <br>
상속은 상태가 아니라 행동에 관한 것이고 데이터베이스에 대해 생각하지 않고 모델링을 한다면 addressable 클래스를 사용했을 것 <br>
<br>
결론적으로 단일테이블 상속은 기본적으로 동작이 아닌 공통 상태가 많은 클래스의 상속 계층을 매핑하는 방법 
<br>
상속 계층 구조를 관계형 데이터베이스에 매핑하는 다른 방법이 있음 <br>
일반적으로 세가지 정도가 있지만 레일즈는 가장 간단한 단일테이블 상속만을 제공
_____

1. 단일 테이블 상속 : 전체 계층 구조는 해당 행의 클래스 이름을 가지는 여분의 칼럼들(type)이 있는 단일 테이블로 매핑됨
2. 구체 클래스 당 하나의 테이블 : 각각 구체 클래스는 그 자신에 속한 하나의 테이블을 가짐 <br>
                           수퍼 클래스는 추상 클래스이며 자신의 테이블은 가지지 않음 <br>
                           수퍼 클래스의 모든 공통 상태는 각 서브 클래스 테이블에 복제됨 
3. 클래스 당 하나의 테이블 : 계층의 각 클래스는 자체 테이블을 가짐. 

_____


만약 Person, Company, addressable 이 클래스들의 각각 자신만의 테이블로 매핑한다면? 
```sql 
addressables (id)
people (id, name, age, height, weight, addressable_id)
companies (id, size, established_date, addressable_id)
addresses (id, street, city, state, addressable_id)
```
상위 클래스로 addressable을 사용해 상속을 모델링하는 계층 구조 얻음 <br>
이제 모든 하위 클래스를 자체 테이블에 넣을 필요 없음 <br>
이렇게 단일테이블 상속을 없앰 <br>
데이터베이스에서 person 을 읽어올 때, 우리는 addressable_id 로 person의 상위 클래스 테이블 addressables를 조인함, 그리고 person 의 address를 읽으려면 addressable_id로 addressable_id로 addresses를 조인 <br>

<br>

이렇게 다형성 연관성을 제거하고 상속으로 대체 <br>

<br>

그런데 만약 people과 company 들에 tag 기능을 추가한다고 한다면 <br>
레일즈의 플러그인인 acts_as_taggable을 사용할 수도 있지만 지금은 사용하지 않고 예시를 들어봄 <br>


<br>

Tangible 클래스를 사용해본다 <br>
그런데 루비는 다중 상속을 허용하지 않고 java와 같은 인터페이스를 갖고 있지 않음 <br>
대신 루비는 모듈을 사용 <br>

Addressable 을 클래스가 아닌 모듈로 모델링해야함 <br>

```ruby
module Addressable
end
module Tangible
end 

class Person < ActiveRecord::Base
	include Addressable
	include Tangible
end 

class Company < ActiveRecord::Base
	include Addressable
	include Tangible
end 
```
이제 addresses와 companies는 모두 주소 지정이 가능하고 태그 지정이 가능토록 개선됨 <br>

```ruby
module Addressable
	has_one :address
end
```
레일즈는 위와 같이 불가 

```ruby
module Addressable
	def self.included(klazz)	# klazz 는 이 module 이 include된 class 객체 
		klazz.class_eval do 
			has_one :address		
		end
	end
end
```

이제 각 클래스들은 address와 has_one 관계를 가지는 addressable 모듈을 include 하고 있음  <br>

이때 데이터베이스는 아래와 같음 

```sql
addresses (id, street, city, state, person_id, company_id)
```
Address 는 person 및 company를 동시에 belongs_to 관계로 가질 수 없음 <br>
#### 다형성 관계가 필요 

```ruby
class Address < ActiveRecord::Base
	belongs_to :addressable, :polymorphic => true 
end

class Tagging < ActiveRecord::Base
	belongs_to :tangible, :polymorphic => true
end 
```

> 아래의 글을 정리 <br>
https://medium.com/@Fred.it/%EB%B2%88%EC%97%AD-%EB%A0%88%EC%9D%BC%EC%A6%88%EC%9D%98-polymorphic-association-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-d13ee23695ab
<br>
https://destiny738.tistory.com/545

______

#### Ruby on rails 기본 제공 관계
- belongs_to : 외래키 관계 설정 
- has_one : 1:x 관계
- has_many : n:x 관계 
- has_many :through [model class] : n:x 관계 설정하면서 model 클래스를 통해 연결된 다른 정보 얻어올 수 있음
- has_one :through [model class] : 1:x 관계를 설정하면서 model 클래스를 통해 연결된 다른 정보 얻어올 수 있음
- has_and_belongs_to_many : 직접적으로 n:n 관계 설정 

