---
link: "[[_Clipping]]"
title: "vite.js  react yarn berry 사용하기 (vscode 타입스크립트 오류)  4전"
source: "https://2yh-develop4jeon.tistory.com/93"
created: 2025-11-20
tags:
  - "clippings"
---
- [인스타그램](https://2yh-develop4jeon.tistory.com/#)

- 	[\[vite.js / react\] yarn berry 사용하기 (vscode 타입스크립트 오류)](https://2yh-develop4jeon.tistory.com/93)
	yarn berry는 yarn의 최신 버전(yarn 2와 그 이후의 버전)을 지칭합니다.
	PnP(Plug 'n' Play) 방식, Zero Install 방식을 지원하며 인기가 많은 패키지 관리 도구입니다.
	## | yarn berry 특징
	#### Cache와 Zero-Install
	yarn berry는 설치된 패키지를 글로벌 캐시에 저장하여,
	같은 패키지를 여러 프로젝트에서 사용할 때 다운로드 시간을 절약합니다.
	패키지는 zip 파일 형태로.yarn/cache에 저장되며,
	이를 통해 네트워크 요청 없이 빠르게 패키지를 불러올 수 있고,
	디스크 공간을 효율적으로 사용할 수 있습니다.
	또한, Zero Install 기능을 통해, 패키지들이 리포지토리에 함께 저장하며
	프로젝트를 클론 하는 것만으로 필요한 모든 패키지를 바로 사용할 수 있습니다.
	따라서 개발 환경 설정 시간을 크게 단축시킬 수 있습니다.
	#### Plug 'n' Play (PnP)
	PnP는 node\_modules 폴더를 사용하지 않고, 대신 모든 의존성 정보를.pnp.cjs 파일에 기록합니다.
	yarn은 이 파일을 통해 모듈을 해석하고 로드합니다.
	이로 인해 의존성 해석에 걸리는 시간이 줄어들게 되고, 유령 의존성 문제를 해결할 수 있습니다.
	## | 사용하기 with React.js / Vite.js
	우선 vite를 사용하여 리액트 프로젝트를 현제 폴더에 만들어 줍니다.
	```typescript
	npm create vite@latest ./
	or
	yarn create vite ./
	```
	만약 yarn create로 vite를 설치할 때
	vite은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
	라는 에러가 뜨면 create-vite 바이너리가 설치되지 않아서 그럴 가능성이 있습니다.
	따라서 create-vite를 전역으로 설치한 다음, 프로젝트 디렉터리를 초기화해 줘야 합니다.
	```typescript
	yarn global add create-vite
	yarn create vite ./
	```
	참고: [https://classic.yarnpkg.com/en/docs/cli/create](https://classic.yarnpkg.com/en/docs/cli/create)
	[
	Yarn
	Fast, reliable, and secure dependency management.
	classic.yarnpkg.com
	](https://classic.yarnpkg.com/en/docs/cli/create)
	다음으로 yarn을 사용할 때 berry 버전을 사용하기 위해 버전을 저장해 줍니다.
	```typescript
	yarn set version berry
	```
	또한 저희는 node\_modules가 없는 PnP 방식을 사용하기 위해
	.yarnrc.yml에 다음 텍스트를 추가하여 pnp 방식으로 사용하겠다 명시해 줍니다.
	```typescript
	nodeLinker: pnp
	```
	이제 패키지를 다운로드해 줍니다.
	```typescript
	yarn install
	```
	그럼.pnp.cjs 파일이 생성되고, 해당 파일에서 패키지들의 위치와 의존성을 관리하게 됩니다.
	## | 타입스크립트 오류
	만약 타입스크립트를 사용해 프로젝트를 초기화하면
	파일을 열어보면 타입 오류가 발생하는 경우가 있습니다.
	이유는 패키지들이.yarn/cache에 zip 파일로 관리되는데
	이때 타입스크립트도 zip 파일로 관리가 되고, 이를 vscode가 해석을 못 해 발생하는 오류입니다.
	따라서 vscode가 타입스크립트에 대한 정보를 알 수 있도록
	연결시켜 주기 위해 다음 명령어를 입력합니다.
	(eslint나 프리티어 사용 시에도 해당 명령어로 연결시켜 줘야 합니다.)
	```typescript
	yarn dlx @yarnpkg/sdks vscode
	```
	그럼 vscode에서 아래와 같은 메시지가 뜨는데 Allow를 눌러주면 문제가 해결됩니다.
	![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2Fm0RWB%2FbtsIzVnpP7T%2FAAAAAAAAAAAAAAAAAAAAAFBcn-cp5lMVn4ZjVlfuxY-04dT-XAYuj5EpCIcqLcrr%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3Dvmzi0cGp7g63t7ZSfYybIuVsOjg%253D)
	만약 여기서 allow를 못 눌렀다면
	컨트롤 + 시프트 + p를 누른 후 "select typescript version"을 입력 후
	use workspace version을 클릭하면 해결됩니다.
	![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FnMGkn%2FbtsIyfAEd0H%2FAAAAAAAAAAAAAAAAAAAAAMwEvXXFtJnYl01x34iufnUdar42mLUYrbP1l2OpY5Yf%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3DcrT6BIeMggdW0wXpdp5UYXG2T6E%253D)
	참고: [https://yarnpkg.com/getting-started/editor-sdks](https://yarnpkg.com/getting-started/editor-sdks)
	[
	Editor SDKs | Yarn
	An overview of the editor SDKs used to bring PnP compatibility to editors.
	yarnpkg.com
	](https://yarnpkg.com/getting-started/editor-sdks)
	드리고 Zero Install을 사용하기 위해 캐시파일을 깃허브에 다 올리게 되는데
	이때 불필요한 파일과 필요한 파일을 구분해서 올리기 위해.gitignore에 다음을 추가해 줍니다.
	```typescript
	# Zero-Installs
	.yarn/*
	!.yarn/cache
	!.yarn/patches
	!.yarn/plugins
	!.yarn/releases
	!.yarn/sdks
	!.yarn/versions
	```
	참고: [https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored](https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored)
	[
	Questions & Answers | Yarn
	A list of answers to commonly asked questions.
	yarnpkg.com
	](https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored)
	## | node\_modules 폴더가 생기는 문제
	이제 yarn dev를 실행시켜 보면 아래와 같이 node\_modules 폴더가 생깁니다.
	![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2F5nd5f%2FbtsIAbp2agZ%2FAAAAAAAAAAAAAAAAAAAAAHcTfjLrw73aEPD_MYt3LnB8LaL7JStv_Ac0LZFcxTlO%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3DY8gU1gBwQmXldCOBElkSTbBjjbQ%253D)
	이때 생기는 node\_modules 폴더는 vite.js에서 성능을 위해 미리 번들된 의존 파일이거나
	vite에 의해 생성된 어떤 다른 파일의 캐시 파일을 저장해 놓는 폴더입니다.
	기본적으로 vite는 해당 캐시 파일을 node\_modules/.vite에 저장해 두기 때문에
	node\_modules 폴더가 생기게 됩니다.
	따라서 해당 이유로 생기는 node\_modules 폴더는 그냥 신경 쓰지 않고 프로젝트를 진행하면 됩니다.
	만약 그래도 해당 폴더가 생기는 자체가 신경 쓰이고 불편하다면
	vite.config 파일에 캐시 파일들이 저장될 경로를 따로 설정해 줄 수 있습니다.
	```typescript
	import { defineConfig } from "vite";
	import react from "@vitejs/plugin-react";
	// https://vitejs.dev/config/
	export default defineConfig({
	  plugins: [react()],
	  cacheDir: "vite_cache",
	});
	```
	cacheDir 속성에 저장할 폴더 이름을 넣어주면
	![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2Fbdw5uA%2FbtsIyxaenhi%2FAAAAAAAAAAAAAAAAAAAAAIouC27mLPrJI8ft8UGpv-68M3fCIPvJ5Buv5WshXXyP%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1764514799%26allow_ip%3D%26allow_referer%3D%26signature%3DH6u4mDw8JCGj7Bb5hkzw74Xw47Q%253D)
	이런 식으로 해당 폴더에 캐시 파일이 저장됩니다.
	마지막으로 해당 폴더를.gitignore에 추가해 주면 됩니다.
	```typescript
	# Vite cache
	vite_cache
	```
	참고: [https://ko.vitejs.dev/config/shared-options.html#cachedir](https://ko.vitejs.dev/config/shared-options.html#cachedir)
	[
	Vite
	Vite, 차세대 프런트엔드 개발 툴
	ko.vitejs.dev
	](https://ko.vitejs.dev/config/shared-options.html#cachedir)
	#### '' 카테고리의 다른 글
	| [\[React\] useState와 useRef를 통한 상태 관리 (애니메이션 상태 최적화)](https://2yh-develop4jeon.tistory.com/99) (0) | 2024.12.30 |
	| --- | --- |
	| [\[React\] 리액트에서 컴포넌트 추상화에 대한 고민](https://2yh-develop4jeon.tistory.com/95) (0) | 2024.09.21 |
	| [무한 스크롤을 구현하기 위한 몇 가지 방법들 (Intersection Observer API를 사용하는 이유)](https://2yh-develop4jeon.tistory.com/92) (1) | 2024.06.17 |
	| [\[Next.js\] 프로젝트에 PWA 적용하기](https://2yh-develop4jeon.tistory.com/90) (0) | 2024.05.28 |
	| [\[Next.js, React(vite.js)\] 로컬 개발 환경 https 적용하기](https://2yh-develop4jeon.tistory.com/88) (0) | 2024.05.02 |