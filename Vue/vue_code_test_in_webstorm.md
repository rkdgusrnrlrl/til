# Webstorm 에서 Vue 디버깅 하기

- [크롬 확장 프로그램 설치](https://chrome.google.com/webstore/detail/jetbrains-ide-support/hmhgeddbohgjknpmjagkdomcpobmllji)
- Run/Debug configurations에서 Javascript Debug 추가
  - URL 에 돌아가고 있는 서버의 url (ex : http://localhost:8000)
- 만든 Run 을 디버그 모드로 실행
- Vue 파일에서 브레이크포인트를 걸고 디버그모드로 실행하면 됩니다

### 전체적인 작업

- `npm run serve`  Run  을 통해 어플리케이션 실행(디버그 모드일 필요 없음)
- 위의 설명대로 진행
- 디버깅이 걸려 야 하는 부분 테스트

### 참조

- [Webstorm에서 Vue 앱 디버깅](https://github.com/vuejs-kr/vuejs-kr.github.io/issues/60)