---
link: "[[_IDE Setting Start]]"
title: IntelliJ 소스 루트 폴더 설정법
source: https://www.perplexity.ai/search/intellij-eseo-teugjeong-poldeo-ij5goMA.TVi_TQHF8Hs5JQ
author:
  - "[[Perplexity AI]]"
published: 
created: 2025-03-04
description: Perplexity is a free AI-powered answer engine that provides accurate, trusted, and real-time answers to any question.
tags:
  - Intellij
  - IDE
  - JAVA
  - sourceroot
  - source
---
IntelliJ IDEA에서 자바 패키지를 생성할 수 있는 폴더와 그렇지 않은 폴더의 차이는 다음과 같습니다:

## 패키지 생성 가능 폴더

**소스 루트(Source Root)로 지정된 폴더**에서만 자바 패키지를 생성할 수 있습니다. 이러한 폴더는 다음과 같은 특징이 있습니다:

- 파란색 폴더 아이콘으로 표시됩니다.
- 주로 `src/main/java` 경로에 위치합니다.
- 컴파일 대상이 되는 자바 소스 코드 파일들이 위치합니다.

## 패키지 생성 불가능 폴더

소스 루트로 지정되지 않은 폴더에서는 자바 패키지를 생성할 수 없습니다. 이러한 폴더는:

- 일반적인 노란색 폴더 아이콘으로 표시됩니다.
- 리소스 파일이나 기타 프로젝트 관련 파일들이 위치할 수 있습니다.

## 소스 루트 지정 방법

일반 폴더를 소스 루트로 지정하려면:

1. 해당 폴더를 우클릭합니다.
2. "Mark Directory as" > "Sources Root"를 선택합니다[^2][^5].

또는:

1. File > Project Structure로 이동합니다.
2. Modules 탭에서 원하는 폴더를 선택하고 "Sources" 항목을 체크합니다[^6].

이렇게 설정하면 IntelliJ IDEA가 해당 폴더를 컴파일 대상 소스 코드가 위치한 곳으로 인식하게 되어 패키지 생성이 가능해집니다[^1][^5].

특정 폴더에 자바 패키지를 생성할 때 어떤 설정이 필요한지

IntelliJ에서 패키지를 생성할 때 주의해야 할 점은 무엇인지

IntelliJ에서 패키지를 생성할 때 사용할 수 있는 단축키는 무엇인지

IntelliJ에서 패키지를 생성할 때 디렉토리 구조가 어떻게 변하는지

IntelliJ에서 패키지를 생성할 때 에러가 발생하는 이유는 무엇인지

---

[^1]: https://stackoverflow.com/questions/41638654/java-project-folder-structure-in-intellij-idea

[^2]: https://hianna.tistory.com/783

[^5]: https://burn.eone.one/blog/2024/235/intellij-java-new-project/

[^6]: https://timotimo.tistory.com/132