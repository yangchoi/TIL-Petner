### ruby on rails 철학
1. don't repeat your self (dry)
- 코드를 반복적으로 쓰지마라 (코드의 재활용성)
- 똑같은 역할을 하는 메소드가 반복적으로 쓰이지 않도록 

2. Convention Over Configuration(COC)
- 설정보단 규약
- 최대한 rails에서 정해진 규칙을 활용한다 
- 대표적인 예로 MVC 패턴에 있어 Model과 Controller의 이름을 정의함에 있어 다음 규칙이 Rails 내에서 지켜지고 있음
> Hello 라는 이름의 Controller와 Model 명칭을 정한다면 <br>
> Controller : hello_controller.rb <br>
> Model : hello.rb <br>
위와 같이 이름을 명시하면 Controller에서 알아서 class와 매칭이 이루어지고, model 에서는 테이블과 매칭이 이루어짐


### gemfile, gemfile.lock
- gemfile : 공통, 각 environment 별 설치해야하는 라이브러리(gem)에 대해 기록이 되어있음
- gemfile.lock : gem 이 설치될 때 마다 설치된 gem의 버전 별로 dependency 관계에 대해 정의되어 있음


### rails 내에서 controller와 view 생성을 통해 홈페이지에 hello world를 띄우는 과정
- rails 내 홈페이지에 접속시 
1. 홈페이지 접속
2. 미들웨어(rack)에서 요청 받음
3. 라우터에서 요청에 대한 Controller#Action 찾아냄
4. Controller에서 내부적으로 요청 처리하고 view 에 결과 전송
5. 요청에 대한 결과를 view에서 유저에게 보여줌


### rack?
- config.ru는 서버 실행에 대한 script 내용에 담겨져 있는 파일
- 서버 통신은 rack이라는 기술을 통해 이뤄짐
- ruby on rails 라는 application에서 서버에 요청을 하고 <br> 
  응답에 대해 rack은 apllication과 서버의 중계인으로서 '미들웨어' 역할을 함 
- rack은 중간에 소통을 통해 요청/응답을 처리해 서로에게 전해줄 수 있음
- rack은 라우터 연결에 대해서도 관여할 수 있음
- ruby on rails는 컨트롤러와 라우터와의 통신에 있어 내부적으로 action dispatcher 기술이 쓰이는데, <br>
  action dispatcher 내부 구성에 있어서도 rack에서 비롯됨
  
  (rack에 대해 : https://www.joinc.co.kr/w/Site/Ruby/Rack)
  

### 라우터 규칙
- root : 루트도메인으로 웹사이트에 접속시 어떤 페이지에 보여줄지에 대한 정의를 함
(root 문법은 get 메소드로 정의, url 정의와는 다르게 Controller#Action으로서 정의함)

- get : get 메소드 기반의 url 정의 문법, http://도메인/welcome/index 접속시 <br>
  app/controllers/welcome_controller.rb 내의 index 액션을 둘러본 후, <br>
  app/views/welcome/index.html.erb의 결과물을 보여줌

- resources : 자동으로 rest api 문법에 의거해 method/url 정의가 이루어짐



### Controller 와 view
> contriller 와 view는 기본적으로 서로 종속 관계로 되어있음
(controller 이름은 복수명으로)
- controller 내의 action들은 곧 view의 파일명이 됨
- 만약 내가 edit 이라는 action을 controller에 생성한다면 view 쪽에도 그대로 edit 이라는 파일이 있어야 템플릿 에러가 나지 않음


### model 과 database table 
1. model 생성 및 migrate 개념
(model 명은 단수)
- 모델 생성시 데이터베이스를 제어 및 관계를 정의하는 model, migrate, 테스트코드 파일이 생성됨
> 테이블은 model 명의 복수형으로 생성됨 <br>
> migrate 파일에 별다른 설정 없을 시, 기본적으로 id, created_at, updated_at 컬럼이 자동 생성됨 <br>
> 데이터 타입을 따로 명시하지 않을 경우 기본적으로 string으로 정의됨 <br>
> 일부 테이블 명은 복수형으로 표현될 때 s로 표현되지 않고 형태가 변형될 수 있음 ( mouse > mice )


### active record
- ruby on rails 에서 지원되는 모듈 중 하나, database의 전반적인 부분을 담당
- 객체 관계 맵핑
- ruby on rails에서 데이터를 다룰 때 있어서는 sql을 직접적으로 사용해 데이터베이스를 제어하진 않음
- orm 등을 통해 표현함
- 즉, orm과 데이터베이스 간의 언어를 해석하고 연결을 도와주는 맵핑 


______


### joins 과 includes 의 차이 
- joins로 인해 lazy loading(N+1) 문제가 발생할 경우 
- 이런 문제를 해결하기 위해 includes 메소드를 사용한다 

https://jongjineee.github.io/2019/07/18/includes_joins.html


