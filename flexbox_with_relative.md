# flex 안에 posiotion relative 문제

- `display : flex ` 에 자식 컴포넌트가 `position : relative` 를 갖으면 문제 가 있다.
- 전제 조건 중하나가 부모 엘리먼트가 사이즈가 정해져 있을 경우 이다
- 해당 사이즈 넘겨 되는 경우 자식 컴포넌트가 자동으로 줄어 버리는 이슈가 있다.
- 이는 box model 에서는 보이지 않지만 `relative` 는 원래 공간을 그대로 차지 하고 있어 보이지기는 여유가 있지만 해당 공간을 다 차지 하고 있서 해당 사이즈에 자식 엘리먼트 크기를 맞추는 걸로 알고 있다.
- 해결 방법은 `position : absolute` 로 변경하면 된다. 
- 하지만 `absolute` 는  `relative`  와 같이 동작하지 않는다.
- 우선 `relative`  기존 위치에서 얼마를 옮겨야 하는 지 정해 줘준다면,  기준 컴포넌트에서 얼마나 떨어질지 를 정해 줘야 한다. 
- 또 부모를 기준 콤포넌트 로 하려면 `position : relative`  를 가져야 한다 

## 예시

- Github 레포지토리 : [flexbox-with-relative](https://github.com/rkdgusrnrlrl/flexbox-with-relative)

