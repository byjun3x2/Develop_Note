---
link: "[[_Git Start]]"
title: 아니 git pull 명령어만 사용하면 되지 왜 굳이 git fetch를 사용하는 거야
source: https://www.perplexity.ai/search/ani-git-pull-myeongryeongeoman-0ZS42vgBTxuiG3HfPtmWQQ
created: 2025-12-05
tags:
  - clippings
---
## 아니 git pull 명령어만 사용하면 되지 왜 굳이 git fetch를 사용하는 거야

검토됨 15개의 소스

`git pull` 만 사용해도 문제는 없지만, **`git fetch` 는 작업 중이던 코드가 갑자기 꼬이는 것을 방지하기 위한 '안전장치' 역할을 하기 때문에 중요합니다.**`git pull` 은 원격 저장소의 내용을 가져와서(`fetch`) 내 코두와 **즉시 합쳐버리기(`merge`)** 때문에, 내가 작성 중이던 코드와 충돌이 나면 당장 해결해야 하는 상황이 발생할 수 있습니다. 반면 `git fetch` 는 일단 가져와서 확인만 하고 병합은 나중에 할 수 있어 훨씬 안전합니다.

## git fetch를 굳이 사용하는 이유

`git pull` 은 편리하지만, "묻지도 따지지도 않고 병합"하는 특성 때문에 때때로 위험할 수 있습니다. 개발자들이 `git fetch` 를 선호하는 구체적인 상황은 다음과 같습니다.

- **충돌(Conflict) 예방 및 사전 검토**: `git fetch` 를 하면 원격 저장소의 변경 사항을 `origin/main` 같은 원격 추적 브랜치로만 가져옵니다. 내 작업 코드(Working Directory)에는 전혀 영향을 주지 않으므로, `git log origin/main` 이나 `git diff main origin/main` 으로 **남들이 무엇을 고쳤는지 먼저 안전하게 뜯어볼 수 있습니다**.[yozm.wishket +3](https://yozm.wishket.com/magazine/questions/share/zWX3P5GVg81ovUC7/)
- **갑작스러운 흐름 끊김 방지**: 신나게 코드를 짜고 있는데 `git pull` 을 했다가 덜컥 충돌 메시지(CONFLICT)가 뜨면, 하던 작업을 멈추고 충돌 해결에 시간을 쏟아야 합니다. `git fetch` 는 이런 일이 발생하지 않으므로, 내가 편한 타이밍에 병합(`git merge`)을 시도할 수 있습니다.[freecodecamp +1](https://www.freecodecamp.org/korean/news/git-fetch-vs-pull/)
- **병합 방식 선택권 확보**: `git pull` 은 기본적으로 `merge` 를 수행합니다. 하지만 상황에 따라 `rebase` 를 해야 깔끔한 커밋 히스토리가 유지될 때가 있습니다. `git fetch` 로 먼저 변경 사항을 확인한 뒤, `git merge` 를 할지 `git rebase` 를 할지 전략적으로 결정할 수 있습니다.[cheonjoosung.github](https://cheonjoosung.github.io/blog/cs-gitifetchpull)

## git fetch vs git pull 비교

두 명령어의 핵심 차이는 **"내 작업 공간(Working Directory)을 건드리는가?"** 입니다.[reddit](https://www.reddit.com/r/git/comments/1gblj80/why_git_fetch_preferred_over_git_pull_git_vs/)

| 기능 | git fetch | git pull |
| --- | --- | --- |
| **동작** | 원격 변경 사항을 로컬 `.git` 폴더로만 다운로드 (업데이트 확인용) | 원격 변경 사항 다운로드 + **현재 브랜치와 즉시 병합** |
| **내 코드 영향** | **없음** (작업 중인 파일 안 바뀜) | **있음** (파일 내용이 바뀜) |
| **충돌 가능성** | **0%** (병합을 안 하므로) | **있음** (같은 파일 수정 시 발생) |
| **주 사용 목적** | 다른 사람의 작업 내용 확인, 코드 리뷰, 안전한 업데이트 | 빠른 동기화, 충돌 걱정 없을 때 |

## 실무에서의 사용 팁

혼자 개발하거나 간단한 프로젝트라면 `git pull` 만 써도 충분합니다. 하지만 협업 중이거나 복잡한 기능을 개발 중이라면 다음과 같은 흐름을 추천합니다.

1. **`git fetch`**: 일단 원격 변경 사항을 안전하게 가져옵니다.
2. **`git status`** 또는 **`git log --all --graph`**: 그래프를 보며 내 커밋과 원격 커밋이 어떻게 갈라졌는지 확인합니다.
3. **`git merge origin/main`** (또는 `rebase`): 충돌이 날지 안 날지 알고 있는 상태에서 안전하게 합칩니다.

결론적으로 `git fetch` 는 \*\*"일단 업데이트 내용만 확인하고, 합치는 건 내가 준비됐을 때 하겠다"\*\*는 신중한 접근 방식입니다.