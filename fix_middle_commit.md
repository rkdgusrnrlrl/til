# 중간 커밋 수정하기

오늘 MongoDB 로 마아그레이션 작업을 하며, 커밋을 하다 보니, 패스워드 정보를 설정 파일에 넣어 버렸다. 충격과 공포 였으나 마음을 가다듬고 마성의 `git rebase` 사용법을 뒤져보았다. [GIT REBASE, 커밋 이력을 유지하면서 과거 커밋의 내용 수정하기](http://blog.appkr.kr/work-n-play/git-rebase/) 라는 아주 좋은 글을 발견 하였다. 

위글을 고수는 터미널에서 작업 했으나 나는 초보임으로 IDE(Webstorm) 의 힘을 빌리기로 했다. 아래와 같은 절차로 진행 했다.

- 우선 `VCS log` 창을 연다 보통 `ALT + 9` 로 되어 있다.
- 내가 수정해야 하는 `commit log` 에 오른쪽을 클릭하면 `interactively Rebase from Here` 라는 메뉴를 클릭 한다
- 그러면 해당  `commit log`  부터 끝까지  `commit log`  들이 나오고 수정할  `commit log`  앞에 `select` 에서 `edit` 를 선택하고 `start rebase` 버튼을 클릭한다.
- 이제 해당 파일을 수정해 준다. 나 같은 경우는 그 `commit` 에 수정했던 파일 이였다. 
- 파일을 수정 하고 `commit changes` 창을 띄우면(`CTL + K`) `Amend commit` 이라는 체크박스가 있다. 체크해주면 해당 수정 `commit message` 로 자동으로 바뀐다. `commit` 을 눌러준다
- Action 검색으로 `Continue Rebase` 하면 완료
- 만약 `push` 되었다면 `git push -f` 로 해결 혹은 IDE 에서 `push` 시 `force push` 가 있으니 그걸 사용
- IDE 를 사용 하니 자동화 되는 부분이 많다. 그러니 IDE 를 쓰는데 무리 해서 터미널을 쓸 필요는 없을 것 같다. 

