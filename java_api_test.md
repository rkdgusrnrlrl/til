# JAVA API 테스트 하기

- API 를 콜할수 있는 가장 유명한 라이브리러는 [HttpClient](https://hc.apache.org/index.html) 임

- [HttpClient Quick Start](https://hc.apache.org/httpcomponents-client-4.5.x/quickstart.html) 를 살펴보면 기본 사용법이 굉장히 어려워 보임

- 하단에 fluent API 를 쓰면 가독성 높고 쓰기 쉬워짐

- 따라서 2개를 의존성에 추가 해야함

  ```groovy
  dependencies {
      ...
      testCompile group: 'org.apache.httpcomponents', name: 'httpclient', version: '4.5.5'
      testCompile group: 'org.apache.httpcomponents', name: 'fluent-hc', version: '4.5.5'
  }
  ```

- json API 의 경우 아래와 같이 테스트 함

  ```java
  Content content = Request.Get("http://localhost:4567/users")
                                  .execute()
                                  .returnContent();
  String body = content.asString();
  assertEquals(body, "{\"data\":{\"users\":[]}}");
  ```