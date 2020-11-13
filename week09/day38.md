### ruby mixin
- mixin : 모듈이 추가 동작 및 정보를 클래스에 혼합하는데에 사용될 시 
- mixin 사용시 코드를 다시 작성하지 않고도 클래스를 사용자 정의할 수 있음 

#### Ruby의 module
- 루비에서 모듈은 "메서드와 상수의 집합"
- 모듈은 클래스와 달리 instantiate(인스턴스화) 될 수 없음
- 모듈의 주 목적은 그 안에서 정의한 메서드를 다양한 클래스에 include, prepend, extend 를 통해 mixin해서 재사용하는 것
- mixin 해서 사용하는 메서드 : 인스턴스 메서드 
- 객체 생성없이 모듈 자체에서 호출하는 메서드 : 모듈 메서드 
- 모듈 메서드는 mixin 해도 사용할 수 없음 

```ruby
module Mymodule
  const = "my const"
  
  def self.module_method
    "module_method is called
  end
  
  def instance_method
    "instance_method is called"
  end
end
```

```ruby
irb > Mymodule::const
>> "my const"

irb > Mymodule.module_method
>> "module_method is called"

irb > Mymodule.new.instance_method
>> NoMethodError
```

#### Ruby의 Ancestors
- 루비에서는 클래스가 생성될 때 ancestors 배열에 클래스 조상의 목록을 저장해둠
- ancestors에는 이 클래스가 상속받는 모든 클래스. 자기 자신, 그리고 include, prepend를 통해 mixin된 모듈들이 포함됨 

- 클래스의 인스턴스 메서드 호출시 ancestors 배열의 앞에서부터 메서드 정의 찾음
- 상속 개념과 비슷하게 메서드 정의를 찾지 못하면 다음 조상에게서 찾는 식
- 즉, 둘 이상의 조상들이 같은 이름의 메서드를 정의하고 있다면 더 가까운 조상에게 정의된 메서드 실행 

```ruby
irb > String.acenstors 
# => [String, Comparable, Object, Kernel, BasicObject]
irb > String.included_modules 
# => [Comparable, Kernel]

irb > "foo".upcase 
# => "FOO"
irb > "foo".object_id 
# => 70264361086420

irb > String.instance_method(:upcase) 
# => #<UnboundMethod: String#upcase>
irb > String.instance_method(:object_id) 
# => #<UnboundMethod: String(Kernel)#object_id>
```


#### Ruby에서의 mixin

#### include
- 모듈에 정의된 메서드를 클래스에 재사용하는 방법 (가장 쉽고 ㄴ러리 알려진 방법)
- 클래스 정의 시 어떤 모듈을 include하면 그 모듈은 ancestors 배열 상에서 부모 클래스 앞에 위치하게 됨 
- 따라서 메서드 이름이 같다면 include 된 모듈이 부모 클래스보다 우선순위를 가짐 

```ruby
module MyModule
  def log
    "log by MyModule"
  end
end

class BaseClass
  def log
    "log by BaseClass"
  end
end

class MyClass < BaseClass
  include MyModule
end
```

```ruby
irb > MyClass.ancestors
# => [MyClass, MyModule, BaseClass, Object, Kernel, BasicObject]
irb > MyClass.instance_method(:log)
# => #<UnboundMethod: MyClass(MyModule)#log>
irb> MyClass.new.log
# => log by MyModule
```
>> MyClass의 조상인 BaseClass의 log가 아닌 include 한 MyModule의 include가 나옴 


#### prepend
