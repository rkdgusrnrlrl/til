# `__new__` ,  `__init__` , `super()`

## `__new__ `,  `__init__`  란

`django rest framework` 소스를 열어 보면, 위의 메서드 들이 구현되어 있는 것을 볼 수 있다. `__new__` 의 경우 `__init__` 이전에 호출 되는 함수로 `django rest framework` 에서 사용 된 것을 보면, `__init__` 메서드 호출 전에 어떤 클래스를 `__new__` 할지 선택해주는 역활을 한다.



## `__new__` 의 역활

`__new__` 는 클래스의 정적 메서드로서 인스턴스 생성 해주는 역활을 한다. 그래서 값을 리턴 해줘야 하는데, `super().__new__()` 을 보통 리턴 해준다. 아무 것도 리턴 하지 않으면 생성자 호출시 `None` 을 리턴 한다. 그리고 `__init__` 은 호출 되지 않는다. 

보통을 잘 사용 되지 않는 다고 한다 `__init__` 쪽을 오버라이드 하는데 그전에 전처리가 필요 한 경우 쓰여지는 것 같다.



## `__init__` 의 역활

인스턴스의 프로퍼티를 초기화 하는데 사용 된다. 기본 생성자의 역활이라고 생각 하면 된다. 



## `super().__init__()` 와 `ParentClass.__init__()` 차이점

`super().__init__() ` 를 사용 할 경우 다중상속이 상위 클래스의 다중상속이 유지 되지만,  `ParentClass.__init__()` 의 경우 상위 클래스의 다중 상속이 끊어 진다.  mro(메서드 실행 순서) 가 `super` 를 쓰면 그대로 내려 오는 듯 하다.

### 참조

- [Python의 메서드 실행 방식 (MRO)](https://winterj.me/python-mro/)
- [[Python] __init __ () 메소드로 파이썬 super () 이해하기](https://code.i-harness.com/ko-kr/q/8caa9)



## `__new__` 를 사용한 factory 패턴

`__new__` 의 인자를 체크 해서 해당 인자에 맞는 인스턴스를 생성 하는데, 

### 참조

- [Using a class' __new__ method as a Factory: __init__ gets called twice](https://stackoverflow.com/questions/5953759/using-a-class-new-method-as-a-factory-init-gets-called-twice)