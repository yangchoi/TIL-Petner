### 오늘 한 일 
- 어떤 페이지 접속시 root path로 빼기 
(해당 액션이 컨트롤러로 들어올 시 301 던져주고 root_path로 빠질 수 있도록)

#### 해결 방법 
- show가 실행 될 때 before_action을 이용해 block_show 메소드 실행 
- block show에서 redirect_to root_path 설정 
- 단, 301 코드를 먹임 
- 301 코드를 먹이지 않으면 캐싱 처리가 되어서 경로처리가 안먹을 수도 있어서 값을 넘겨줘야함

_________


### 301 & 302 
#### 301 move permanently
- 요청한 리소스가 location 헤더에 주어진 url로 완전히 옮겨짐을 의미 
- 검색 엔진은 해당 리소스로 연결되는 링크를 갱신 (검색엔진 최적화 관점에서는 '원 콘텐츠가 새로운 Url로 옮겨졌음' 이라고 함)

https://developer.mozilla.org/ko/docs/Web/HTTP/Status/301

#### 302 found
- 클라이언트가 요청한 리소스가 location 헤더에 주어진 url에 일시적으로 이동되었음을 가리킴 
- 브라우저는 사용자를 이 url의 페이지로 리다이렉트 시키지만 검색엔진은 그 리소스가 일시적으로 이동되었다고 해서 그에 대한 링크 갱신하지 않음 
(seo 관점에서는 링크 주스가 새로운 url로 보내지지는 않음)

https://developer.mozilla.org/ko/docs/Web/HTTP/Status/302

> 결론 : 위의 작업은 홈페이지 검색 시 에전에 만들어져 현재는 서비스하지 않는 사이트가 걸려들어 <br>
해당 사이트를 아예 root_path 로 돌리기 위함이니 seo 관점에서 새로운 url로 옮겨놓는 301 코드가 사용하기에 더 적절 



### redirect_back(fallback_location:..)
