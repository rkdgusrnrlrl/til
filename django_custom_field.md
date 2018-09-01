# 장고 선택 가능한 field 검증

장고에서 선택 가능한 필드를 만든는 법은 공식 페이지에 잘 나와있다. [Models > Fields >Choices](https://docs.djangoproject.com/ko/2.1/ref/models/fields/#choices) 에 보면 tuple 을 생성해 `CharField` 에 `choices` 필드에 넘겨주면 된다.

검증은 `Forms` 를 사용 해 검증이 가능 하다. `django.forms.fields` 에 아예 [ChoiceField](https://docs.djangoproject.com/ko/2.1/ref/forms/fields/#choicefield)가 있으며, 내부를 더 들여 봐야 겠지만, 추측해보면 choices 가 있는 Field 면 ChoiceField로 되는게 아닌가 싶다. 

```python
#Model
class APIStatus(models.Model):
    API_STATUS_CHOICES = (
        ('SUCCESS', '성공'),
        ('FAIL', '실패'),
    )
    status_id = models.AutoField(primary_key=True)
    check_time = models.DateTimeField(auto_now_add=True)
    status = models.CharField(max_length=10, choices=API_STATUS_CHOICES)
    api = models.ForeignKey(API, on_delete=models.CASCADE)


#Model Form
class APIStatusForm(ModelForm):
    class Meta:
        model = APIStatus
        fields = ('status',)


# 테스트 코드
def test_api_status_form():
    api_form = APIStatusForm({'status': 'WRONG'})
    assert {} == api_form.errors


# 테스트 결과
"""
{'status': ['Select a valid ...of the available choices.']} != {}

Expected :{}
Actual   :{'status': ['Select a valid ...of the available choices.']}
"""
```


생각해보면 필드 검증은 파라미터를 받았을 때 하면 되는 게 맞는 것 같다. 그래서 `Form`  을 사용 해 검증 하는 것 같다. 하다 보니 `validator` 쪽도 보게 되었는데, 필드에 기본 `validators` 인자를 통해 `validator`  함수를 받는다. 함수의 기본 구조는 인자로 `value`  라는 해당 필드 값을 받고, 검증 로직을 넣어, 실패지 `ValidationError` 를 던지면 된다.

특정 인자가 필요한 경우 `callable` 클래스로 만들어 진행하고 해당 필드를 `__init__` 함수를 오버라이드해 해당클래스 인스턴스를 생성해  `validators`  멤버에 넣어준다. 

참조 : [장고 choice 검증 필드](https://gist.github.com/rkdgusrnrlrl/05bc2a528e6ea4974be013f0f5266ec7)