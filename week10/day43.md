### 오늘 할 일 
- 좋아요 기능 수정 (ajax) 
- 좋아요 카운트를 counter_cache로 수정 



#### 통제변인
어떤 코드가 안돌아갈 경우,<br>
어떤 코드를 건들면 안되는지 (통제변인인지)<br>
어떤 코드가 건들여도 괜찮은 코드인지 파악하고 해당 코드를 조금씩 변경해가면서 테스트 해본다.

_____________


### orm에서의 active record
#### active record 의 특징 
- model과 Data를 나타냄
- model간의 연관성을 나타냄
- 모델이 데이터베이스에 쓰이기 전에 모델의 유효성을 검증
- 객체지향 방식으로 작업 진행 

### Convention over configuration(COC) in active record
#### Controller 이름은 복수명, Model 이름은 단수명으로 표현하는 것에 대해 
- model과 table을 생성할 때 active record는 이 둘의 관계를 고려해 매핑을 함
- model의 이름에 대해 pluralize(복수화)되어 table 이름이 결정됨 
- 이와 같이 rails의 정해진 룰에 따라 model명은 단수, 테이블 명은 복수가 됨 

#### schema conventions 
- active record에서는 테이블 컬럼 내 이름을 지을 때 컬럼의 목적에 맞게 자동으로 지어짐

#### polymorphic assications
- 데이터 조회시 타 테이블을 참조해 데이터를 조회해야하는 경우 보통 외래키를 활용한 방법이 많이 알려짐 
- 게시판에 댓글 기능을 구현한다고 가정
- 만약 외래키 기능을 사용한다면 댓글 기능이 필요한 테이블 n개에 따른 댓글 테이블도 n개를 만들어야함 
- 이는 비효율적이며 테이블 낭비
- polymorphic 방식을 이용하면 테이블 연계가 몇개가 되던 간에 댓글 테이블은 하나만 있으면 됨 
- 서로 다른 model 이름을 가진 페이지에서 댓글이 작성되면 댓글이 쓰여진 model과 해당 model의 id가 기록됨 
- 댓글 모델은 다형성 model 이다 보니 타 테이블과의 연관 관계를 설정한 후 어떤 컬럼 이름을 기준으로 데이터들을 저장힐지나 다형성 여부와 같은 설정을 해줘야함 
- 댓글은 comment 라는 이름으로 가정하고, commentable_type, commentable_id 컬럼에 데이터를 저장할 것이므로 <br>
   belongs_to:commentable, polymorphic: true 를 줘야함 
```ruby
class Comment < ApplicationRecord
  belongs_to :commentable, polymorphic: true
end
```
> comments에 polymorhphic 옵션을 주는 이유는 comments는 하나의 모델에 대해서만 belongs_to 관계를 가질 수 있고, <br>
  2개 이상의 model 에는 belongs_to 를 가질 수 없기 때문 
  
> belongs_to : 어떤 모델의 데이터에 종속되어 있다 (belongs_to에 지목된 모델명은 단수 명)


#### cached counter
- 댓글이 달릴 때 마다 자동으로 댓글을 counter 하는 예시 

