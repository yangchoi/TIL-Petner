### rails 와 redis

![image](https://user-images.githubusercontent.com/48708746/103192411-ee8b8e00-491b-11eb-9424-c9d15d84d341.png)

- redis로 서버의 메모르에 데이터 저장 

- 최초에 웹서버 접속시엔 db 서버를 참조, db 서버를 참조하면서 메모리에 key-value 로 이루어진 데이터 저장하게 됨 
- 이후엔 key 참조하며 value 불러오는 방식


##### key-value 
- key와 value는 한 페어로 구성되어 db를 하나하나 탐색하는 것이 아닌 사진에 redis 메모리에 key-value 를 등록한 값을 통해 조회하는 방식 ex) 색인


##### redis로 얻을 수 있는 것 
-redis 적용을 통해 데이터 불러오는 속도가 빨라짐

#### redis cache 
- string, list, set, hash 등 다양한 방식으로 저장될 수 있음
- 더 나아가 확률적 알고리즘으로 불리는 하이퍼로그로그 방식으로 redis key를 저장할 수 있음
cf) 하이퍼로그로그 : unique item에 대한 카운팅을 하는 알고리즘, 정확한 수의 파악보다는 약n개 라는 개략적인 수의 파악에 쓰임
(참고 : https://d2.naver.com/helloworld/711301)

(참고 : https://kbs4674.tistory.com/121)



