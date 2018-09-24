# 파이썬 파일 경로 핸들링

## 부모 디렉토리 경로 쉽게 얻어 오기

```python
import os
from pathlib import Path

Path(os.path.dirname(os.path.abspath(__file__))).parent.parent.parent
# ex) a/b/c/d.py -> a
```

## 특정 파일 경로 검색 및 필터링 하기

```python
import os
import glob

# 장고의 migrations 아래 있는 파이썬 파일 경로(str)을 가져온다 
some = glob.glob('**/migrations/*.py')
# 이중에서 __init__.py 가 포함 되어 있지 않은 파일 경로 (str)을 필터링 한다.
filted_file_paths = list(filter(lambda file_name: not ("__init__.py" in file_name), some))
```

## 경로 합치지

```python
import os

# ex base_dir='/a/b/c' db_file_name='db.sqlite3'
abs_db_path = os.path.join(base_dir, db_file_name)
```

- 그냥 String 값 이니 합쳐주면 되지 않냐 생각 할 수 있지만 두 경로 사이 경로 구분자 가 필요 하다
- 이는 OS 에 따라 다르기 때문에 `'/'` 과 같은 값을 직접 쓰면 좋지 않으므로, `os.path.join` 를 사용 하자

