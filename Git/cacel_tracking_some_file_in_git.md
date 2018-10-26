# 전체 커밋 로그에서 특정 파일 삭제

git 을 쓰다보면 공개 되면 안되는 설정 파일 및 키 값들을 모르고 커밋 하는 경우 가 많다. 이게 한 커밋 전이면 지우고 복구 하면되는데, 그것이 아니면 `git filter-branch` 를 사용 해야 한다.  특정 파일을 삭제 하는 경우 아래와 같이 사용 한다.

```bash
$ git filter-branch --tree-filter 'rm filename' HEAD
```

