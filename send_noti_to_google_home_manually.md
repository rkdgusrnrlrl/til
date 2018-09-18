# 구글홈 메뉴얼 하게 알람 보내기

구글홈에서 알람을 알려 주기 위해, ifttt 로 해결 하려 하니 if 부분만 가능 하고 then 부분에 넣은 수 있는 기능 자체가 없다. 그래서 찾아본 방법을 적어 놓았다.



## Dialogflow 의 흐름

[Build Actions for the Google Assistant (Level 1)](https://codelabs.developers.google.com/codelabs/actions-1/index.html#0) 를 보고 따라 했다.

모든 과정은 한글(한글로 문장을 받고 답변을 한다는 가정)로 진행 했다. 기본적으로 `intents` 를 등록 해준다. 그때 문장을 넣어 주는 데, 문장에 따라 안에 값을 분석해 주 인자 화시켜버린다. 여러 문장을 넣어 주면 그 문장 마다 사용 도는 공통된 인자를 추출 한다. 이 인자가 웹훅 혹은 google function 인자로 넘겨 주는 것 같다.

다음으로 Fulfillment 를 등록 해주면 되는데, 요약 하면 위의 처리가 끝난 값을 받을 웹훅을 등록 하든 google function 을 사용 해 처리 하는 것을 말한다. 

하지만 google function 과 연동이 이상 한것 같다. 분면 내 소스가 배포 되었다고 뜨는 데 google function  로그를 살펴 보면, 배포 로그를 찾을 수 없다. request를 보내보니 서버는 죽은 상태.... 뭔가 내가 제어가 불가능. 그러자니 웹훅을 등록 하자니 당장 떠 있는 서버가 없다... 방법이 보이지 않아서 포기

인터 페이스는 직관적이 여서 좋긴 한데 연동 되는 부분이 아직 허술 하지 않나 싶다.



## Node.js 모듈을 사용 해 메뉴얼 하게 처리

답이 안나와.... 라이브러리를 뒤지던중 [google-home-notifier](https://github.com/noelportugal/google-home-notifier) 를 발견 했다.

당연히 리눅스에서 돌려 봤고 잘 작동 하는 것을 확인 했다. 하지만 초기 npm 으로 해당 모듈 설치시 잘 안되는 문제가 있는데 [해당 이슈](noelportugal/google-home-notifier/issues/8#issuecomment-304688674)를 찾고 해 해결 하였다. `libavahi-compat-libdnssd-dev` 만 설치 하면 됐다. 

구글 홈 이름으로 디바이스를 찾으려고 했는데 어려움이 있었다. 결국 내부 아이피를 ip 확인 해서 해결 했는데, iptime 관리자 페이지에서 `고급설정 > 무선랜 관리 > MAC 주소 인증` 을 통해 확인 할 수 있다.