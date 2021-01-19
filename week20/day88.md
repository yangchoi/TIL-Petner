## Rails polymorphic association
- 다중 연관성 
- 하나의 모델이 여러개의 모델과 관계를 갖는 상태 

#### 예시 
##### 회원은 자신의 사진을 업로드 한다 
##### 물건을 소개하는 사진을 업로드 한다 

![image](https://user-images.githubusercontent.com/48708746/104992244-f7c3d280-5a63-11eb-83da-34b9ad475e41.png)
- User_Image와 Product_Image가 담고있는 정보가 매우 유사
- 이를 하나로 묶기 위해서 사용하는 것이 polymorphic assocation 
- 아래는 이를 하나로 묶은 후의 그림 

![image](https://user-images.githubusercontent.com/48708746/104992321-204bcc80-5a64-11eb-964e-2e1194b196e0.png)
- 여기서 생기는 문제는 어떻게 foreign_id a만을 이용해서 User 이미지인지 Product 이미지인지 구분하냐는 것. 
- 이를 알기 위해서는 하나의 정보가 필요, 또한 어떤 모델에 관련된 내용인지 담고있는 특정도 필요 
- 이를 적용한 다중 연관성을 위한 모델은 아래의 그림

![image](https://user-images.githubusercontent.com/48708746/104992423-5b4e0000-5a64-11eb-8be0-a988c62dd8e5.png)
- foreign_id와 더불어 foreign_type이 생성되어 User와 Product 를 구분해줌

#### Rails 에서 다중 연관성 설정 

##### Image 모델 
```ruby
class CreatePictures < ActiveRecord::Migrate
  def change
    create_table :pictures do |t|
      t.string :name
      t.integer :imageable_id
      t.string :imageable_type
      t.timestamps
    end
  end
end
```
- foreign_id와 foreign_type에 대해 특정 이름, imageable 을 붙여서 만들어줌

각각의 모델을 설정하면 다음과 같다 
```ruby
class Picture < ActiveRecord:;Base
  belongs_to :imageable, polymorphic: true
end

class Employee < ActiveRecord:;Base
  has_many :picture, as: :imageable
end

class Product < ActiveRecord::Base
  has_many :pictures, as: :imageable
end
```
- 다중 연관성을 위해 다중 연관을 갖는 모델( picture )에 연관관계를 사용할 이름은 belongs_to 로 정해줌(imageable) 
- 다중 연관성을 true로 설정해줌 (polymorphic: true) 
- 이와 연결된 모델(employee, product)에서는 as를 이용해 관계와 연결시켜줌 


https://guides.rubyonrails.org/association_basics.html#polymorphic-associations
