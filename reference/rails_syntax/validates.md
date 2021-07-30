### validates

유효성 검사 
```ruby

class Person < ApplicationRecord
  validates :name, presence: true
end


irb > Person.create(name: "yang").valid?
-> true

irb > Person.create(name: nil).valid
-> false
```
