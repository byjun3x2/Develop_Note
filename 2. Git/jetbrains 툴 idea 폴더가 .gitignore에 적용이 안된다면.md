[[_Git Start]]

IntelliJ에서 프로젝트를 생성하면 `.idea` 폴더가 자동으로 생성됩니다. 이 폴더는 IDE의 프로젝트별 설정값을 저장하며, 개인 환경 설정이 포함되어 있어 다른 개발자와 공유할 경우 충돌이 발생할 수 있습니다. 따라서 `.idea` 폴더는 일반적으로 `.gitignore` 파일에 추가하여 Git의 버전 관리에서 제외하는 것이 권장됩니다[1][3][4].

### `.gitignore`에 `.idea` 폴더를 제외하지 못하는 경우 해결 방법
1. **`.gitignore` 파일 생성 및 수정**:
   - 프로젝트 루트 디렉토리에 `.gitignore` 파일을 생성하거나 기존 파일을 엽니다.
   - 아래 내용을 추가합니다:
     ```
     # IntelliJ IDEA settings
     .idea/
     ```
   - 이미 커밋된 `.idea` 폴더가 있다면, 이를 먼저 제거해야 합니다.

2. **이미 커밋된 `.idea` 폴더 제거**:
   - 다음 명령어를 사용해 Git의 추적에서 제거합니다:
     ```bash
     git rm -r --cached .idea
     ```
   - 이후 변경 사항을 커밋합니다:
     ```bash
     git commit -m "Remove .idea folder from version control"
     ```

3. **Git 상태 확인**:
   - `.gitignore` 파일이 제대로 적용되었는지 확인하려면 아래 명령어를 실행하세요:
     ```bash
     git status
     ```
   - `.idea` 폴더가 추적되지 않아야 합니다.

### 주의사항
- `.gitignore` 파일이 제대로 적용되지 않는 경우, 캐싱 문제일 수 있으므로 위의 `git rm --cached` 명령을 사용하는 것이 중요합니다[2][6].
- 팀 프로젝트에서는 `.idea` 폴더를 공유하지 않도록 주의하여 각 개발자가 자신의 환경에서 독립적으로 설정하도록 해야 합니다[4][6].

Sources
[1] 자바 프로젝트를 생성하면 구성되는 폴더와 파일  ‍♂️ - problem solving https://woongcheolshin.tistory.com/56
[2] .gitignore 파일 주의사항 - 제뉴어리의 모든것 - 티스토리 https://januaryman.tistory.com/556
[3] .idea 폴더란 .gitignore 추가하는 이유 https://wotres.tistory.com/entry/idea-%ED%8F%B4%EB%8D%94%EB%9E%80-gitignore-%EC%B6%94%EA%B0%80%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0
[4] 인텔리제이 .gitignore 파일 설정 시 .idea와 .iml을 왜 제외하나요? https://honey-dev.com/%EC%9D%B8%ED%85%94%EB%A6%AC%EC%A0%9C%EC%9D%B4-gitignore-%ED%8C%8C%EC%9D%BC-%EC%84%A4%EC%A0%95-%EC%8B%9C-idea%EC%99%80-iml%EC%9D%84-%EC%99%9C-%EC%A0%9C%EC%99%B8%ED%95%98%EB%82%98%EC%9A%94/
[5] Intellij 프로젝트 폴더가 보이지 않아요.. - velog https://velog.io/@dbwjd5864/Intellij-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%ED%8F%B4%EB%8D%94%EA%B0%80-%EB%B3%B4%EC%9D%B4%EC%A7%80-%EC%95%8A%EC%95%84%EC%9A%94
[6] 인적 오류로 인한 .idea 폴더 커밋 문제 해결: .gitignore 설정의 중요성 https://pixx.tistory.com/384
[7] [Java] IntelliJ 인텔리제이 프로젝트 생성하기 & 파일구조 설정 (Mark ... https://bibi6666667.tistory.com/126
[8] [ Git ] IntelliJ 프로젝트 Git 연동 , .gitignore 설정 및 적용 방법 - velog https://velog.io/@ryusuz/Git-IntelliJ-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-Git-%EC%97%B0%EB%8F%99-.gitignore-%EC%84%A4%EC%A0%95-%EB%B0%8F-%EC%A0%81%EC%9A%A9-%EB%B0%A9%EB%B2%95
