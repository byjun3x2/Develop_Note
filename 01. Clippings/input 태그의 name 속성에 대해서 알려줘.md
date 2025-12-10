---
link: "[[_Clipping]]"
title: "input 태그의 name 속성에 대해서 알려줘"
source: "https://www.perplexity.ai/search/input-taegeuyi-name-sogseonge-LlcY88vMQ1OrB2wRQgTAwg"
created: 2025-12-09
tags:
  - "clippings"
---
## input 태그의 name 속성에 대해서 알려줘

검토됨 19개의 소스

HTML `<input>` 태그의 **`name` 속성** 은 사용자가 입력한 데이터가 **서버로 전송될 때 해당 데이터의 이름표(Key)** 역할을 하는 핵심 속성입니다. 폼(Form) 제출 시 이 속성이 없으면 서버는 해당 입력값을 인식하거나 받을 수 없습니다.[tcpschool +1](http://www.tcpschool.com/html-tag-attrs/input-name)

## 주요 기능 및 특징

`name` 속성은 단순히 요소를 구별하는 것을 넘어 데이터 통신과 그룹화에 필수적인 기능을 수행합니다.

- **서버 전송 식별자 (Key 역할)**  
	폼(Form)이 제출되면 데이터는 `name=value` 쌍의 형태로 서버에 전달됩니다. 예를 들어 `<input name="username" value="user1">` 이라면 서버는 `username` 이라는 변수로 `user1` 이라는 값을 받게 됩니다. `name` 속성이 생략된 input 요소의 값은 서버로 전송되지 않습니다.[velog +2](https://velog.io/@dongeranguk/input-%ED%83%9C%EA%B7%B8-id%EC%99%80-name%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- **요소 그룹화 (Radio/Checkbox)**  
	라디오 버튼(`type="radio"`)과 같이 여러 선택지 중 하나만 골라야 하는 경우, 여러 input 태그의 `name` 값을 **동일하게 설정** 하여 하나의 그룹으로 묶어줍니다. 이렇게 하면 그룹 내에서 배타적인 선택(하나만 선택 가능)이 가능해집니다.[play-with.tistory +1](https://play-with.tistory.com/366)
- **자바스크립트 접근**  
	자바스크립트에서 `document.getElementsByName('이름')` 을 통해 해당 `name` 을 가진 요소들을 배열 형태로 한 번에 선택하거나 제어할 수 있습니다.[sangseek +1](https://sangseek.com/communities/18595)

## id 속성 vs name 속성 비교

개발 과정에서 자주 혼용되는 `id` 와 `name` 의 차이점은 다음과 같습니다.

| 구분 | `id` 속성 | `name` 속성 |
| --- | --- | --- |
| **주 목적** | **식별 및 스타일링** (CSS/JS 제어용) | **데이터 전송** (서버 통신용) |
| **중복 여부** | 페이지 내에서 **유일해야 함** (중복 불가) | **중복 가능** (Radio 버튼, 배열 데이터 등) |
| **서버 전송** | 전송되지 않음 | **Parameter Key** 로 전송됨 |
| **필수 여부** | 필요 시 사용 | 폼 전송 시 **필수** |

[seolhee2750.tistory +2](https://seolhee2750.tistory.com/249)

## 사용 예시

다음은 `name` 속성이 서버 전송과 그룹화에 어떻게 쓰이는지 보여주는 예시입니다.

```
xml
<form action="/submit" method="get">
  <!-- 1. 서버 전송용 이름표 -->
  <label>아이디: <input type="text" name="user_id"></label>
  
  <!-- 2. 라디오 버튼 그룹화 (name이 같아야 하나만 선택됨) -->
  <p>성별:</p>
  <label><input type="radio" name="gender" value="male"> 남성</label>
  <label><input type="radio" name="gender" value="female"> 여성</label>
  
  <button type="submit">제출</button>
</form>
```

위 폼을 제출하면 서버(URL)로 다음과 같은 데이터가 전송됩니다:  
`?user_id=입력값&gender=선택값` [tcpschool +1](http://www.tcpschool.com/html-tag-attrs/input-name)