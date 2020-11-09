### 오늘 한 일 
- staffs/journal_like에서 좋아요 2개 이상 받은 돌봄 사진들 welcome에 띄우기 (미완) 

#### 막히는 부분 
- attachment에서 like_count 2개 이상인 레코드의 id를 가져와 journal_like와 같은 attachment_id면 띄우려고 했는데 잘 안됨 
- where절을 잘못 쓰는 바람에 여러 id들 중에 딱 한 id만 가져와 반복문에서 돌아가는 것으로 보임 
- 또 현재 journal_card에서 journal.attachment_id를 image_tag 로 띄우려고 했는데 그 작업도 진행이 되지 않음.(unless를 통해 확인해 보니 attachment_id가 아예 nil인 상태)
- attachment_id 를 image_tag에 넣으면 사진으로 띄워질 것이라 생각했는데 아닌 것 같아 다른 방법을 생각해 봐야 함 

#### 현재 진행중인 방향 
- welcome_controller에서 journal_likes_count가 2개 이상인 데이터를 attachment에서 가져와 id만 따로 빼내어 변수에 담음 (journal_likes_count_id)
- 해당 변수를 기준으로 journal_like에서 where 절을 통해 journal_likes_count_id와 같은 attachment_id를 @journal_likes로 지정해서 view에서 반복문 돌림 

___________________________________________________


### has_one_attached
: 하나의 연관관계와 모델 사이의 관계를 지정함

### has_many_attached
: 여러 연관관계와 모델 사이의 관계를 지정함

### unless
: if 문과 반대로, 조건이 false일 때 실행되는 조건문 


____________________

### change_column 대신 reversible을 사용하는 이유 
- reversible은 기존 테이블에 끼어든다는 느낌이 강하므로 기존에 있던 데이터를 그대로 사용하는 것이 가능
- add_column은 아예 새로운 것을 생성하는 느낌
- journal_likes_count 의 경우 reversible을 해서 journal_likes 데이터로 count를 할 필요가 있었기 때문에 reversible을 사용 
