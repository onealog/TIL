# git stash 몇 가지 팁

초보자를 위한 깃 책을 집필하고 있다. git stash에 관해 쓰다가 내가 자주 사용하는 stash 명령어 및 팁을 여기에 소개한다.   

<br>

- **git stash는 변경사항을 임시보관소 stash에 잠깐 보관하는 명령어**
- `git stash save <message>` 로 <message>를 남기며 저장할 수 있다.
  - 또 다른 명령어로는 `git stash -m <message>`
  - (모를 때는 `git stash push -m <message>` 로 했었다.. 사실 어느 것으로 하나 상관 없는 것 같다)
- stash에 보관된 변경사항 가져오는 방법
  - `git stash list` 를 입력해서 보관했던 stash 목록을 살펴본 다음..
  - 보통은 `git stash apply "stash@{n}"` 이렇게 해서 꺼내올 수 있는데..
  - 그냥 `git stash apply <n>` 으로 인덱스만 적어도 가져올 수 있다.
- 명령어 정리
  - `~ apply` 는 적용 => stash에 있는 것을 가져온다.
  - `~ pop` 은 적용 후 삭제 => stash에 있는 것을 가져온 뒤에 stash에 항목에서 제거한다.
  - `~ drop`은 삭제 => stash에 있는 항목을 제거한다.
- 뒤에 `"stash@{n}"` 이나 `<n>` 을 지정해주지 않으면 스택 구조라서 가장 최근에 보관한 stash가 적용된다.
  - `예시) git stash apply, git stash pop, …`
