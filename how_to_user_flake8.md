## Flake8 사용법

## flake8 란

- flake8 이란 파이썬 정적 코드 분석 툴이다. 
- 비슷한 걸로 `javascript` 계열에 `eslint ` 가 있다.

## flake8 설치

```bash
$ pip install flake8
```

## flake8 검사하는 예제

- 파일 하나 분석

  ```bash
  $ flake8 app.py
  ```

- 디렉토리 하위 파일들 분석

  ```bash
  $ flake8 ./dir
  ```

- 설정 파일의 설정으로 분석 (설정 파일이 `flake8` 이라는 가정)

  ```bash
  $ flask8 --config=./flake8 ./dir
  ```

