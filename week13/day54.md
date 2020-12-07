### module
- 필요에 따라 로드할 수 있도록 만들어진 파일 
- 모듈은 메서드와 상수를 namespace로 분리하는 역할을 함 
- class와 유사해보이지만 모듈에는 인스턴스를 만들 수 없고 하위클래스를 만들 수 없음 

greeting.rb
```ruby
module Greeting
  def Greeting.welcome()
    return "hi"
  end
end
```
main.rb
```ruby
require './greeting'
puts Greeting.welcome()
```

> require 는 모듈을 로드할 때 사용하는 명령 <br>
> greeting은 불러오려고 하는 모듈의 이름, 모듈의 이름은 확장자를 제외한 파일명 사용 <br>

### module function 
- 모듈 함수란 private 인스턴스 메소드면서 모듈의 싱글톤 메소드인 메소드 
- 서브루틴이 이용할 목적인 메서드는 모듈함수로 정의할 수 있음 


____

# frozen_string_literal 
- 프로젝트에서 메모리를 절약하고 가비지 컬렉터의 압력을 분산해 성능 향상을 도와줌 

https://medium.com/@taekani/ruby-on-rails-frozen-string-literal-f1c77fbda006


____

### open_graph (og) 
- 각종 sns 에서 링크 공유시 보이는 썸네일, 제목, 설명들이 뜨는 것 

____


#### yield , content_for
