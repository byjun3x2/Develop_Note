---
link: "[[_Git Start]]"
title: hint Using 'master' as the name for the initial branch. This default branch
source: https://www.perplexity.ai/search/hint-using-master-as-the-name-VyuylwEzSZOauwB_MYr0OA
created: 2025-12-05
tags:
  - clippings
---
경고 내용

```
(터미널에서 git init 을 했을때 나오는 메세지였고 아래 내용과 같다)

hint: Using 'master' as the name for the initial branch. This default branch name
hint: will change to "main" in Git 3.0. To configure the initial branch name
hint: to use in all of your new repositories, which will suppress this warning,
hint: call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
hint:
hint: Disable this message with "git config set advice.defaultBranchName false"

```

해당 경고 메시지는 "앞으로 새로 만드는 저장소(Repository)의 기본 브랜치 이름을 `master` 가 아닌 `main` 등으로 변경하도록 권장한다"는 내용을 담고 있다.

이 메시지가 뜨는 이유와 대처 방법은 아래와 같다

## 1\. 메시지가 뜨는 이유

과거에는 Git이 저장소를 초기화(`git init`)할 때 기본 브랜치 이름을 자동으로 `master` 로 설정했 하지만 최근에는 포용적인 용어 사용을 위해 `main` 이라는 이름을 표준으로 사용하는 추세임. 
Git 버전이 업데이트되면서 앞으로 기본값을 `master` 에서 `main` 으로 바꿀 예정이니, 사용자가 미리 설정을 변경하여 이 경고를 끄거나 새로운 관례를 따르라고 알려주는 것.

## 2\. 해결 방법 (권장)

가장 권장되는 방법은 앞으로 생성할 모든 저장소의 기본 브랜치 이름을 `main` 으로 설정하는 것.
아래 명령어를 터미널에서 한 번만 입력하면 됨.

```
bash
git config --global init.defaultBranch main
```

이렇게 설정하면 다음부터 `git init` 을 할 때 경고 메시지 없이 자동으로 `main` 브랜치가 생성됩니다.

## 3\. 이미 생성된 master 브랜치 이름 바꾸기

만약 방금 `git init` 을 실행해서 이미 `master` 브랜치가 만들어진 상태라면, 아래 명령어로 이름을 `main` 으로 변경할 수 있음.

```
bash
git branch -m master main
```

(또는 단순히 `git branch -m main` 만 입력해도 현재 브랜치 이름이 변경됩니다.)

요약하자면, Git 커뮤니티와 GitHub 등에서 `master` 대신 `main` 을 표준으로 채택하고 있어 발생하는 안내 메시지이므로, 설정을 통해 `main` 을 기본값으로 쓰시는 것을 추천함.