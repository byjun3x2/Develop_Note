---
link: "[[_JavaScript]]"
title: _yarn 폴더 안의 unplugged 폴더의 정체를 알려줘
source: https://www.perplexity.ai/search/yarn-poldeo-anyi-unplugged-pol-A7UDiIeAR1CuIzrfD2XTVA
created: 2025-11-20
tags:
  - clippings
---
## .yarn 폴더 안의 unplugged 폴더의 정체를 알려줘

검토됨 10개의 소스

`.yarn/unplugged` 폴더는 Yarn Berry(v2+)의 PnP(Plug'n'Play) 모드에서 **압축을 푼 패키지들이 저장되는 공간** 입니다.

보통 Yarn Berry는 패키지를 `.yarn/cache` 폴더에 Zip 파일 형태로 압축해서 관리하지만, 기술적인 이유로 압축을 풀어야만 동작하는 예외적인 패키지들이 이곳에 저장됩니다.

주요 특징과 생성 원인은 다음과 같습니다.

## 1\. 생성 원인 (왜 압축을 푸는가?)

대부분의 자바스크립트 패키지는 압축된 상태(Zip)에서도 바로 읽어올 수 있지만, 다음과 같은 경우에는 반드시 파일 시스템에 실제 파일 형태로 존재해야 합니다.

- **바이너리 실행 파일 포함**: `.bin` 스크립트나 C++ 등으로 빌드된 네이티브 모듈은 운영체제가 직접 실행해야 하므로 Zip 내부에서는 실행될 수 없습니다.[imch +1](https://imch.dev/posts/commitizen-with-yarn-pnp/)
- **Shell Script 사용**: 특정 패키지가 쉘 스크립트를 통해 다른 파일을 참조해야 할 경우, 실제 경로가 필요합니다.[imch](https://imch.dev/posts/commitizen-with-yarn-pnp/)
- **수동 디버깅**: 개발자가 `yarn unplug [패키지명]` 명령어를 사용해 특정 패키지의 코드를 직접 수정하거나 디버깅하려고 강제로 압축을 푼 경우입니다.[imch](https://imch.dev/posts/commitizen-with-yarn-pnp/)

## 2\. Git 관리 여부 (.gitignore)

이 폴더는 **Git에 올리지 않는 것이 권장** 됩니다 (`.gitignore` 에 추가).

- **이유**: 이곳에 있는 파일들은 대부분 플랫폼(OS)에 종속적인 바이너리 파일이거나, `.yarn/cache` 의 Zip 파일로부터 언제든지 다시 생성할 수 있는 중복 데이터이기 때문입니다.[reddit](https://www.reddit.com/r/node/comments/ez3krb/unplugged_in_yarn_2/)
- **Zero-Install 사용 시**: Zero-Install을 쓰더라도 `.yarn/cache` 와 `.pnp.cjs` 등은 커밋하지만, `.yarn/unplugged` 는 무시하도록 설정하는 것이 일반적입니다.[reddit](https://www.reddit.com/r/node/comments/ez3krb/unplugged_in_yarn_2/)

## 3\. 요약

- **역할**: Zip 실행이 불가능한 패키지들을 위해 **"압축을 풀어놓은(Unplugged)"** 전용 공간
- **관리**: 일반적으로 **Git 버전 관리에서 제외** 대상