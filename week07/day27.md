### 루비 연산자 

1. && / ||
and, or

2. &&= / ||= <br>
a &&= b ---> a&&b <br>
a ||= b ---> a||b


### 오늘 한 일 
- Journal의 이미지들을 페이지에 띄우되, 한 페이지에 한 장 씩 만 띄우기 

#### 안되던 부분
- Journal의 id로 이미지를 불러오면 한 장 씩 띄울 수 없을 것이라 생각해 <br>
  ActiveStorage::Blob에서 key값을 하나씩 띄우려고 했었음 <br>
- 이미지를 한장씩 불러오기 위해서는 blob의 key값 뿐이라고 생각
- 그런데 ActiveStorage::Attachment라는 테이블에서 id값으로 가져오는게 더 깔끔했다. 
- 위의 테이블에서는 record_type이라는 컬럼명으로 여러 테이블들의 이미지들을 가지고 있는데, <br>
- 여기에 조건문으로 record_type: "Journal"을 주어 journal 이미지만 가져오면 된다. 
- 이 이미지들을 가지고 정렬해 id 값으로 이미지를 불러오면 내가 처음 생각했던 방법보다 훨씬 간편하다.

### 다음으로 할 일 
- 이미지를 눌렀을 때 like 표시 되게 할 것 
- default가 like이고 cancel 시 journal_like의 status가 cancel이 되게 할 것 
