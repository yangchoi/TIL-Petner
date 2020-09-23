#### controller와 route
route에서 resource를 지정하면 controller에서 그 resource들을 조작한다. 
controller에서 수행하는 자원 조작들은 resource의 관점에서 크게 비파괴적, 파괴적 액션으로 나눌 수 있다.
이 액션들을 erb와 연결된다. 

- 비파괴적
1. new > form 관련 액션 
2. show
3. index
4. edit
| show, index는 get 형태로 동작

- 파괴적 
1. create
2. update
3. destroy
| create는 post, update는 put, destroy 는 delete 
| destory는 삭제할 타겟이 있다는 점에서 put과 다르다 


#### REST ( Representational State Transfer)
<br>
<br>

#### debugging
binding.pry
<br>
<br>

#### 배포 툴
카피스트라노
- 배포 명령어 
```bash
bundle exec cap production deploy
```
<br>
<br>

#### git pull upstream master = glum 
#### git checkout master = gcm
<br>
<br>

#### ruby 와 rails
ruby는 웹, 임베디드 어디에서나 사용할 수 있게 만들어졌고 rails는 웹 전용 프레임워크이다. <br>
따라서 웹과 관련된 문법은 rails syntax... 로 검색하면 되고, <br>
그냥 루비 문법인 경우에는 ruby syntax... 로 검색하면 되는 것. 

#### ruby의 암묵지
ruby의 문법 중에 아래와 같은 문법이 있다. 
```ruby
{:created_at => week_range}
```
그런데 아래의 경우도 똑같이 통용된다.
```ruby
{:created_at: week_range}
```
아래의 문법이 더 사용하기 쉽기 때문에 사람들은 아래의 문법을 더 많이 쓴다. 
ruby는 이러한 암묵지가 많다고 한다..
<br>
<br>

#### dig 
```bash
h = {}
> {}
h[:a] = {}
> {}
h [:b] = {}
> {}
h
> {:a=>{}, :b=>{}}
h[:a][:b]={}
>{}
h[:a][:b][:c] = {}
> {}
h
> {:a=>{:b=>{:c=>{}}}, :b=>{}}
h[:b][:d]={}
> {}
h[:a][:b][:c][:d] = 'a' 
> "a"
h.dig :a
> {:b=>{:c=>{:d=>"a"}}}
h.dig :a, :b 
> {:c => {:d => "a"}}
h.dig :b, :d
> {}
h [:a][:b][:c]
> {:d => "a"}
h
> {:a => {:b => {:c=> {:d => "a" }}}, :b => {:d => {}}}
h[:d] 
> nill
h [:d][:b]
> not found
h.dig :d, :b
> nill 
```

```

