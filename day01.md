## 개발환경 (웹)

### DB 동기화 (임의로 만든 명령어)
```bash
$ rails sync:db
```

### rails server 실행
```bash
rails s -b 0.0.0.0
```

### DB 동기화 
#### DB 변경이 있을 시 로컬 적용 위해 사용 
```bash
rails db:migrate
```



## 공개키 

### 공개키 만들기
1. ssh 로 이동
```bash
cd .ssh 
```
2. 공개키 보기
```bash
cat id_rsa.pub  
```
> cat : 파일 내용 출력 

## 개발환경 (모바일)

### 로컬 서버 실행
실제 url을 테스트 서버로 바꿔줌
```bash
bin/development-server-ip-change.sh
```


### 로그 보기
로그값을 분석할 줄 알아야함
```bash
tail -f log/development.log 
```
## CSV 파일 import


### 리눅스 크론탭
윈도우의 스케줄러 같은 것으로 특정 시간에 특정 작업을 해야할 때 사용 <br>
(위에서는 csv 파일을 특정 시간에 한 번 씩 읽어 들이는데에 사용) <br> 

주기확인사이트: [주기확인사이트](https://crontab.guru/#)


### BDD (Behavior Driven Development)
테스트 주도 개발인 TDD를 근간으로 파생된 개발 방법으로 TDD에서 한 발 더 나아가 테스트 케이스 자체가 요구사양이 되도록 하는 개발 방법
BDD를 통해 개발을 하면 테스트 메소드 이름을 "이 클래스가 어떤 행위를 해야한다" 라는 식의 문장으로 작성해 행위에 대한 테스트에 집중할 수 있음

### 루비 
#### Question mark (물음표)
본 메소드는 true false 값을 리턴한다 <br>

#### Exclamation mark (느낌표)
본 메소드를 쓰면 해당 객체 내용이 바뀐다 <br>
이 객체를 다른 곳에서 사용할 경우 예상치 못한 일이 일어날 수 있다 (dangerous method)



