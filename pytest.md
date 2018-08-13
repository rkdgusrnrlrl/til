# Pytest

파이썬에서 테스트 프레임 워크로 사용시, 간단하게 해결이 되지 않았던 부분 및 참고 사항을 정리

## 커멘트 라인에서 실행법

- 특정 파일을 실행 시키려 할 경우 : `PYTHONPATH=./. pytest test/test_pytest.py`
  - `PYTHONPATH=./. pytest` 를 쓰지 않으면 해당 프로젝트 모듈을 인식 하지 못함
  - 더 나은 해결 방법이 있을 지도 모름

