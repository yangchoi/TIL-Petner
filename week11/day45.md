### migration reversible 
> reversible : migration 파일에 대해 테이블 up(migrate)/down(revert) 여부에 따라 <br>
              테이블을 어떻게 재설정할지 결정하는 기능(함수)
1. up : migration 파일에 적힌 db 명세기록을 토대로 데이터베이스 서버에 적용
2. down : migration 파일에 적힌 db 명세기록을 토대로 데이터베이스 서버에서 제거(롤백) 

#### 이미 migration 이 진행된 파일에서 수정(속성변경 등)을 하면 적용이 안됨, 따로 migration 파일을 추가해야함 
> rails g migration change_[컬럼이름]_to_[테이블이름]

### active record and referential integrity 
- 데이터베이스가 아닌 모델에 사용되는 active record는 후에 참조무결성에 있어서도 많은 보안을 해낼 수 있음 
> 참조 무결성 : 데이터베이스의 한 곳에서 어떤 특정값으로 참조를 하는 정보가 데이터베이스의 다른 곳에 반드시 존재하여아하는 원칙 


### DSL(Domain Specific Language)
- dsl : 특정 도메인(산업분야등 특정 영역)에 특화된 언어 
- 문제 영역 해결에는 그 영역의 언어를 전제로 둬야하며 그곳에서 프로그래밍 솔루션을 내는 것이 중요 
- 특정 영역 문제 해결에는 그 영역에 맞는 특화된 도구를 사용하자 

1. 내부 dsl 
- 호스트 언어 구문을 이용해 자체적으로 의존하는 무언가를 만드는 경우 
- Lisp, Ruby..

2. 외부 dsl
- 호스트 언어와 다른 언어에서 생성된 dsl 
- gui 도구를 제공해줌 
- java, c++,,

#### dsl 장단점 

1. 장점 
- 반복 제거, 비슷한 처리 코드는 자동 생성 (템플릿) 
- 프로그래밍 코드 양이 적고 가독성 높음 

2. 단점
- 설계 어렵
- 잘 설계되지 않으면 어려운 코드 됨 
- 하위 호환성 유지 

> Ruby 의 activerecord, validations, rake, rspec, capistrano, cucumber 가 Dsl <br>
> Java의 경우 Maven 등등 ..

참고 : https://unabated.tistory.com/entry/DSLDomain-Specific-Language-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0

_____



### active record validations intro 
- 데이터베이스가 데이터에 저장되기 전 active record를 통해 유효성 검사를 하는 과정 

#### validations overview
- 유효성 검사(validate)는 데이터가 저장되기 전 validate 조건에 맞는 데이터에 대해서만 저장이 되도록 도와줌 
- 데이터베이스의 조건 중 참조 무결성 조건도 지켜나갈 수 있다는 장점이 있음 

- 유효성 검사를 하는 메소드 
```ruby
create
create!
save
save!
update
update!

```

> ! 는 bang 이라고 부름 


#### valid? and invalid? 
- active record의 객체를 통해 데이터가 저장되기 전, validation 측에서 데이터 검증이 일어나고 조건에 맞지 않는 데이터일 경우 에러메시지 남김 
- valid? 메서드가 작동된 후 유효성 검사에서 false가 리턴될 시 에러메시지를 내부적으로 확인 가능 

##### new 메소드를 통해서는 에러메시지 확인이 안됨
> create 와 다르게 인스턴스화에 있어서 바로 transaction 과정을 거쳐 데이터베이스에 저장 시키는 메소드가 아니다 보니 에러메시지 반환하지 않음

#### errors[] 
- 객체 내 컬럼이 유효성 검사를 할 때 에러를 발견했다면 errors[:attribute] 메소드를 통해 알아낼 수 있음 
- 에러의 원인을 알고 싶다면 detail[:attribute]


### validation helpers
- 전부 모델 옆에 붙는 옵션들 

#### acceptance
- 컬럼내 불린 여부에 대해 검사 
- 모델에 명시된 컬럼이 nil 혹은 true 형태여야만 데이터 저장됨 

#### validates_assocaited
- 2개의 모델 관계에서 validates_associated 옵션이 있는 모델은<br>
  다른 연계 모델에서 데이터 저장시 유효성 조건에 맞게 저장됐는지 검사 (has_many, belongs_to 관계 구분은 상관없음) 
> 단, 하나의 모델에 대해서만 validates_associated 옵션을 줘야함 
  그렇지 않을 시 무한 루프 에러 발생 

#### confirmation
- 모델을 통해 데이터를 저장할 때 재입력을 통해 확인이 필요할 시 사용되는 검사 
- 본 유효성 검사는 strong parameter과 연계되어 사용되어야 함 

#### exclusive 
- 모델을 통해 데이터 저장할 때 사전에 validate에 설정한 예약어가 없어야함 
- 만약 예약어+다른 단어 조합으로 사용할 경우 유효성 검사(valid?) 에서는 true

#### inclusion
- exclusive와는 반대로 내용 속에 사전에 validate 설정한 예약어가 있어야함 
- 예약어+다른 단어 조합으로 사용할 경우 유효성 검사에서는 false

#### format
- parmas[:attribute] 데이터에서 정규식 패턴을 분석해서 정규식 조건에 맞는 단어인지 확인 
- with 에 명시된 조건이 아닐 시 insert 안됨 

