### template is missing 에러 
> layout이 없어서 발생하는 에러 
> _show.html.erb 폴더를 불러오지 못해 해당 html/text 파일을 찾지 못해서 발생했는데 <br>
  show.html.erb 로 하니 해결. <>
  (레일즈 렌더링 개념을 좀 더 공부할 것)
  
  
### display:flex

#### 잘안되던 일 
- 컨텐츠 크기에 따라 review content div 태그의 크기가 변하는 것 
> overflow:hidden 먹이고 height:auto를 주었는데 안되었음 
> 그 둘다 지우고 display:flex를 주니까 해결 

- 헤더를 누르면 가장 최근 id 값을 파람값으로 넘겨 해당 id가 가지고 있는 사진을 보여주고 <br>
  이전 버튼을 누르면 그 id값을 기준으로 이전 id의 사진을 보여주는 작업 
> 컨트롤러에서 orm 코드를 잘못 짜 파람값이 가장 최근 id값으로 고정되어 버림 
> 아직 해결중


#### 내일 할 일
- 예쁜 돌봄 사진 마저 작업
