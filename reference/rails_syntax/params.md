### Strong parameters

참고 : https://api.rubyonrails.org/classes/ActionController/StrongParameters.html


```ruby
class PeopleController < ActionController::Base
  def create
    Person.create(person_params)
  end
  
  def update
    redirect_to current_account.people.find(params[:id]),tap { |person| person.update!(person_params) }
  end
  
  private
    def person_params
      params.require(:person).permit(:name, :age)
    end
end
```

strong parameters 가 있는 accepted_nested_attributes_for 를 쓰기 위해서는 **nested_attributes**가 허가되어야함

### nested_attributes ( nested : 중첩 )

참고 : https://api.rubyonrails.org/classes/ActiveRecord/NestedAttributes/ClassMethods.html
nested_attributes 는 부모와 관련된 레코드들을 attributes에 저장할 수 있게 허가함 <br>

attribute writer는 association 후에 적음 <br>
고로 두 메소드가 모델에 추가된 것

- author_attributes=(attributes)
- pages_attributes=(attributes)


```ruby
class Book < ActiveRecord::Base
  has_one :author
  has_many :pages
  
  accepts_nested_attributes_for :author, :pages
end
```