#### length 
- 모델을 통해 데이터를 저장할 때 글자 수 검사, 조건에 맞을 시 insert

#### numericality 
- 숫자 및 소수 (음수포함)이 있는지 검사, 조건이 맞을 경우 insert

#### presence 
- form 안에 내용이 존재하는지 검사 

#### inverse_of
- 외래키로 연계된 두 테이블 관계에서 데이터 참조 시, 사전에 메모리에 저장시켜 놓아 메모리 최적화에 도움을 줌 
- 외래키 이름과 모델 이름이 같으면 따로 설정해줄 필요 없음 

#### absence 
- 데이터 저장 시 지목된 컬럼에 내용이 없어야함 

#### uniqueness
- 데이터 입력될 시 해당 옵션이 걸린 컬럼이 테이블에서 유일한 값인지 확인 

#### validates_with 

.. 기타 등등


참고 : https://kbs4674.tistory.com/161?category=876767


_____


### actove record associations 
- 어떤 관게의 연관관계는 인간에겐 당연한 상식이나 컴퓨터에게는 당연하지 않으므로 직접 명시를 해주어야함
- 두개 이상 모델(테이블) 간 관계 정의법은? 

#### assocations
- rails 에서 연결은 두개의 active record model 간의 연결
- 모델 사이의 연관은 왜 필요한가? 
- 코드 작업을 더 간단하고 쉽게 할 수 있기 때문

- active record associatioin을 사용하면 두 모델 사이에 관련이 있음으로 선언해 <br>
다른 연계 모델 간의 작업을 간소화 할 수 있음

#### rails의 연관관계 총 6개 
```ruby
belongs_to
has_one
has_many
has_many :through
has_one :through
has_and_belongs_to_many

```
- 연관은 macro-style호출을 사용해 구현되므로 모델에 기능을 선언적으로 추가할 수 있음
- 한 모델이 다른 모델에 속한다고 선언하면 레일즈에 두 모델 인스턴스 간의 기본키-외래키 정보를 유지하도록 지시하고 모델에 여러가지 메소드 추가 가능 


1. belongs_to : 1:1연결
- belongs_to 관계는 단수 표현을 사용해야함 
- 복수 사용시 에러, 레일즈가 자동으로 클래스명을 관계 명에서 유추함 

2. has_one : 1:1 이나 조금 다름
- 이 연관은 모델의 각 인스턴스가 다른 모델의 한 인스턴스를 포함하거나 소유함을 나타냄 

3. has_many : 1:m 
- 이 연관은 모델의 각 인스턴스에 다른 model의 인스턴스가 0개 이상 있음을 나타냄 
- 이 연관을 선언할 때는 모델명을 복수형으로 지정 

4. has_many :through : m:m
- 다대다 연결

5. has_one :through : 1:1
- 다른 모델과 1:1 연결 
- 모델이 제 3 모델을 거쳐서 달느 모델의 인스턴스와 일치될 수 있음을 나타냄 

6. has_and_belongs_to_many  : n:m
- 개입된 모델 없이 다른 모델과 직접 다대다 연결

#### 두 모델간 1:1 관계를 설정하려면 belongd_to를 하나에 추가하고, has_one을 다른 모델에 추가해야함 <br>
여기서 belongs_to와 has_one의 배치는 아래와 같음
- 외래키 존재하는 곳과 데이터의 실제 의미에 대해서도 고려해야함
- has_one 관계는 무언가가 나를 가리키고 있다고 말함 
"supplier 업체를 소유하고 있다"

#### 모델 간 m:n 관계를 선언하는 방법 2가지 
1. has_one_belongs_to_many 사용 

2. has_many :through 
- 조인 모델을 통해 간접적으로 연결 만들어냄 

- 독립적 엔티티로 작업해야하는 경우엔 has_many :through 관계 설정
- 관계 모델을 사용해 작업을 수행할 필요가 없는 경우 has_and_belongs_to_many 관계 설정 (이 경우 데이터베이스에 join 테이블을 생성해야함)
- join 모델에서 유효성 검사, 콜백 또는 추가 속성이 필요한 경우 has_many :through 사용 


### polymorphic assiciations 
- 기존 associations 에서 더 나아간 변형 
- polymorphic associations을 사용하면 모델이 단일 연관에서 둘 이상 다른 모델에 속할 수 있음 

- polymorphic 방식으로 선언하는 방법

```ruby
class Picture < ApplicationRecord
  belongs_to :imageable, polymorphic: true
end
 
class Employee < ApplicationRecord
  has_many :pictures, as: :imageable
end
 
class Product < ApplicationRecord
  has_many :pictures, as: :imageable
end
```
- 위와 같이 선언시 employee model 또는 product model에 picture model 이 속하게 됨 

- polymorphic 에서 belongs_to 선언은 다른 모델이 사용할 수 있는 인터페이스 설정하는 것으로 생각할 수 있음 
- employee model의 인스턴스에서 @employee.pictures를 통해 employee에 종속된 pictures 들 검색 가능 
- 역시 @product.pictures 통해서도 데이터 검색 가능 

- picture model의 인스턴스 있는 경우 @picture.imageble을 통해 부모에게 접근 가능
- 위의 작업을 수행하기 위해선 모델에서 polymorphic 인터페이스를 선언하는 외래키 컬럼과 타입 컬럼 모두 선언해야함 

