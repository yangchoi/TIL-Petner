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

