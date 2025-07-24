[[_React]]

```Javascript

import React from "react";  
import {BrowserRouter, Routes, Route} from 'react-router-dom';  
import MyButton from "./MyButton";  
import AboutPage from "./AboutPage";  
import Profile from "./Profile";  
import Home from "../pages/Home";  
import MapTest from "../pages/MapTest";  
import NotFound from "../pages/NotFound";  
  
export default function App() {  
    const [show, setShow] = React.useState(false);  
  
    function showImg() {  
        console.log("showImg");  
  
        if (show) {  
            console.log(show);  
            setShow(false);  
  
        } else {  
            setShow(true);  
        }  
    }  
  
  
    return (  
  
        <BrowserRouter>  
            <div>  
				<h1>Welcome to my app</h1>  
                <MyButton props={showImg}/>  
                {show ? <Profile/> : ""}  
                <AboutPage/>  
                =============================================  
            </div>  
  
            <Routes>                
	            <Route path="/" element={<Home/>}/>  
                <Route path="*" element={<NotFound/>}/>  
                <Route path="/how" element={<MapTest/>}/>  
            </Routes>
		</BrowserRouter>    );  
}
```

사건의 발단 
cra 로 리액트 앱을 구성하지 않고 webpack 을 통해서 수작업으로 리액트 앱을 구성하고 라우팅 연습을 하기 위해서
BrowserRouter 를 사용하는 도중에 
아무리 해도 라우팅이 동작을 하지 않는 상황이 발생

원인은 webpack.config.js 파일 안에 있는 webpack devserver 부분에 있었다.

historyApiFallback: true, 으로 지정해야 정상 작동을 한다.

cursor 에디터에서는 일단 아래와 같이 설명을 하긴 했다.

# React routing 404 error troubleshooting
_Exported on 2025. 7. 24. at 18시 27분 13초 GMT+9 from Cursor (1.2.4)_

---

**User**

App.jsx 에서 * 으로 접근하는 라우트와 how로 접근하는 라우트 모두 작동을 안하고 404 에러를 띄우는데

---

**Cursor**

react-router-dom을 사용할 때, 라우트가 정상적으로 작동하지 않고 404 에러가 뜨는 경우는 주로 다음과 같은 원인 때문입니다:

1. **라우터가 올바르게 감싸져 있지 않음**
2. **정적 파일 서버(예: webpack dev server, Vercel, Netlify 등)의 설정 문제**
3. **라우트 경로 오타 또는 컴포넌트 문제**
4. **잘못된 import 또는 export**

현재 코드를 보면, App.jsx에서 라우트 설정 자체는 크게 문제 없어 보입니다.  
하지만, 아래 사항을 점검해보세요.

---

### 1. public/index.html 설정 확인

SPA(싱글 페이지 앱)에서 새로고침 시 404가 뜨는 경우, 서버가 모든 경로를 index.html로 리다이렉트해야 합니다.  
개발 환경(webpack dev server)에서는 보통 자동으로 처리되지만, 배포 환경에서는 별도 설정이 필요합니다.

#### 개발 환경에서라면:
- webpack.config.js에 아래 설정이 있는지 확인하세요.

```js
devServer: {
  historyApiFallback: true,
  // ...기타 설정
}
```

---

### 2. 라우트 경로 확인

- `/how`로 접근하면 `<MapTest />`가 보여야 하고,
- 그 외의 모든 경로는 `<NotFound />`가 보여야 합니다.

경로 설정은 올바르게 되어 있습니다.

---

### 3. import 경로 및 파일명 확인

- `pages/MapTest.jsx`, `pages/NotFound.jsx` 파일이 실제로 존재하는지,
- 컴포넌트가 `export default`로 잘 내보내지고 있는지 확인하세요.

---

### 4. 브라우저 새로고침 시 404

- 개발 서버가 SPA 라우팅을 지원하지 않으면, 새로고침 시 404가 뜹니다.
- 위 1번의 `historyApiFallback` 설정이 필요합니다.

---

### 5. 실제 증상 확인

