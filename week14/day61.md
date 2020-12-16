### Rspec 을 이용한 TDD

![image](https://user-images.githubusercontent.com/48708746/102313342-ce6edd00-3fb3-11eb-945d-951ec89ceb1b.png)

#### unit test
- 왼쪽 끝에 위치한 기능들 (Model, helper, view, service)을 테스트하는 경우 단위 테스트 (unit test) 
- 개별 구성 요소를 개별적으로 테스트해 주변 시스템과 독립적으로 에상되는 동작을 구현함을 증명 
- 단위 테스트는 일반적으로 작고 빠름 
- 하지만 실제 서비스에서는 모든 테스트에 통과했는데 예기치 못한 에러, 버그가 생길 수 있음 >> 통합테스트 해야함 

#### intergration test 
- 통합테스트는 동작하는소프트웨어를 만들고 있다는 것을 확신할 수 있기에 효과적 
- 유닛 테스트 보다는 느리고, 테스트가 깨지기 쉬운 경향이 있음 

> 테스트를 만들기 위해서는 이 유닛테스트와 통합 테스트를 적절하게 조합해 테스트 환경을 구축하는 것이 중요 

(참고 : 
https://medium.com/@70hojung/rspec-%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-tdd-b4ccd705aa06
https://books.thoughtbot.com/assets/testing-rails.pdf
)


### test 실행 및 로그 확인 

- 로그 확인 
ail -f log/test.log   


- rails http status 코드 심볼 

unprocessable_entity : 422 ( 서버가 요청을 이해하고 요청 문법도 올바르지만 요청된 지시를 따를 수 없음) 
https://gist.github.com/mlanett/a31c340b132ddefa9cca



### rails helper 
- 재사용 가능 코드를 view에 공유하는 메소드 

