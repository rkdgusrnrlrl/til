# TripleA 코드 분석 하기

tripleA 는 A&A 라는 보드게임을 기반으로 만들어진 PC 게임 이다. 오픈소스로 공개 되어 있고, 해당 소스는 github 에 올려져 있다. 해당 글은 TripleA 코드를 분석해 구조를 파악하고, 이슈를 해결 하기 위한 초석을 다지기 위해 작성 되었다.

## 코드의 기본 적인 배경 지식

- 우선 해당 소스는 JAVA 로 구성 되어 있다.
- JAVA FX 로 만들어 진 데스트탑 어플리케이션이다. 
  - 내부 Swing 컴포넌트도 보인다. (Swing 이 메인 일지도...)
  - 아마 JAVA FX 로 넘어 가고 있는 중인 듯 싶다.
- 빌드 툴로 gradle 을 사용 한다.



## 디버깅 준비

- 우선 나는 intellij 를 사용 한다. 따라 모든 내용은 intellij 로 설명 되어 있다.

- 우선 gradle Task 중 `game-core > application > run` 을 실행 해준다

- 디버깅을 하기 위해 기본적으로 맵 하나를 받는 것이 좋다. 

  - High Quality > Available > MiniMap 을 설치 하였다.

- 진입점은 `games.strategy.engine.framework.startup.ui.panels.main.MainBuilder` 를 살펴 보면 된다.

  ```java
  final MainPanel mainPanel = new MainPanel(
      gameSelectorPanel,
      uiPanel -> {
          setupPanelModel.getPanel().preStartGame();
          setupPanelModel.getPanel().getLauncher()
              .ifPresent(launcher -> launcher.launch(uiPanel));
          setupPanelModel.getPanel().postStartGame();
      },
      () -> Optional.ofNullable(setupPanelModel.getPanel())
      .map(ISetupPanel::getChatPanel),
      setupPanelModel::showSelectType);
  ```

  - 위의 코드에 `MainPanel` 의 생성자의 두번째 인자인 `launchAction`  플레이 버튼 뒤에 실행 되는 액션임으로 저기에 디버깅을 걸으면 게임 시작 진입에 디비깅을 할 수 있다.
  - `launchAction` 의 타입은 `Consumer<MainPanel>` 이기 때문에 `Consumer` 이해를 하고 있으면 좋을 것 같다.

