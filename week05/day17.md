#### MVC 패턴

![image](https://user-images.githubusercontent.com/48708746/95933271-1da85e00-0e09-11eb-82e7-be51be4f7733.png)

- Rails 응용프로그램과 통신 할 때, 브라우저는 Web 서버에 request(요청) 전송하고 이 요청을 처리하는 역할을 함<br>
- 그리고 이 요청 처리는 Rails 컨트롤러에 전달됨 
- 이 요청 처리를 전달받은 컨트롤러는 즉시 view 를 생성해 HTML을 브라우저에 보냄
- 동적사이트는 일반적으로 컨트롤러(사용자등) 사이트 요소를 나타내며 <br>
  데이터베이스와의 통신을 담당하고 있는 ruby의 객체인 model과 상호 작용
- 모델을 호출한 후 컨트롤러는 뷰를 렌더링해 완성된 web 페이지를 HTML로 브라우저에 반환 

#### MVC 의 동작

![image](https://user-images.githubusercontent.com/48708746/95935256-c8bb1680-0e0d-11eb-9ba9-cd9228301f85.png)


1. 브라우저에 /users 라는 URL 요청을 Rails 서버로 전송
2. /users 요청은 Rails 라우팅 장치 (라우터)에 의해 Users 컨트롤러의 index 에 할당
3. index 작업이 실행되고 거기서 User 모델에 User.all 요청 
4. User 모델은 요청받은 모든 사용자를 데이터베이스에서 꺼냄
5. 데이터베이스에서 검색한 사용자 목록을 User 모델에서 컨트롤러에 반환 
6. Users 컨트롤러는 사용자 목록을 @users 변수에 저장하고 index 뷰에 전달
7. index 뷰를 시작하고 ERB(embedded ruby : 루비의 view로 HTML에 포함된 Ruby 코드) 를 실행해 HTML 생성(렌더링) 
8. 컨트롤러는 뷰에서 생성된 HTML을 받아 브라우저에 반환 

- 사용자가 요청한 URL을 Users 자원으로 사용되는 컨트롤러 액션 코드는 아래와 같다 
config/routes.rb
```ruby
Rails . application . routes . draw do
resources : users root 'application # hello ' end 
```
이러한 매핑 코드는 Rails 라우팅 설정파일 (config/routes.rb) 에 사용 

#### 라우터
- 컨트롤러와 브라우저 사이에 배치되어 브라우저의 요청을 컨트롤러에 배분(라우팅) 함

##### 라우팅 수정 
- 서버의 루트 URL에 엑세스하면 기본 페이지 대신 사용자 목록 표시하도록 수정하기 
(/ 방문시 /users 열리게 만들기) 
<br>

```ruby
root 'application # hello' 
```
위와 같이 하면 루트 액세스시 Application 컨트롤러의 hello 액션에 라우팅되도록 되어 있음 <br>
이번 경우엔 Users 컨트롤러의 index 액션을 사용하고자 함.
- 루트에서 users 라우팅 추가 
config/routes.rb

```ruby
Rails . application  . routes . draw do 
  resources :users
root 'users # index' end
```

#### rails db:migrate
- 데이터베이스 마이그레이션 (migrate)
- 데이터베이스 업데이트, 새로운 데이터 모델 생성 

#### 컨트롤러의 골격 
app/controllers/users_controller.rb
 ```
- user 페이지 생성했다고 가정 <br>
/users : index <br>
/users/1 : show >> id=1 사용자를 표시하는 페이지 <br>
/users/new : new >> 새 사용자 만들 페이지 <br>
/users/1/edit : edit >> id = 1 사용자 편집 페이지 <br>
