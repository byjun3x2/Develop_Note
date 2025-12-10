---
link: "[[_Clipping]]"
title: "git checkout 명령어가 있는데 왜 굳이 restore 를 만들었을까"
source: "https://www.perplexity.ai/search/git-checkout-myeongryeongeoga-L3SzVr9RRniehnLW4g2aVg"
created: 2025-12-05
tags:
  - "clippings"
---
## git checkout 명령어가 있는데 왜 굳이 restore 를 만들었을까?

검토됨 17개의 소스

한마디로 정의하자면 \*\*"하나의 명령어(`checkout`)가 너무 많은 기능을 담당하여 혼란스러웠기 때문"\*\*입니다.

Git 2.23 버전부터 `checkout` 의 기능을 명확히 분리하여 브랜치 변경은 `switch` 로, 파일 복구는 `restore` 로 나누게 되었습니다. 개발자 입장에서 왜 이 분리가 필요했는지 구체적인 배경과 차이점을 정리해 드립니다.[oigie.tistory +1](https://oigie.tistory.com/143)

## 1\. 기존 checkout의 문제점: 과부하와 모호성

`git checkout` 은 태생적으로 두 가지의 전혀 다른 성격의 작업을 수행했습니다.

- **브랜치 이동 (HEAD 변경):** "나 `feature` 브랜치로 갈래." (`git checkout feature`)
- **파일 복구 (내용 덮어쓰기):** "이 파일 망쳤으니 마지막 커밋 상태로 되돌릴래." (`git checkout -- filename`)

이 두 기능은 기술적으로는 "무언가를 꺼내온다(Check out)"는 점에서 비슷할 수 있지만, 사용자의 **의도(Intent)** 측면에서는 완전히 다릅니다. 특히 초보자나 협업 과정에서 실수로 브랜치 이동 대신 파일 변경 사항을 날려버리는 사고가 발생하기 쉬운 구조였습니다.[enleaf +1](https://blog.enleaf.me/581)

## 2\. 역할의 분리: Switch & Restore

Git 2.23부터는 이 모호함을 해결하기 위해 목적에 맞는 전용 명령어를 도입했습니다.

- **`git switch`**: 오직 **이동** 만 담당합니다. (브랜치 변경)
- **`git restore`**: 오직 **복구** 만 담당합니다. (파일 내용 되돌리기)

이렇게 나누면 명령어를 입력할 때 "내가 지금 이동을 하려는 것인지, 복구를 하려는 것인지"가 명확해집니다.[velog +1](https://velog.io/@kms8571/git-switch-restore)

## 3\. 문법 비교: 더 직관적인 사용성

`restore` 는 복구 작업에 특화된 옵션들을 제공하여 문법이 훨씬 직관적입니다.

| 작업 내용 | 기존 (`checkout`) | 변경 후 (`restore`) |
| --- | --- | --- |
| **작업 내용 취소** (Working Tree 복구) | `git checkout -- file` | `git restore file` [outsider](https://blog.outsider.ne.kr/1505) |
| **Staging 취소** (Unstage) | `git reset HEAD file` | `git restore --staged file` [outsider](https://blog.outsider.ne.kr/1505) |
| **특정 커밋 시점으로 복구** | (복잡한 조합 필요) | `git restore --source=HEAD~1 file` [oigie.tistory +1](https://oigie.tistory.com/143) |

특히 `git add` 로 스테이징된 파일을 다시 내릴 때, 기존에는 `reset` 을 써야 했지만 이제는 `restore --staged` 로 통일성 있게 처리할 수 있다는 점이 큰 장점입니다.[velog](https://velog.io/@kms8571/git-switch-restore)

## 요약

`restore` 를 만든 이유는 `checkout` 이 가진 \*\*"브랜치 이동"\*\*과 \*\*"파일 복구"\*\*라는 두 가지 책임을 분리하여 **실수를 줄이고 명령어의 의미를 명확하게 만들기 위해서** 입니다.

아직 `checkout` 도 여전히 동작하지만, 새로 배우거나 스크립트를 짤 때는 의도가 명확한 `switch` 와 `restore` 를 사용하는 것이 권장됩니다.