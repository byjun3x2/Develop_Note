---
link: "[[_Clipping]]"
title: "git checkout . 을 하면 어떤 상황이 펼쳐지는지"
source: "https://www.perplexity.ai/search/git-checkout-eul-hamyeon-eodde-BLTvyhj5TUCruubfKPiX8Q"
created: 2025-12-05
tags:
  - "clippings"
---
## git checkout. 을 하면 어떤 상황이 펼쳐지는지

검토됨 15개의 소스

`git checkout .` 명령어는 현재 작업 디렉토리(Working Directory)에서 아직 스테이징되지 않은(unstaged) 모든 파일의 변경 사항을 취소합니다. 즉, 마지막 커밋 시점의 상태로 모든 파일을 되돌리는 역할을 합니다.[zoosso.tistory +1](https://zoosso.tistory.com/729)

이 명령어를 실행하면 다음과 같은 상황이 발생합니다.

- **변경 사항 폐기**: `git add` 명령어로 스테이징 영역(Index)에 추가하지 않은 모든 수정 내용이 사라집니다.[zoosso.tistory](https://zoosso.tistory.com/729)
- **파일 복원**: 작업 디렉토리에 있는 추적 중인(tracked) 파일들이 가장 최근 커밋된 버전으로 복원됩니다.[lemu-devblog.tistory +1](https://lemu-devblog.tistory.com/61)
- **데이터 손실 가능성**: 이 작업으로 폐기된 변경 사항은 복구하기 어렵기 때문에, 중요한 내용이 있을 경우 신중하게 사용해야 합니다.

`git checkout` 명령어는 브랜치 전환, 커밋 이동, 파일 복원 등 다양한 기능을 가지고 있어 역할이 복합적입니다. 이러한 혼동을 줄이기 위해 Git 2.23 버전부터는 파일 복원 기능이 `git restore` 명령어로 분리되었습니다. 따라서 현재는 `git checkout .` 대신 `git restore .`를 사용하는 것이 의도를 더 명확하게 표현할 수 있어 권장됩니다.[velog +3](https://velog.io/@junsikchoi/TIL-Git-%EC%BB%A4%EB%B0%8B-%EC%97%86%EC%9D%B4-Checkout-%ED%95%98%EB%A9%B4-%EC%96%B4%EB%96%A4-%EC%9D%BC%EC%9D%B4-%EC%9D%BC%EC%96%B4%EB%82%A0%EA%B9%8C)