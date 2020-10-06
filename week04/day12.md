#### 오늘 한 일 
- 미완성 SMS 페이지 완성 및 견적 페이지 완성

- 돌봄 상세보기 페이지에 돌봄 일지 보기와 돌봄 사진 보기 버튼 추가 


#### 링크에 값 넣어 보내기 
- 위의 돌봄 상세보기 페이지에 추가한 돌봄 일지 보기와 돌봄 사진 보기 버튼에서 배운 것.

- 돌봄 일지 보기 버튼이나 돌봄 사진 보기 버튼을 누를 시 해당 돌봄(task_id)가 필터링된 페이지를 띄워야 했다. 

- 그러기 위해서는 링크에 해당 task_id와 그 task_id를 나타낼 키를 넣는 작업이 필요했다.

- 먼저 필터링된 페이지의 url을 보면 다음과 같은 형태이다. 

    http://localhost:3000/staffs/journals?q%5Btask_id_eq%5D=11537

- journals 라는 페이지에서 q라는 필터링을 위한 키, 해당 필터링을 위해 필요한 키인 task_id_eq, 마지막으로 task_id 값이다. 
- 위의 작업을 위해 staffs_journals_path 라는 주소값에 실어보낼 값으로 task_id_eq 키와 task_id 값을 보내면 되는데, <br>

  필터링을 위한 키인 q가 그 키와 값을 필요로 하기 때문에 중괄호로 묶어서 보내야한다. 
  
  
```ruby
    <%= link_to '돌봄 일지 보기', staffs_journals_path(q:{task_id_eq: @task.id}), class: "ui button" %>
```
