---
link: "[[_Javascript]]"
title: nvm 을 설치하고 node 의 lts 버전을 설치하고 yarn 을 사용하기 위해 corepack enable 을 하는데 여기서
source: https://www.perplexity.ai/search/nvm-eul-seolcihago-node-yi-lts-eUhvewvcTBulyNdYEK9IkQ
created: 2025-11-20
tags:
  - clippings
---
## nvm 을 설치하고 node 의 lts 버전을 설치하고 yarn 을 사용하기 위해 corepack enable 을 하는데 여기서 corepack이 뭔지 무슨 역할을 하는지 왜 생겨났는지 왜 필요한지 설명을 해줄래

검토됨 16개의 소스

**Corepack** 은 Node.js 개발팀이 제공하는 \*\*"패키지 매니저를 관리하는 도구"\*\*입니다. 쉽게 말해, `npm` 을 통해 `yarn` 이나 `pnpm` 같은 다른 패키지 매니저를 전역(Global)으로 설치하던 기존 방식을 대체하고, 프로젝트별로 패키지 매니저 버전을 엄격하게 관리하기 위해 만들어졌습니다.

요청하신 내용을 바탕으로 Corepack의 개념, 역할, 그리고 탄생 배경을 정리해 드립니다.

## 1\. Corepack이란 무엇인가?

Corepack은 Node.js v16.9.0(및 v14.19.0)부터 Node.js 설치 시 기본적으로 포함되어 배포되는 바이너리 도구입니다.[velog +1](https://velog.io/@dongkyun/Node-Corepack)

- **역할:**`yarn`, `pnpm` 과 같은 패키지 매니저의 실행을 \*\*중개(Proxy)\*\*합니다.
- **특징:** 사용자가 별도로 `npm install -g yarn` 을 하지 않아도, 시스템에 `yarn` 명령어를 사용할 수 있게 해줍니다. 사용자가 `yarn` 을 입력하면 Corepack이 이를 가로채서 적절한 버전의 Yarn을 실행시킵니다.[careerly +1](https://careerly.co.kr/comments/104798)

## 2\. 왜 생겨났으며, 왜 필요한가?

Corepack은 기존의 글로벌 설치 방식(`npm i -g yarn`)이 가진 **버전 파편화 문제** 와 **비효율성** 을 해결하기 위해 도입되었습니다.

## ① 프로젝트별 버전 일관성 보장 (가장 큰 이유)

과거에는 개발자 A가 Yarn v1.22를 쓰고, 개발자 B가 Yarn v3.0을 쓰고 있다면, 같은 프로젝트에서도 `lock` 파일이 깨지거나 의존성 설치 결과가 달라지는 문제가 발생했습니다.

- **Corepack 사용 시:** 프로젝트의 `package.json` 파일에 `"packageManager": "yarn@3.2.1"` 과 같이 버전을 명시할 수 있습니다.
- **결과:** 개발자가 터미널에 단순히 `yarn` 만 입력해도, Corepack이 자동으로 해당 프로젝트가 요구하는 **정확한 버전(v3.2.1)을 다운로드하여 실행** 합니다. 팀원 모두가 강제로 같은 버전을 쓰게 되는 셈입니다.[jejette.tistory +1](https://jejette.tistory.com/144)

## ② 글로벌 설치의 번거로움 제거

`nvm` 으로 Node 버전을 변경할 때마다 매번 `npm install -g yarn` 을 다시 해줘야 했던 경험이 있으실 겁니다.

- Corepack을 활성화(`corepack enable`)해두면, Node 버전을 바꿔도 별도 설치 없이 즉시 Yarn이나 PNPM 명령어를 사용할 수 있습니다. 필요한 바이너리는 Corepack이 알아서 관리하기 때문입니다.[polyframe.tistory +1](https://polyframe.tistory.com/117)

## 3\. 왜 corepack enable을 해야 하는가?

Corepack은 Node.js에 포함되어 있지만, 기본 설정상 **비활성화(Disabled)** 상태로 출고됩니다.

- 이는 기존에 사용자가 직접 설치한(`npm i -g`) 패키지 매니저와의 충돌을 방지하기 위함입니다.
- 따라서 "나는 이제 Corepack을 통해 패키지 매니저를 관리하겠다"고 선언하는 과정이 바로 `corepack enable` 명령어입니다. 이 명령어를 실행하면 Node.js 설치 경로의 `bin` 폴더에 `yarn`, `yarnpkg`, `pnpm` 등의 실행 파일(심볼릭 링크)이 생성되어 전역에서 호출할 수 있게 됩니다.[offbyone.tistory +1](https://offbyone.tistory.com/442)

---

## 요약

NVM 설치 후 `corepack enable` 을 하는 이유는 \*\*"Node 버전을 바꿀 때마다 매번 Yarn을 새로 설치하는 귀찮음을 없애고, 프로젝트마다 제각각인 Yarn/PNPM 버전을 자동으로 맞춰주기 위함"\*\*입니다.

> **참고 (2025년 동향):**  
> Corepack은 매우 유용한 도구이지만, 최근 Node.js 생태계에서는 이를 기본 번들에서 제외하거나 별도로 설치하게 하려는 논의도 있습니다. 하지만 현재 시점(2025년 11월)에서 Yarn Berry(v2+)나 최신 환경을 세팅할 때 가장 권장되는 표준 방식은 여전히 Corepack을 사용하는 것입니다.[news.hada +1](https://news.hada.io/topic?id=19970)