### rspec
- ruby 프로그램을 지정하고 테스트하는데에 사용되는 BDD 도구 

** BDD & TDD 
둘다 거의 차이는 없음 
- BDD(Behaviour-driven development) : 비즈니스 요구사항에 집중해 테스트 케이스 개발, 좀 더 자연어에 가깝게 작성 
- TDD(Test-driven development) : 테스트 자체에 집중하여 개발 

(참고 : https://blog.aliencube.org/ko/2014/04/02/differences-between-bdd-and-tdd/)

- 자연어에 가깝게 작성하는 BDD 테스트 케이스 중 하나인 user story 기법 
  어떤 비즈니스 요구사항을 바탕으로 시나리오를 만들고 그렇게 만들어진 시나리오를 바탕으로 유닛테스트 작성 > BDD 를 적용한 소프트웨어 개발 


** 간단한 RSpec 예제

-greeter,rb

```ruby
class Greeter
  def greet
    "hello world"
  end
end
```

- spec/greeter_spec.rb

```ruby
require_relative '../greeter.rb' 

RSpec.describe Greeter do 
  describe '#greet' do # describe 블록은 중첩 가능, 이 경우 greet 메서드가 Greet 클래스의 일부임을 전달함 
            # #greet의 #은 greet가 인스턴스 메소드(클래스 메소드의 경우 . ) 임을 보여주는 규칙 
            # RSpec 은 문자열을 전혀 해석하지 않으므로 다른 문자열을 사용하거나 describe 블록을 완전히 생략할 수 있음 
    it "says hello" do  # 예제 블록 
      expect(Greeter.new.greet).to eq("hello world") # 테스트의 기대 (기대 충족시 테스트 통과, 아니면 실패)  
    end
  end
end
```


