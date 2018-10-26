# 다른 브랜치에 있는 커밋 옮기기

- jetbrain IDE 를 사용
- cherry-pick 을 사용 하여 옮김
  - 붙일 브랜치로 checkout 
  - `VersionControl > Log` 창에 `Branch` 를 커밋이 있는 브랜치를 선택함
  - 로그 창에 옮길 커밋 영역을 선택 함
  - 오른쪽 클릭 하여 나오는 메뉴 중 `Cherry-Pick` 을 선택함
  - 커밋 하나 하나 마다 `Commit Changes` 창이 뜸 특별히 수정 할 것 이 없으면 계속 `Commit `을 진행
  - conflict 나는 부분은 에디터로 해결
- 중간에 쓸데 없는 커밋은 rebase 로 수정
  - 중간 커밋 삭제 : `git rebase --onto commit-id^ commit-id`

