### rails asset pipeline

#### rails asset pipeline
- 자바스크립트와 css 를 합치고 압축할 수 있는 프레임워크 제공 
- coffeescript, sass, erb와 같은 타 컴파일 언어 이용가능하게 해줌 
- spockets-rails gem 에서 가져오로 수 있음

#### 주요기능
##### 병합
- JS, CSS를 하나의 파일로 합쳐줌
- PRODUCTION에서 레일즈는 MD5지문(fingerprint)를 각 파일 이름에 넣어서 브라우저가 이 팡르들을 캐시할 수 있게 함. 
- 파일 내용이 바뀔 때마다 지문 바뀌므로 내용이 바뀔때만 브라우저가 새로운 파일 받아옴 

- 이는 웹페이지 렌더링으로 브라우저 요청 수를 줄일 수 있고 따라서 로딩 시간을 줄여주는 효과가 있음


##### 압축
- asset 파일 내에서 불필요한 스페이스, 코멘트 제거해줌
- 이는 파일 크기를 줄여주고 asset 로딩 시간을 줄여줌 


##### 사전컴파일 
- coffee script, sass 등과 같은 상위 레벨 언어를 css 파일로 컴파일 해줌 


#### asset 경로 
- app/assets 개발자가 만든 image, javascript, stylesheet 파일들이 위치하는 디렉토리 
- lib/assets 애플리캐이션에 국한되지 않는 라이브러리나 다수의 애플리케이션에서 함께 사용할 수 있는 라이브러리에서 사용하는 asset들 윛 ㅣ
- vendor/assets javascript 플러그인과 css 프레임워크에서 사용하는 asset 들 

#### manifest 파일 
- asset pipeline 핵심은 manifest 파일
- 레일즈는 디폴트로 stylesheet 용파일 ( app/assets/stylesheets/application.css)와 javascript 용 파일 (app/assets/javascripts/application.js) 하나 만들어줌

#### asset 폴더에 중복된 파일 존재 
- 다른 경로 상에 동일한 이름을 가진 두개의 asset 파일이 있을 때 
- asset 이 컴파일될 때 asset 경로상에서 발견되는 첫번째 파일 이후의 모든 중복 파일들은 포함되지 않게됨
- rails console 에서 asset 경로 확인 가능 

```ruby
Rails.application.config.assets.paths
```

#### asset pipeline이 사용하지 않는 경로상에 있는 asset 들을 사전 컴파일 하는 방법? 
- other/assets 폴더를 asset pipeline에 포함해서 사전 컴파일을 하고자 한다면? 
- application.rb 파일이나 환경 config 파일(config/enviromemts 폴더 내의 development.rb, production.rb, test.rb 파일) 에 아래의 코드 추가 

```ruby 
config.assets.path << "#{Rails.root}/other/assets"
```

#### 사전 컴파일 대상 추가하는 방법 
config/initializers/assets.rb 에 아래와 같은 설정 추가 

```ruby
Rails.application.config.assets.precompile << 'xx.js'
```

```ruby
Rails.applicatin.config.assets.precompile += %w(
  application-pc.scss
  application-sp.scss
)
```
https://negabaro.github.io/archive/rails-assets-pipeline



### app/assets와 public 의 차이 
- app/assets 안에 저장될 시 이름 뒤에 난수가 붙음 ( 브라어주 캐싱 방지를 위헤)
- 즉, assets 가 캐싱을 회피함

- public 은 난수가 붙지 않지만, assets에 담긴 css, js, 이미지 파일은 난수가 붙음 
- css, js 는 내용이 한 글자라도 바뀌면 난수도 또한 바뀜


https://kbs4674.tistory.com/17
https://guides.rubyonrails.org/asset_pipeline.html#coding-links-to-assets
