### 진행중인 작업 
https://github.com/rails/rails/pull/37901/files
위의 링크를 따라 image resize 하는 작업 중 

#### 막히는 부분 
- 현재 펫트너 홈페이지 레일즈 버전이 6.0 이므로 해당 링크의 코드(6.1) 적용시 후에 버전업 시 충돌 위험이 있다하여 손대기 조금 어려운 상황
- 따라서 이름을 조금씩 바꿔서 코드를 작성했는데 적용이 잘 안됨
- 계획은 attachment 를 불러오는 controller에서 variant resize 를 이용해서 사이즈를 줄인 다음에 view 에 뿌려주는 방식을 생각을 했으나 variant 메소드를 찾지 못함
- variant 메소드를 사용할 수 있는 방향으로 찾으면 resize 할 수 있을 것 같음 

_____



#### attach
- 최신 레코드와 함께 주어진 attachment과 Associate(연관)하고 db에 저장


____


### link rel="canonical" 
- 페이지 중복을 없애줌 

