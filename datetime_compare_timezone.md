# 파이썬 datetime 비교

어떤 언어든 날짜 연산 부분은 쉽지 않다. 그래서 JAVA `joda-time`  을 사용 하고 javascript `moments` 라는 라이브러리를 사용 하곤 한다.  파이썬은 경우 타임존 부분과 `datetime` 이 분리 되어 있는데, 이 타임존은 `pytz`  라이브러리로 사용 한다. 파이쎤의 경우`datetime` 에 비교 연산자를 써서 비교 할 수 있는데 아래 코드와 같다.

```python
import datetime
import pytz

def test_compare_datetime():
    d_naive = datetime.datetime.now()
    timezone = pytz.timezone("UTC")
    d_aware = timezone.localize(datetime.datetime.now())
    assert d_naive < d_aware

=================================== FAILURES ===================================
____________________________ test_compare_datetime _____________________________

    def test_compare_datetime():
        d_naive = datetime.datetime.now()
        timezone = pytz.timezone("UTC")
        d_aware = timezone.localize(datetime.datetime.now())
>       assert d_naive < d_aware
E       TypeError: can't compare offset-naive and offset-aware datetimes

state_monitor/tests.py:24: TypeError
====================== 1 failed, 1 passed in 0.33 seconds ======================
Process finished with exit code 0

```

 하지만 우리는 에러를 만날 수 있는데 이는 타임존 문제 때문이다. 해당 코드를 디버깅 해보면, `d_navie.tzinfo`  가 `None` 으로 설정 되어 있다. `d_ware.tzinfo` 에는 ` UTC` 가 세팅 되어져 있다. 비교 연산을 위해서는 이 타임존 필드를 맞춰 줘야 하는데 아래 처럼 변경 하면 쉽게 해결 할 수 있다.

```python
def test_compare_datetime():
    d_naive = pytz.utc.localize(datetime.datetime.now())
    timezone = pytz.timezone("UTC")
    d_aware = timezone.localize(datetime.datetime.now())
    assert d_naive < d_aware
```

