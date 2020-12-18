### cache 
가장 최근의 의뢰를 기준으로 페이지를 만들기 때문에 <br>
한 번 만들어진 페이지는 캐싱작업을 통해 보존이 필요함 

- 캐시란 한 번 읽어온 데이터를 임의의 공간에 저장해 다음에 읽을 때는 빠르게 결과값을 받을 수 있게 도와주는 공간 
- 캐싱은 응용 프로그램 성능을 향상시키는데에 효과적인 방법
- 캐싱을 통해 단일 데이터베이스가 있는 단일 서버에서 실행되는 여러개의 동시 사용자 로드를 유지할 수 있음 


https://guides.rubyonrails.org/caching_with_rails.html

___



### redis 
- 서비스를 처음 운영할 때는 web-was-db 의 전형적인 3티어 구조 
- 그러나 사용자가 늘면 db에 무리가 가기 시작 
- db는 데이터를 물리 디스크에 직접 쓰기 때문에 서버에 문제가 발생함. 죽더라도 데이터 손실은 없음
- 하지만 transaction 마다 디스크에 접근해야하기 때문에 부하가 많아지면 상당히 느려짐 

- 따라서 캐시 서버 도입 검토하게 됨 

![image](https://user-images.githubusercontent.com/48708746/102588901-82599f00-4151-11eb-9460-b8383b53f0ed.png)

- 클라이언트가 웺서버에 요청 보내면 웹서버는 데이터를 db에서 가져오기 전에 cache 에 데이터가 있는지 확인
- cache에 데이터 있으면 데이터를 db에 요청하지 않고 바로바로 클라이언트에 반환 >> cache hit 

- 반대로 cache 서버에 데이터 없으면 db에 해당 데이터 욫어 >> cache miss 


https://brunch.co.kr/@jehovah/20


#### redis 란? 
- 캐시서버로 쓰임
- 키-값 기반의 인-메모리 데이터 저장소 
- 키-값 기반이기 때문에 쿼리를 따로 적어줄 필요 없이 결과를 바로 가져올 수 있음 


https://www.youtube.com/watch?v=mPB2CZiAkKM

____


#### limit 
- 검색할 레코드 수 지정 

https://kbs4674.tistory.com/164?category=876767


