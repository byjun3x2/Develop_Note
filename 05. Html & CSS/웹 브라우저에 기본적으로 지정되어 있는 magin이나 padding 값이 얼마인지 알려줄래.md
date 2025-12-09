---
link: "[[_HTML & CSS]]"
title: 웹 브라우저에 기본적으로 지정되어 있는 magin이나 padding 값이 얼마인지 알려줄래
source: https://www.perplexity.ai/search/web-beuraujeoe-gibonjeogeuro-j-aLa4c5tcT.qajhMiNBnh0g
created: 2025-12-08
tags:
  - CSS
  - HTML
  - margin
  - padding
---
## 웹 브라우저에 기본적으로 지정되어 있는 magin이나 padding 값이 얼마인지 알려줄래

검토됨 17개의 소스

웹 브라우저에 지정된 기본 `margin` 이나 `padding` 값은 모든 요소에 일괄적으로 적용되는 단일 값이 아니라, 각 HTML 태그(요소)마다 브라우저(User Agent)의 기본 스타일 시트에 의해 다르게 설정됩니다.

예를 들어, 대부분의 웹 브라우저에서 `<body>` 태그는 약 8px의 `margin` 값을 가집니다. 이로 인해 웹 페이지의 콘텐츠가 브라우저 창 가장자리에 바로 붙지 않고 약간의 여백을 두고 표시됩니다. 반면 `padding` 의 기본값은 일반적으로 0입니다.

다른 요소들도 각기 다른 기본 여백 값을 가질 수 있습니다. 예를 들어, 문단 태그인 `<p>` 나 제목 태그인 `<h1>` 등은 상하 `margin` 을 기본적으로 가지고 있어 문단과 제목 사이에 자동으로 간격이 생깁니다.

이러한 브라우저별 기본 스타일이 개발에 방해가 될 수 있어, 많은 개발자들은 CSS Reset이나 Normalize.css와 같은 방법을 사용하여 모든 요소의 `margin` 과 `padding` 을 0으로 초기화한 후 작업을 시작합니다.