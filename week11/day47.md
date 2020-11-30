### 오늘 한 일 
- image resize
https://aws.amazon.com/ko/blogs/compute/resize-images-on-the-fly-with-amazon-s3-aws-lambda-and-amazon-api-gateway/

_______




### namespance
- 모든 식별자(변수, 함수, 형식 등의 이름)가 고유하도록 보장하는 코드 영역 

### 멱등성


### active record query interface 
- active record는 데이터베이스에서 query를 수행하며, mysql, mariadb, postgresql 및 sqlite를 포함한 <br>
대부분의 데이터베이스 시스템과 호환됨 

#### retrieving objects from the database
- 데이터베이스에서 개체 검색하기 위해 active record가 사용하는 다양한 finder method
 
 ```ruby 
find
create_with
distinct
eager_load
extending
from
group
having
includes
joins
left_outer_joins
limit
lock
none
offset
order
preload
readonly
references
reorder
reverse_order
select
distinct
where
 
 ```
 
 - where 및 group과 같은 collection을 반환하는 finder method는 ActiveRecord::Relation의 instance를 반환
 - find 및 first와 같은 단일 엔티티를 찾는 method는 model의 단일 instance 반환
 
 
 #### Model.find(options) 
 - 제공된 옵션을 동등한 sql 쿼리로 변환
 - sql 쿼리 시작하고 데이터베이스에서 해당 결과 검색
 - 모든 결과 행에 대해 적절한 모델의 동등한 루비 객체를 인스턴스화 
 - after_find 실행 후 after_initialize 콜백 (있는 경우) 실행 
 
 
### 단일 라인 객체 탐색

1. find
- 기본키 기반의 id 값 입력받아 데이터 탐색 
- 여러개의 데이터 찾아내볼 수도 있음

2. take
- 순서없이 랜덤으로 데이터 검색
- 데이터가 없고 예외가 발생하지 않으면 take method는 nil qksghks
- take 메소드에 숫자 인수 전달해 갯수에 맞는 결과 반환할 수도 있음

3. first
- 기본키로 정렬된 첫번째 데이터 찾음

4. last
- 기본키로 정렬된 마지막 데이터 찾음

5. find_by 
- 탐색조건과 일치하는 결과 중 첫번째 레코드만을 찾음

### retrieving multiple objects in batches

1. find_each 
- 모델이 가진 데이터 탐색 후, 각 레코드의 객체 데이터를 블록 내에 개별적(반복적) 생성
- 일괄적으로 탐색 후, 각 레코드에 블록 생성

2. find_in_batches
- 모든 roecord branch 를 검색하기 때문에 find_each와 비슷하나 <br>
  개별적으로가 아니라 모델의 배열로 블록에 batch 생성 


#### conditions
- where 메소드를 사용하면 sql문의 where 부분과 동일하게 조건 지정 가능 

* sql injection
- orm을 이용해 아래와 같은 방법으로 데이터 탐색 가능

```ruby
b_title = "안녕하세요"
Bulletin.where("bulletins.title LIKE '%#{b_title}%'")
```
> bulletins 테이블에서 안녕하세요 문구각 포함된 데이터 찾기 

> 하지만 위의 방법은 sql 보안에 취약함

> true 를 반환하는 문법을 통해 모든 데이터 결과가 콘솔에 노출

> 따라서 아래와 같은 방법 추천

```ruby
b_title = 안녕하세요
Bulletin.where("bulletins.title LIKE ?", '%#{b_title}%')
```
> 조건절과 문자값을 따로 분리 

> 위의 방법을 통해 sql injection 방지 


#### array conditions

______


### rails security

#### 세션 
- 사용자가 애플리케이션과 상호작용하는 동안 애플리케이션이 사용자 별 상태를 유지토록 함 (로그인 유지 등) 
- 대부분의 애플리케이션은 애플리케이션과 상호 작용하는 사용자 상태를 추적
- 그것이 장바구니 내용이거나 현재 로그인한 사용자의 id 일수 있음
- 이러한 사용자 별 상태는 세션에 저장됨
- rails 는 애플리케이션에 액세스하는 각 사용자에게 세션 객체 제공
- 사용자에게 이미 활성 세션이 있는 경우, rails는 기존 세션 사용. 그렇지 않으면 새 세션 생성 

##### 세션 하이재킹 
- 사용자의 세션 id를 도용하면 공격자가 피해자의 이름으로 웹 애플리케이션 사용 가능
- 많은 웹 애플리케이션은 인증 시스템이 있고 사요앚가 사용자 이름, 암호를 제공하면 웹 애플리케이션을 확인하고 해당 사용자 id를 세션 해시에 저장 > 이때부터 세션 유효 
- 모든 요청에서 애플리케이션은 새로운 인증없이 세션의 사용자 id로 식별되는 사용자를 로드함 
- 쿠키의 세션 id는 세션을 식별 
- 쿠키는 웹 응용 프로그램에 대한 임시 인증 역할

참고 : https://guides.rubyonrails.org/security.html#sql-injection

_____

#### hash conditions
- active record 사용시, 조건문의 가독성을 높일 수 있는 hash 조건을 전달할 수 있음
- 해시 조건 사용시 정규화하려는 key와 값이 포함된 hash 전달 
> hash 조건에서는 동등성, 범위 및 subset 검사만

#### not conditions
- where.not

#### or conditions

##### ordering


### Eager loading associations
- 가능한 적은 쿼리를 사용해 레코드를 조회하는 메커니즘

1. SQL N+1 problme
- active record 를 사용하면 조회될 모든 연결을 사전에 미리 정할 수 있음 
- 매번 결과를 보여줄 때 마다 sql을 탐색하는 비효율적인 탐색결과를 보여줄 때 <br>
includes 를 사용
- includes 를 사용하면 active records는 지정된 모든 연결이 가능한 최소한의 쿼리 수를 통해 조회도도록 할 수 있음

2. eager loading mulitple associations
- activer record 사용시 includes 사용해 array, hash, nested of array/hash 를 사용해 단일 find 호출과 관계없이 많은 수의 연관을 조회할 수 있음

- eager_loads 는 includes 메소드를 통해서도 표현할 수 있음 

 