- 주소창에 `/how` 입력 후 엔터 → 404 발생
- 주소창에 `/아무거나` 입력 후 엔터 → 404 발생

이 경우, 개발 서버 설정 문제일 가능성이 높습니다.

---

## 해결 방법

1. **webpack.config.js** 파일을 열어 아래 설정이 있는지 확인하세요.

```js
// webpack.config.js
module.exports = {
  // ...기존 설정
  devServer: {
    historyApiFallback: true,
    // ...기타 설정
  },
};
```

2. 설정 후 개발 서버를 재시작하세요.

---

### 추가로, 배포 환경이라면

- Netlify: `_redirects` 파일에 `/*    /index.html   200` 추가
- Vercel: `vercel.json`에 rewrite 설정 필요

---

궁금한 점이나 추가로 확인하고 싶은 부분이 있으면 말씀해 주세요!  
필요하다면 webpack.config.js 파일을 보여주시면 더 정확히 안내해드릴 수 있습니다.

```javascript
devServer: {
  historyApiFallback: true,
  // ...기타 설정
}
```

```javascript
// webpack.config.js
module.exports = {
  // ...기존 설정
  devServer: {
    historyApiFallback: true,
    // ...기타 설정
  },
};
```

---

**User**

historyApiFallback: true, 이 무슨 역할을 하는지 어떤 원리인지 알려줄래 근본적인 원리? 뭐 그런거

---

**Cursor**

좋은 질문입니다!  
`historyApiFallback: true`의 근본적인 원리와 역할을 쉽게 설명해드릴게요.

---

## 1. SPA(싱글 페이지 애플리케이션)와 라우팅

React로 만든 SPA는 실제로는 **index.html 하나만**을 서버에서 내려받고,  
이후의 모든 페이지 이동(라우팅)은 **브라우저에서 자바스크립트로** 처리합니다.

예시:
- `/` → index.html + JS로 Home 렌더링
- `/how` → index.html + JS로 MapTest 렌더링

---

## 2. 문제의 원인

브라우저 주소창에 `/how`를 입력하고 새로고침하면,  
**서버는 `/how`라는 실제 파일이나 폴더를 찾으려고 시도**합니다.

- 만약 `/how`라는 파일이 없으면, 서버는 404(파일 없음) 에러를 반환합니다.
- 하지만 SPA에서는 `/how`도 결국 index.html을 내려주고,  
  JS가 알아서 어떤 컴포넌트를 보여줄지 결정해야 합니다.

---

## 3. historyApiFallback의 역할

`historyApiFallback: true`는  
**서버가 모르는 경로로 요청이 들어오면, 무조건 index.html을 반환**하도록 만듭니다.

즉,
- `/how`로 요청이 오면 → 서버는 index.html을 반환
- `/about`로 요청이 오면 → 서버는 index.html을 반환
- `/`로 요청이 오면 → 서버는 index.html을 반환

이렇게 하면,  
브라우저가 새로고침을 하거나 직접 경로를 입력해도  
항상 index.html이 내려가고,  
React Router가 그 경로에 맞는 컴포넌트를 보여줍니다.

---

## 4. 근본적인 원리 (왜 필요한가?)

- **SPA는 서버가 아닌, 클라이언트(브라우저)에서 라우팅을 처리**합니다.
- 하지만 브라우저 주소창에 직접 경로를 입력하면,  
  서버는 그 경로에 해당하는 파일을 찾으려고 합니다.
- 서버가 모르는 경로는 404가 되기 때문에,  
  **모든 경로를 index.html로 fallback(대체)시켜야**  
  SPA 라우팅이 정상적으로 동작합니다.

---

## 5. 이름의 의미

- **history**: HTML5의 History API (pushState, replaceState 등)를 사용한 라우팅
- **ApiFallback**: 서버가 모르는 경로로 요청이 오면, fallback(대체)해서 index.html을 반환

---

### 요약

> historyApiFallback: true  
> → 서버가 모르는 경로로 요청이 오면, index.html을 반환해서  
> SPA 라우팅이 항상 정상 동작하도록 해주는 설정

---
