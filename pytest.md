# Pytest

파이썬에서 테스트 프레임 워크로 사용시, 간단하게 해결이 되지 않았던 부분 및 참고 사항을 정리

## 커멘트 라인에서 실행법

- 특정 파일을 실행 시키려 할 경우 : `PYTHONPATH=./. pytest test/test_pytest.py`
  - `PYTHONPATH=./. pytest` 를 쓰지 않으면 해당 프로젝트 모듈을 인식 하지 못함
  - 더 나은 해결 방법이 있을 지도 모름
- `print`  함수 내용을 출력 하려면, `-s` 인자를 추가 해 줘야 한다

## 기본 사용 테스트 함수

- 기본적으로 `test_` 가 붙은 함수를 실행 함. 
  -  테스트 함수의 경우  `test_`  를 붙임
  -  테스트에 사용 되는 함수의 경우  `test_`  를 붙이지 않으면 됨

## fixture

- pytest 에서는 before, after 그리고 mock 부분을 fixture 라는 부분으로 해결 할 수 있게 했음
- fixture 는 특정 객체 만들어 줄수 있음, 만들어진 fixture 를 테스트 함수에서 인자로 받을 수 있음(Dependency Injection 됨)
  - **예제 필요**
- fixture 은 테스트 함수 인자와 fixture 명이 같으면 자동으로 DI 되는데, 같은 이름이 여러개인 경우 어떻게 되는 지 모르겠음
- after 같은 기능을 구현 하려면 `return` 해줬던 값을 `yield` 해주면 된다. 그럼 해당 값이 사용 되는 테스트가 돌고 그뒤에서 있는 명령어 들이 작동

### fixture 로 before, after 구현

### fixture scope

- fixture 는 scope 를 제한 해 주수 있는데 아래 가지 옵션을 갖음
  - `function` : 함수 마다 새로 생성 됨
  - `session` : 세션을 폴더 구조를 따르는 줄 알았는데 모든 테스트가 끝나고 돔
  - `module` : 모듈당 한번 생성 됨
  - `class` : 클래스 생성과 소멸시 동작

