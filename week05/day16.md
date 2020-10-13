#### SEO(search engine optimization, 검색엔진최적화)
- 검색 결과를 최상단에 노출하게 만드는 기법 
- ad 는 해당 사이트에 돈을 주어 맨 상단에 노출되지만 SEO의 경우 키워드나 특정 검색어를 웹사이트에 적절히 배치해 <br> 
  검색에 보다 쉽게 걸리게 만드는 것 
  
#### Open Graph Protocol
- 페이스북이 정의한 메타 태그 프로토콜
- metadata를 <head>에 추가하면 페이스북bot이 해당 metadata를 읽어서 표시해줄 수 있다
  
  1. og:title  전달할 제목
  2. og:type 전달할 데이터의 video나 image website등의 타입
  3. og:image 전달할 이미지의 주소
  4. og:url 전달할 사이트 주소 
  
  https://ogp.me/
  
#### Rails layout
- layout false > layout djqtdma 
- layout nil > 부모 layout으로 resetting

- staffs_controller.rb
```ruby
class StaffsController < ActionController::Base
  ...
  layout 'dashboard'
  ...
end
```

layout
  ㄴ dashboard.html.erb
  

#### controller 
> ActionController::Base
- Action controller는 web request의 코어
- action 은 controller에서 public method로 정의된다
(public method는 자동으로 rails routes를 통해 web server에 접속가능)

- 자연스레 ApplicationController는 ActionController::Base를 상속받는다. 
- 다른 controller는 ApplicationController를 상속받는다.

  다른 controller < ApplicationController < ActionController::Base


#### ex
- BooksController
```ruby
class BooksController < ApplicationController
end
```
- routes.rb
```ruby
resources :books
```

- app/views/books/index.html.erb
```html
<h1>book example</h1>
```
- 내가 /books로 갈 때 rails가 자동으로 rendering

- BooksController >>>rendering>>> app/views/books/index.html.erb
```ruby
class BooksController < ApplicationController
  def index
    @books = Book.all
  end
end
```
- rails가 controller의 view 위치 안의 action_name.html.erb(여기서는 index.html.erb)템플릿을 찾고 렌더링한다 
- 만약 view에서 모든 책의 매개변수를 보고 싶다면 ERB 템플릿에서 @books.all 로 books 를 불러온다 

#### @템플릿변수
- 컨트롤러에서 연산된 결과를 view에서 보여주기 위함 <br>
(컨트롤러는 하나의 클래스)


