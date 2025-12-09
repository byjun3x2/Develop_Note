[[_Javascript]]

윈도우 , 맥 모두 사용자의 HOME Directory 아래 있는 .yarnrc 파일

내부에 

```
	nodeLinker: pnp 
```

위와 같이 설정을 해주고

프로젝트 root 경로에서 yarn set version berry 를 하고

yarn init 을 해주면

```
	.yarn
	.pnp.cjs
	package.json
	yarn.lock
```

등등의 파일이 생긴다.
