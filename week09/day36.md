### 오늘 한 일 
- welcome 페이지에 journal_like 띄우기(미완)

#### 안되는 부분 
- scope로 image_attachment를 Join 해서 welcome에 뿌려줄 journal_likes 에 넣었는데, 작동이 안됨 
- 해당 scope 입력하면 전체가 다 나오지 않음. 
- image_attachment를 join 시켜서 attachment_id로 사진을 찾아내면 될 것 같은데 이 부분이 잘 안됨 
- model 부분에서 뭔가 놓치고 있는 듯함
- controller 에서 해결할 수 없는 이유는, journal_card 를 반복문으로 돌리기 때문에 controller 쪽에서 journal_likes와 함께 사진을 view로 보내줘야함
- 따로 보내주면 여러장을 journal_likes 의 id에 맞게 보낼 수가 없음 (내 생각) 
- 뭐가 문젤까? model을 더 공부하면 되는 부분인가? 
- 아직 ruby 스타일을 잘 모르겠다 
- rails 역시 .. 

__________


### activestorage blob
#### active storage 동작 원리 
1. active storage에 이미지 파일 업로드 
2. blob 
3. disk 

#### blob? 
- 파일에 대한 정보를 가지고 있음
- 원본 파일(disk)로 redirect 시켜주는 역할을 가짐 (중간 경유지 역할)
- 웹페이지에서는 이미 url이 변하지 않는 것이 확인되는데, 이는 blob에 대한 정보를 참고하기 때문
(blob은 원본인 disk 정보를 가리킴)
- 각 파일 마다 고유의 blob key 값을 가지고 있으며 이 값은 변하지 않음 

#### disk? 
- blob의 key 값을 참고해서 원본 파일을 사용자에게 보여줌
- disk에 file key 및 암호화 키를 가지고 있음 
- disk 의 file key 값은 변하지 않고 암호화 키는 특정 시간 간격으로 변화 
(암호화 키 변경은 config/application.rb에서 설정 가능)
- 이미지 파일에 있어 원본 url 변경은 결국 암호화 키 변경 때문에 발생 


_____


### join 정리 

#### left (outer) join
- 왼쪽 테이블을 기준으로 오른쪽 테이블의 부가정보가 추가되는 조인 
#### inner join
- 두 테이블을 합친 후, 공통 데이터만 보여짐
#### full out join
- 두 테이블을 합친 후, 보여지는 모든 경우의 수에 따른 결과를 보여줌


_____

### 로그 규칙 
#### Log4j (왼쪽으로 갈 수록 Highter levels, 오른쪽으로 갈 수록 lower levels)
fetal/error/warn/info/debug/trace
(rails는 trace 지원 안함)



_____

### seo 
- 오늘회 사이트 참고 



### ci/cd
https://devuna.tistory.com/56
