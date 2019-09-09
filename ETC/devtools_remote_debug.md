# 크롬 DevTools Remote Debug

크롬의 기능중에 개발자가 유용 하게 쓰는 거는 단연 개발자 도구 일 것이다. 해당 툴을 통해 개발을 위한 많은 정보들을 얻는다. 이런 개발자 도구를 원격으로 쓸 수 있다는 사실은 많이 모를 것이다. 심지어 API 까지 제공 해 주고 있다.  아래 링크를 통해 해당 정보를 볼 수 있다.

[devtools-protocol](https://chromedevtools.github.io/devtools-protocol/)

`chrome.exe --remote-debugging-port=9222` 로 크롬을 실행 하면 `http://localhost:9222/` 로 Remote Debug API 를 접속 할 수 있는데 API 는 많지는 않다. 브라우저 버전과 페이지(탭)에 대한 정보만 알 수 있다. 

그럼 DOM 이라든지 Network(request, response) 는 어떻게 알 수 있을까? 그것은 Rest API 가 아니라 websocket 을 통해 알 수 있다. 페이지 별로 정보를 받아올 수 있느데, 주소는 `http://localhost:9222/devtools/page/{targetId}` 과 같다. 자세한 사용 방법은 [protocol-fundamentals](https://github.com/aslushnikov/getting-started-with-cdp/blob/master/README.md#protocol-fundamentals)

을 참고 하면 된다. request 에 `method` `parameter` 값은 위의 API 를 참조 하면 된다.

