### 오늘 한 일 
- 사이드킥 이용해 정기적으로 width, height 데이터를 resize_metadata 에 넣고, 해당 데이터가 들어갈 시 image_resize에 resize 가 들어가는 작업


#### 안되던 부분 
- update 시 resize_metadata와 image_resize 두 컬럼의 데이터를 넣음
- 이 때 resize_metadata 에 width와 height 두 데이터를 넣어야함 

- resize_metadata 의 type을 jsonb로 재설정하고 json 형태로 넣음 
- 그러면 나중에 나올 때 hash 로 알아서 나옴 

```ruby
blob.update( resize_metadata: { width: 298, height: 298 }, image_resize: "resized" )
```
______



### JSONB & JSON (PostgreSQL)
- 둘다 json 포맷 유효성체크 함 

*** 차이점
** 데이터 저장방식 
- JSON 은 들어온값 그대로 저장, JSONB 는 그렇지 않음 
- 문자열 사이의 공백도 제거해주고 key 순서도 보장하지 않음

** 디스크 사용량
- JSONB가 JSON보다 좀 더 많은 디스크 사용 (항상 그런 것은 않음)

** 인덱싱
- JSON는 인덱싱 불가, JSONB은 가능

** 주의사항
- JSON필드에 많은 양의 데이터를 저장할 수는 있음
- 그러나 JSON 필드에 있는 값을 변경할 때, JSON이 속한 ROW에 락이 걸리기 때문에 적정 수준의 데이터 저장해야함 

> 특별한 사유가 없다면 JSONB를 사용하는게 좋다고 함


