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

- POST 의 경우 body 가 필요한 경우가 있느데, 아래과 같이 해결 할수 있음

  ```java
  @Test
  public void 사용자정보를_등록_출력() throws IOException {
      User user = User.builder()
          .name("강현구")
          .age(29)
          .build();
      ObjectMapper objectMapper = new ObjectMapper();
      String json = objectMapper.writeValueAsString(user);
  
      Content content = Request.Post("http://localhost:4567/users")
          .bodyString(json, ContentType.APPLICATION_JSON)
          .execute()
          .returnContent();
      String body = content.asString();
      assertEquals(body, "{\"data\":{\"user\":"+json+"}}");
  }
  ```

  - `jackson` 을 사용해 클래스를 json `String`  으로 변환 했음
  - 보통 모델 및 `Entity ` 가 있으니 해당 클래스를 인스턴스를 생성해 json `String` 으로 변환 하는 걸 추천

