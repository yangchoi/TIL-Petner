### rake
- unix 에서 소스코드 실행을 위해 프로그램을 빌드할 때 주로 make 라는 도구를 사용함
- rake 는 ruby버전의 make 
- rails 4 이전에서는 rails 명령이 아닌 rake 명령을 사용했음 


### rails mvc (again..)
![image](https://user-images.githubusercontent.com/48708746/99472215-84321600-298b-11eb-904e-c8e1595112f1.png)

1. 브라우저에서 /users 라는 url 요청을 rails 서버로 전송
2. /users 요청은 rails 라우터에 의해 users 컨트롤러의 index 액션에 할당
3. index 작업이 실행되고 거기에서 user 모델에 User.all 실행
4. User 모델은 모든 사용자를 데이터베이스에서 꺼냄
5. 데이터베이스에서 검색한 사용자 목록을 User 모델에서 컨트롤러에 반환
6. Users 컨트롤러는 사용자의 목록을 @users 변수에 저장하고 index 뷰에 전달
7. index 뷰 시작하고 erb를 실행해 html 생성(렌더링)
8. 컨트롤러는 뷰에서 생성도니 html을 받아 브라우저에 반환 

> 사용자가 요청된 url을 Users 자원으로 사용되는 컨트롤러 액션에 대한 코드는 rails 라우팅 설정파일(config/routes.rb) 에서 설정 

### REST 아키텍처 
- 인터넷 자체나 web 애플리케이션 등의 분산/네트워크화된 시스템이나 응용 프로그램을 구축하기 위한 아키텍쳐 스타일 
- 응용 프로그램 구성 요소를 자원으로 모델링하는 것 
- 이러한 자원은 관계형 데이터베이스의 CRUD 조작과 4개의 기본적인 http request 메소드(post/get/patch/delete)를 모두 지원하고 있음 
- rails 개발자는 restful 스타일로 작성해야 컨트롤러와 액션 결정이 쉬워짐 

#### Users 자원이 제공하는 restful 경로 
![image](https://user-images.githubusercontent.com/48708746/99473021-1b4b9d80-298d-11eb-865b-3562ae81aa9b.png)


### ActionController::Base
- rails의 action pack 이라는 라이브러리가 제공하는 컨트롤러의 기본 클래스 
- rails 컨트롤러는 반드시 ApplicationController를 계승하고 있기 때문에 application 컨트롤러에 정의된 규칙은 응용 프로그램의 모든 작업에 반영됨 
- 따라서 어떤 컨트롤러도 모델 객체의 조작이나 들어오는 http request 필터링 뷰를 html로 출력하는 등 다양한 기능을 수행할 수 있게 됨 




(참고 : https://railstutorial.jp/chapters/toy_app?version=5.1#code-demo_user_model)
