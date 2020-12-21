### rails 서버 환경 
- rails 서버 환경 : development, test, production  
- 기본적으로 주어진게 위의 3가지, 사용자가 원하면 추가적으로 만들어낼 수 있음 

#### development 
- 기본적으로 연습할 때 많이 쓰는 환경
- 서버 내 캐싱이 꺼져있나보니 퍼포먼스가 다소 떨어지는 편
- 코드 수정이 이루어지면 바로 본 서버에 적용됨
- 오류 접할 시 오류 페이지가 화럿ㅇ화 

#### test
- 자동화 테스트할 때 쓰이는 환경 
- 테스트에 최적화 되어 있다보니 서버 최적화에 있어서 성능에 초점을 둠 
- 명령어 한 번의 입력으로 모든 과정을 자동으로 거치며 오류 및 버그 찾아내고 보고함 

#### production 
- 실제 서비스 운영 때 쓰이는 env
- 보안, 성능 퍼포먼스에 초점 맞춰짐
- 코드 수정이 이루어져도 바로 본서버에 적용 안됨 ( 서버를 껐다가 켜야함 ) 
- 기본적으로 서버 오류 로그 미출력 및 public 폴더 저장소를 미지원
- 오류 접할 시 public 폴더 내에 있는 404, 500 에러 페이지로 이동



#### 환경설정
- 각 환경에 대해서는 config/environments 에서 개별적으로 설정 가능

#### db 설정
- 각 환경별로 db는 기본적으로 분리됨
- 각 환경에 따른 db 설정은 config/database.yml 에서 확인 가능 

![image](https://user-images.githubusercontent.com/48708746/102734373-047cda00-4383-11eb-84a4-5116ee47ef4e.png)


( 참고 : 
https://guides.rubyonrails.org/testing.html#the-test-environment 
https://community.openproject.com/topics/1613?board_id=9
https://kbs4674.tistory.com/18
)



### self 

current object 에 접속하기 위한 키워드 

내 코드가 인스턴스 메소드 안에 있을 때 self 는 클래스의 인스턴스. 
즉, self는 객체 


#### 예시 
```ruby 
def coffee
  puts self
end

coffee
#main
```
- 이 코드는 self 값을 출력할 coffee 메소드를 정의한 후에 호출함

##### 왜 main이 출력되나? 
- 왜냐하면 최상위 객체의 이름이기 때문. 
- 클래스 외부에서 정의된 모든 메서드를 찾을 수 있는 객체 

- 아래의 coffee 메소드와 같은 경우 
- 하지만, cat 이라는 이름의 클래스 안에 메소드를 정의 한다면 다음 self 는 cat 

```ruby 
class Cat 
  def meow
    puts self
  end
end

Cat.new.meow
# <Cat:0x7a14c5>
```
- 이 예시에서는 self의 값이 내가 어디서 쓰느냐에 따라 바뀐다는 것을 알 수 있음 


#### 그래서 self는 왜 유용한가? 

##### 명확성을 위한 self
- self의 실용적용돈는 메소드와 지역변수의 차이를 알 수 있다는 것 

- 변수와 메소드 이름이 같은 것은 좋은 생각은 아니나, 
- 만약 그런 상황에 있다면, self.method_name 으로 메소드를 부를 수 있을 것 

```ruby
class Example
  def do_something
    banana = "variable"
    
    puts banana
    puts self banana
    
  end
  
  def banana
    "method"
  end
  
end

Example.new.do_something

#"variable" > puts banana
# "method" > puts self.banana
```

- banana 라는 지역 변수가 있고, 그 안에 do_something 이라는 메소드도 있음
- 거기다 banana 라는 메소드도 있음

- 지역변수가 우선순위를 가져감 

- 이것이 만약 banana라는 메소드를 부르고 싶을 때, banana 변수값을 출력하는 대신 self를 쓰는 이유


(참고: https://www.rubyguides.com/2020/04/self-in-ruby/ ) 




 
