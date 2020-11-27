### 오늘 한 일 
- active storage blob의 사진 크기를 줄여서 페이지 로딩 속도를 높이는 것 

#### 작업 방향 
- active storage blob 의 사진 크기를 사이드킥을 이용해 정기적으로 줄이기 
- 해당 파일들을 active_storage_blob_resize에 업데이트 
- 크기 조정이 된 active_storage_blob_resize 사진들을 예쁜 돌봄 사진 페이지에 넣기 

______




### sidekiq
- 비동기 작업 처리를 위해 사용 
- background job 및 이를 쉽게 해줌 (선입선출) 
> background job : 서버가 돌아가는 작업이 이루어지는 동시에 무언가의 작업이 이루어지는 것 
- ruby로 작성된 오픈 소스 작업 스케쥴러 
- 등록된 작업을 레디스 큐에 저장해놓고 워커들에게 가져가서 처리하는 방식 
- 사이드킥 젬은 redis-server에 의존되는 방식이므로 redis-server 설치해주어야함 

#### sidekiq 작업
1. worker 생성
2. schedule.yml 에 worker 등록
- perform 메소드 만들어줌
- include Sidekiq::Worker 
3. controller에서 worker에 따른 perform_at, perform_sync 적용 

______


### aws lambda 
https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/welcome.html
- 서버를 프로비저닝하거나 관리하지 ㅇ낳아도 코드를 실행할 수 있게 해주는 컴퓨팅 서비스 
> 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해두었다가 필요시 시스템을 즉시 사용할 수 있는 상태로 미리 준비해두는 것 


### aws s3
- aws에서 제공하는 온라인 스토리지 웹 서비스 




