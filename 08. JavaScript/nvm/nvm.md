---
link: "[[_JavaScript]]"
title: nvm이 뭔지 한줄로 설명하고 왜 생겨났는지 언제 생겨났는지 단점이 있으면 그것도 기술해줘
source: https://www.perplexity.ai/search/nvmi-mweonji-hanjulro-seolmyeo-kBiT9OMoRo.PEH6HEwNjqA
created: 2025-11-20
tags:
  - clippings
---
## nvm이 뭔지 한줄로 설명하고 왜 생겨났는지 언제 생겨났는지 단점이 있으면 그것도 기술해줘

검토됨 10개의 소스

nvm(Node Version Manager)은 하나의 컴퓨터에서 다양한 Node.js 버전을 손쉽게 설치하고 필요에 따라 전환하며 관리할 수 있게 해주는 도구입니다.[velog +1](https://velog.io/@mayinjanuary/NVM-%EC%9D%B4%EB%9E%80-%EB%85%B8%EB%93%9CNode.js-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%ED%95%98%EB%8A%94-%EB%B2%95)

## nvm의 등장 배경

nvm은 여러 프로젝트가 각기 다른 Node.js 버전을 요구하는 상황에서 발생하는 호환성 문제를 해결하기 위해 만들어졌습니다. Node.js와 npm 패키지는 버전에 따라 동작 방식이 달라지는 경우가 많아, 특정 프로젝트는 구버전 Node.js에서만 작동하고 다른 프로젝트는 최신 버전을 요구할 수 있습니다. nvm이 없다면 개발자는 프로젝트를 바꿀 때마다 기존 Node.js를 삭제하고 필요한 버전을 수동으로 재설치해야 하는 번거로움이 있었습니다. nvm은 2012년경에 이러한 문제를 해결하기 위해 등장했습니다.[pozafly.github +2](https://pozafly.github.io/node/node-version-manager/)

## nvm의 단점

nvm은 유용하지만 몇 가지 단점도 존재합니다.[leapcell](https://leapcell.io/blog/ko/node-js-beojeon-tamseok-nvm-volta-fnm-simcheung-bunseok)

- **성능 저하**: nvm은 셸 스크립트 기반으로 동작하기 때문에, 터미널을 새로 열 때마다 스크립트를 실행하는 과정에서 미세한 속도 저하가 발생할 수 있습니다. Volta나 fnm 같은 최신 버전 관리 도구에 비해 속도가 느리다는 평가가 있습니다.[pozafly.github +1](https://pozafly.github.io/node/node-version-manager/)
- **수동 버전 전환**: 프로젝트 디렉터리로 이동해도 해당 프로젝트에 맞는 Node.js 버전으로 자동 전환되지 않습니다. `.nvmrc` 파일을 사용하더라도 `nvm use` 같은 명령어를 직접 실행해야 버전이 적용됩니다.[velog](https://velog.io/@sehyunny/5-node-manager-compared)
- **플랫폼 종속성**: nvm은 초기에 macOS와 Linux 환경을 위해 개발되었습니다. Windows에서는 `nvm-windows` 라는 별도의 프로젝트를 설치해야 하는 번거로움이 있습니다.[leapcell](https://leapcell.io/blog/ko/node-js-beojeon-tamseok-nvm-volta-fnm-simcheung-bunseok)
- **전역 패키지 관리**: Node.js 버전을 전환하면 해당 버전에 종속된 전역(global) 패키지들을 새로 설치해야 합니다. 버전 간에 전역 패키지가 공유되지 않아 버전 변경 시 재설치가 필요합니다.[hoho325.tistory](https://hoho325.tistory.com/457)