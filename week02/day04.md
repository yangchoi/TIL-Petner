#### 할 일 
- admin petner 페이지에 의뢰수행건수 컬럼 내림차순, 오름차순 만들기 
- admin 의뢰 페이지에 UI 수정 

#### rails tutorial 따라하기
https://www.railstutorial.org/book/beginning

#### 웹페이지에  hello world 띄워보기 
- 컨트롤러에 가서 render function을 이용해 "hello world" 를 HTML에 리턴시킨다
app/controllers/application_ controller.rb
```ruby
class ApplicationController < ActionController::Base

  def hello
    render html: "hello, world!"
  end
end
```
이 다음으로 rails에게 직접 디폴트 페이지 대신 위의 페이지를 띄우겠다는 것을 알려야한다. <br>
그러기 위해서는 rails router를 수정해야한다.<br> 
rails router는 controller 앞에 위치하며 브라우저로부터의 요청을 어디로 보낼지 결정한다. <br>
<br>
특히 여기서는 root URL을 사용하는 페이지를 결정하는 root route, 즉 디폴트 페이지를 바꾸고자 한다. <br>
root URL은 슬래쉬 뒤에 아무것도 안오는 http://www.example.com/ 과 같은 형태이다
<br>

rails의 route 파일은 config/routes.rb 이며, 아래와 같은 형태로 root route를 정의할 수 있다. 
```ruby
root 'controller_name#action_name'
```

위의 hello world를 적용시키기 위해서는 controller 이름인 application과 action 이름인 hello를 사용해 아래와 같이 적으면 된다 <br>
config/routes.rb
```ruby
Rails.application.routes.draw do
  root 'application#hello'
end
```
