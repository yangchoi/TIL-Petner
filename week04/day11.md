### git 


#### git stash 
- 작업 중이나 commit을 원치 않는 작업물들을 스택에 잠시 보관
- 워킹 디렉토리에서 수정한 파일들만 저장할 수 있음
- 아래에 해당하는 파일들을 보관해 둔다 
1.  modified 이면서 tracked 상태인 파일
2. staging area에 있는 파일(git add를 통해 staged 상태가 된 파일들) 



### rails 

#### 날짜 몇일 부터 몇일까지 찾기 
- ransack을 이용해 범위를 정한다. 
```html
<div class="two wide field list-filter">
  <div class="field">
    <label>업데이트 날짜</label>
    <div class="ui calendar" id="rangestart2">
      <div class="ui input left icon">
        <i class="calendar icon"></i>
        <%= f.text_field :updated_at_gteq, value: "#{params.dig('q', :updated_at).presence || '' }", class: "input is-medium", placeholder: "Start" %>
      </div>
    </div>
  </div>
  <div class="field">
    <div class="ui calendar" id="rangeend2">
      <div class="ui input left icon">
        <i class="calendar icon"></i>
         <%= f.text_field :updated_at_lteq, value: "#{params.dig('q', :updated_at).presence || '' }", class: "input is-medium", placeholder: "End" %>
      </div>
    </div>
  </div>
</div>
```
- gteq : greater than or equal
- lteq : less than or equal

