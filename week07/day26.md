### model 생성 

```bash
rails g model journal_like status:string journal:references admin_user:references

```
- journal_like 라는 모델을 만드는데, 그 안에는 <br>
string 타입의 status가 있고, journal과 admin_user 테이블을 참조(references)한다. (id는 알아서 만들어 준다)
- 위의 명령문 입력시 model및 테스트 코드 파일 spec이 생성된다. 

### 테스트 
- 모델을 건들일 때는 테스트 코드를 꼭 작성해준다. 

journal_like_spec.rb

```ruby
require 'rails_helper'

RSpec.describe JournalLike, type: :model do
  describe "associations" do
    it { should belong_to(:journal) }
    it { should belong_to(:admin_user) }
  end
end

```
> 참조한 journal, admin_user가 잘 오는지 확인 
