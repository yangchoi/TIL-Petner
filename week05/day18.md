### Rails Routing from the Outside in

#### Rails 라우터의 목적 
- Rails Router는 URL을 인식하고 컨트롤러의 액션, 혹은 rails webserver interface(Rack Application)에 URL들을 보내는 역할을 함
- 라우터는 또한 경로와 URL을 만들 수 있다.

##### 코드와 URL 연결하기 
- rails application이 요청을 받는다면 

```ruby
GET /patients/17
```
- 요청은 파라미너 안의 {id: '17'}이 들어있는 patients 컨트롤러의 show action을 전달받게 된다. 

##### 코드 안의 경로와 URL 만들기 
- 아래와 같이 수정하여 경로와 URL도 만들 수 있다. 

```ruby
get '/patients/:id', to: 'patients#show', as: 'patient'
```
- 그리고 컨트롤러 안의 코드도 아래와 같이 작성한다. 

```ruby
@patient = Patient.find(params[:id])
```

- 뷰도 아래와 같이 작성한다. 

```ruby
<%= link_to 'Patient Record', patient_path(@patient) %>
```

- 그러면 라우터가 /patients/17 이라는 경로를 만든다. 
- 이는 view의 불안정함을 줄이고 코드를 더 이해하기 쉽게 만든다. 

##### rails router 환경설정
application이나 엔진 안의 라우터는 config/routes.rb 파일에 있다. 

```ruby

Rails.application.routes.draw do
  resources :brands, only: [:index, :show] do
    resources :products, only: [:index, :show]
  end
 
  resource :basket, only: [:show, :update, :destroy]
 
  resolve("Basket") { route_for(:basket) }
end
```


#### Resrouce Routing
- Resource routing을 통해 index, show, new edit, create, update, destroy Action(RESTful API)에 대해<br>
별도의 Route 규칙을 선언하는 대신 한 줄의 코드로 RESTful API 규칙을 빠르게 선언할 수 있음 

##### 웹 resource
- 브라우저는 get, post, patch, put, delete와 같은 특정 HTTP 메서드를 사용하는 URL에 요청을 하여 페이지를 불러옴
- 각 메서드는 resource에서 작동하는 요청
- 리소스 경로는 여러 관련 요청을 단일 컨트롤러 작업에 매핑을 함
<br>
- rails application이 요청을 받을 때 

```ruby
DELETE /photos/17
```
이는 컨트롤러 액션에 매핑하기 위해 라우터에 요청

```ruby
resources :photos
```
- rails는 destroy action으로 파라미터 안에 {id:'17'}을 갖고 있는 photos 컨트롤러에 해당 작업을 요청


##### CRUD, 동사 및 동작
Rails에서 resourceful 라우터는 HTTP 동사들과 URL 사이를 컨트롤러 액션으로 매핑함 
- 관례상, 각 액션은 데이터베이스안의 특정한 crud 동작들을 매핑하기도 함
- 라우터 파일에 아래와 같은 하나의 코드가 있다면 

```ruby
resources :photos
```

Photos 컨트롤러에 매핑되는 7개의 다른 라우터들이 만들어짐

![image](https://user-images.githubusercontent.com/48708746/96073302-25d3cc80-0ee1-11eb-9b84-f167c2c43900.png)

- 라우터는 HTTP 동사와 인바운드 요청에 맞는 URL을 사용하기 때문에 4개의 URL들이 7개의 다른 액션에 매핑이 됨.



#### 라우터 찾기 

```cmd
rake routes|grep 찾고자하는 route명
```
