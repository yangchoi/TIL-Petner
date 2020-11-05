### 오늘 한 일 
- welocome에 좋아요 2개 이상 받은 예쁜 돌봄 사진 띄우기 (미완) : 내일 안엔 끝내기 

#### 다음으로 해야할 일 
- 예쁜 돌봄 사진의 사진들을 페이지당 1장에서 한 30장 정도로 해서 스크롤 내려 보게 만들기 

### 막히는 부분 
- JournalLike 테이블을 역할을 정확하게 생각하지 않고, JournalLike 테이블에서 attachment_id를 끌어와 이미지를 띄우려고 했음
- 그러나 JournalLike 테이블은 like counting 역할 만을 하는 테이블로 둬야만 했음. 
- image 를 끌어오는 방법에 대해 아직 개념이 모호함 

### 해결법 
- active_storage_attachment에 journal_like 컬럼을 새로 생성
- 컬럼에 JournalLike 에서 like 2개 이상 받은 값들을 보내준다. 
- active_storage_attachment에 있는 그 값들로 이미지 url을 받아 보여주면 됨 

### 추가적 공부가 필요한 부분 
- rails model의 전체적인 부분 
- model의 active record association (https://rubykr.github.io/rails_guides/association_basics.html)
- active record migration
- active record reversible 

___________________


### 활성 레코드 관계 (Active Record Association)
- 관계 : 활성 레코드 모델들간의 연관 
- 관련 > 매크로 스타일의 호출로 구현되어 있어서 선언만 하면 모델들 사이에서 생성됨 
<br>

- belongs_to B > B 객체의 예에 속해있다. 
- has_one B > B 객체의 예를 하나 갖는다 
- has_many B > B 객체의 예를 여러개 갖는다 
- has_many :through B > B 객체의 예를 통해 여러개 갖는다 
- has_one :through B > B 객체의 예를 통해서 하나 갖는다 
- has_and_belongs_to_many B > B 객체의 예에 속해 있으면서 동시에 B 객체의 에를 많이 갖는다. 


### rails sync:assets


### Active Record Migration 
- migration 은 active record의 기능으로 데이터베이스 스키마의 기능을 확대하도록 도와줌 

#### reversible 
- migration 파일에 대해 테이블 up/down 여부 따라 테이블을 어떻게 재설정할지 결정하는 기능 
- change 대신 up/down 메서드 사용 
- up : 스키마에 대한 변환방법 기술 
- down : up 메서드에 대해 행해진 변환을 역행하는 방법을 기술 
(up 후 down 실행 시 스키마가 변경되지 않도록 해야함 > up에서 테이블을 만들었으면 Down에서는 삭제해야함)

```ruby
class  ExampleMigration  <  ActiveRecord :: Migration  [ 5.0 ] 
  def  up 
    create_table  : distributors  do  | t | 
      t . string  : zipcode 
    end

    # CHECK 제약 조건을 추가 
    execute  << - SQL
      ALTER TABLE distributors
        ADD CONSTRAINT zipchk
        CHECK (char_length (zipcode) = 5);
    SQL

    add_column  : users ,  : home_page_url ,  : string 
    rename_column  : users ,  : email ,  : email_address 
  end

  def  down 
    rename_column  : users ,  : email_address ,  : email 
    remove_column  : users ,  : home_page_url

    execute  << - SQL
      ALTER TABLE distributors
        DROP CONSTRAINT zipchk
    SQL

    drop_table  : distributors 
  end 
end
```

https://railsguides.jp/active_record_migrations.html#reversible%E3%82%92%E4%BD%BF%E3%81%86


### 의문 
- 왜 change column 이 아닌 reversible 을 사용할까.. 

#### 읽어볼 글 (레일즈의 polymorphic association)
https://medium.com/@Fred.it/%EB%B2%88%EC%97%AD-%EB%A0%88%EC%9D%BC%EC%A6%88%EC%9D%98-polymorphic-association-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-d13ee23695ab

