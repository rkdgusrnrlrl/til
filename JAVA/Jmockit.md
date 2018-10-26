# Jmockit 

이전에 나는 Mocking 라이브러리로 mockito 를 썼었다. 가장 많이 사용 되는 라이버러리이고, SpringTest 도 Mockito를 내부적으로 사용 하고 있는 걸로 알고 있다. spark 써 보면서 많이 쓰는 프레임워크 및 라이브러리가 꼭 좋은(내 상황에 최적화 된) 것은 아니라는 것을 알게 되었다. 그래서 한번 다른 것들(?)을 시도 해보고 있다. spark 에서는 easyMock 을 추천 하는데 Mocking 라이브러리가 여러개(기본적으로 3개가 유명)있다는 걸 알고 뭐가 좋을까 알아보았다.

## Mockito VS Jmockit VS easyMock

- [Mockito vs EasyMock vs JMockit](http://www.baeldung.com/mockito-vs-easymock-vs-jmockit)
- [Difference between Mockito and JMockit](https://blog.knoldus.com/2018/01/02/difference-between-mockito-and-jmockit/)
- [What are the best mock frameworks for Java?](https://www.slant.co/topics/259/~best-mock-frameworks-for-java)

위의 링크를 참조 했지만 구글 번역기로 돌려 잘 알아보지 못했다. 내가 jmockit 을 정한 이유는 mockito는 써봤고, easyMock 은 너무 경량 일 것 같다(그냥 느낌...) 그리고 jmockit 을 쓰면 코드가 일관성을 갖게 도움을 주고 러닝 커브가 가파르기 때문에 선정 했다. 그리고 private 메서드도 mocking 이 가능한걸로 알고 있다.

어찌 됐든  Jmockit 을 사용 하기로 했다.



## Jmockit 간단한 Mock 테스트

```java
import mockit.Expectations;
import mockit.Mocked;
import org.junit.Test;
import spark.Request;

import javax.servlet.http.HttpServletRequest;

import static org.junit.Assert.assertArrayEquals;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.fail;

public class TestJmockit {

    private final String JSON_STRING = "{\"name\":\"이름\"}";

    @Test
    public void testMockTest(@Mocked Request request) {
        new Expectations() {{
           request.body(); result = JSON_STRING;
        }};

        String body = request.body();
        assertEquals(body, JSON_STRING);
    }
}

```

- 해당 코드는 `junit`, `jmockit` , `spark` 의 의존성을 갖고 있다.
- `request.body()` 메서드를 Mocking 한 테스트 코드 이다.
- `{{ }}` 흡사 mustache 템플릿 코드 같은 문법 떄문에 해당 코드를 이해햐는데 어려웠는데, 알기 쉽게 쓰면 아래와 같다.

```
new Expectations() {
    //static block
    {
        request.body(); result = JSON_STRING;
    }
};

```

- 해당 표현은 익명 함수의 static block 이다. 



## The Record-Replay-Verify Model

- jmockit 은 `record replay verify` 단계를 갖는다. 
- `record` 위에 `Expectations`  부분인데, mock 이 어떻게 동작 할지 정의 해준다.
- `replay` 테스트 할 코드를 실행 하는 단계 이다.
- `verify` 는 우리가 예상했던 것 처럼 동작했는지 검증 한다. 예를 들어 `A.a()` 가 호출 됐는지, 1번만 호출 됐는지 등을 검증 한다. 
- 이런 형테의 구조를 명시적으로 할 수 있게 한다. 



## 참조

- [JMockit 101](http://www.baeldung.com/jmockit-101)
  - 프로듀스 101 도 아니고 왜 뒤에 101이 붙었는지 모르겠음 
  - 최근(2018)에 작성되기 시작해 최신 내용으로 이뤄져 있다.
  - 시리즈로 연재 할 것 같은데 우선 [A Guide to JMockit Expectations](http://www.baeldung.com/jmockit-expectations) 가 있다.