# flask API 서버 개발

- 이 문서는 주기적으로 배운 내용을 계속 정리 햘 예정 임
- 해당 내용 관련 소스는 [rkdgusrnrlrl/flask_real_world](https://github.com/rkdgusrnrlrl/flask_real_world)에서 있음
- [realworld](https://github.com/gothinkster/realworld) 의 백엔트 부분은 구현 함
- 기본적으로 다른 라이브러리 혹은 프레임워크 결합시 결합된 프레임워크를 사용 하지 않음
  - 단위로 테스트 하기 용이 하고, 추후 다른 프레임워크에 결합시 쉬움
  - 더 많은 부분(결합에 필요한 부분)을 더 파악 할 수 잇음
- 라이브러리 프레임워크는 최소한으로 함
- 테스트는 되도록 챙기되 생산성이 너무 떨어지는 경우 테스트를 위해 프레임워크 혹은 라이브러리를 만들어야 하는 경우 혹은 stuff 및 fixture 만드는데 너무 많은 시간이 소요 될 경우 간소화 및 패스 함
- 코드 컨벤션은 `pep8` 을 따름

## Flask

- `route` 걸어주는 `function` 의 경운 인자로 `request` 를 받지 않는 부분이 의아 했음 
  - `import` 된 `request` 를 사용
  - `request` 에` json` 함수를 지원해서  쉽게 `dictionary` 로 변경 할 수 있음
- `response` 의 경우 `jsonify` 를 사용해 `json` 으로 변경 해줘야 한다.
  - 당연히 `SQLAlchemy` 모델의 인스턴스인 경우  `jsonify`  으로 변경 불가능
  - `SQLAlchemy` 모델의 인스턴스를 `dict` 로 변경 해줘야 하는데 `__dict__` 로 변경 하면 이상한 것들이 달려 옴
  - `dict`필드에 `byte` 가 있는 경우 `json` 으로 변경되 안됨
- 테스트를 위한 `client` 를 제공해줌 
  - `pytest` 에서는 `fixture` 로 만들어 두어 사용 할 수 있음



## SQLAlchemy

- ActiveRecord 패턴 인 줄 알았는데(django-orm 처럼), DataMapper 패턴 구현체라 기쁜 마음으로 사용
- `persistance` 부분이 중요, 등록을 했는데, `id` 값이 할당이 안되 문서를 보니, `session` 사용 부분 `persistance` 관련 내용이 많이 있었음. 해당 문제는 별개로 `commit()` 을 안해서 생긴 문제
  - `add` 함수로 인스턴스가 저장 된 줄 알았는데, `commit` 추가 호출 해줘야함. 이점은 꽤 번거로움
  - 확실히 한단계 추상화 계층이 필요할 듯, 아마 `Repository`?! 이렇게 JAVA 와 비슷한 형태로...
- `SQLAlchemy`  의`Base` 사용시 모델과 `app` 따로 `import` 하면 초기 테이블 생성 함수 콜할 때 모델들이 테이블로 생성되지 않음
  - `Base` 부분은 따로 공통으로 빼두어야 할 것 같음
- flask 과 연동 되어야 할 경우 아래 내용들을 참고 했음
  - [How do I lazy init SQLAlchemy](https://stackoverflow.com/questions/22890049/how-do-i-lazy-init-sqlalchemy) : sqlalchemy 의 engine 은 flask 앱 실행시 초기화 할 수 있는 방법 공유
  - [Flask and SQLAlchemy without the Flask-SQLAlchemy Extension ](https://dev.to/nestedsoftware/flask-and-sqlalchemy-without-the-flask-sqlalchemy-extension-3cf8) :  `flask-sqlalchemy`를 쓰지 않고 flask 과 sqlalchemy 를 통합해 쓰는 방법 공유
  - [flask_sqlalchemy_starter](https://github.com/nestedsoftware/flask_sqlalchemy_starter) : 위의 방법으로 만들어진 boilerplate 
