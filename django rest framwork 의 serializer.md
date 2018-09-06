# django rest framwork 의 serializer

django rest framework 의 serializer 를 쓰던 중 `SlugRelatedField` 가 잘 동작 되지 않아서 디버거를 걸어 serializer 가 어떻게 동작 하는 지 분석했다

request -> viewset (.list())



### ListModelMixin.list(request, *arg, **kwargs)

ModelViewSet 의 리스트 API 구현체로 queryset 에 페이징 처리를 해주고 헤당 값을 `Serializer` 를 통해 serializer(dictionary 로 변경) 이 주 역활이다.

### Serializer

핵심을 `serializer` 인데, 기본은 `BaseSerializer` 이고, 여기서 `many_init` 과 `__new__` 주요하게 사용 된다. 또 `serializer.data` 는 프로퍼티 처럼 보이지만 사실 함수 이다. 

- viewset 에 세팅된 `serializer` 가 생성 하기 위해 `__new__` 가 먼저 call 되고 
  - 이떄 인자중 `many` 의 값이 True 로 온오기 떄문에 `many_init` 을 호출 한다. 

- `many_init` 에서 해당 `Serializer` 인스턴스가 생성되 child 인자로 `ListSerializer` 의 인자로 사용된다.
- `ListSerializer`  클래스를 호출해 인스턴스를 생성 한다. 
- 또 여기서 `BaseSerializer` 가 호출 된다 이떄는 `many` 의 값이 없기 때문에 `super(BaseSerializer, cls).__new__(cls, *args, **kwargs)`  이 호출 된다. 
- 그러면 `Field.__new__` 가 호출 된다. 해당 함수에서 인스턴스를 생성 하고 `_args`, `_kwargs` 에  값을 넣어준다.
- 그후 `ListSerializer` 의 `__init__` 함수가 도는데, `self.child` 에 생성한 `Serializer` 인스턴스를 넣어준다
  - `BaseSerializer.__init__` 이 콜 되고, `self.instance` 에 `queryset` 이 할당 된다 
- 작성중....

