### 오늘 한 일
- 업로드 실패된 이미지 view에서 제외시키기 

#### 시도한 방법
- attachment에서 blod_id로 연결된 blob 테이블에서 filename이 FullSizeRender.jpg 인 파일들을 where.not으로 제외시키기 
- 처음엔 위의 방법으로 filename을 where.not 한 blob 을 attachment 에 join 하려고 했음
- 잘안됨 ( 생각해보면 좀 말이 안되는 상황인게 느껴지는데 정확히 왜 안되는지는 설명이 잘 안됨..) 
- 그래서 아예 blob 테이블을 따로 불러와 거기서 해당 filename을 where 함 
- 그렇게 따로 추출한 blob에서 id만 따로 빼와 attachment에서 해당 id들을 where.not으로 제외 시켜 blob을 join하지 않고 해결 

________



### Image Magic
- 그래픽 이미지를 새로 만들거나 고치는데에 사용되는 자유-오픈소스 소프트웨어 

### minimagick 
- 루비의 gem 
- rails에서 Image magic을 사용하기 위해 사용 
- mini magick에서 Image magic으로 명령을 전달 
