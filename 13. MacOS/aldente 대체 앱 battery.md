[[_MacOS_Start]]

aldente 라는 MacOS 어플리케이션은 맥북의 배터리 충전 제한을 걸어두는 앱이다.

이렇게 어플리케이션을 사용하면서도 배터리 충전을 제한하는 이유는

다음과 같은 리튬 이온 배터리의 화학적 특성 때문이다.

- 전압 스트레스 감소: 리튬 이온 배터리는 100% 완충 상태(높은 전압)나 0% 방전 상태에서 내부 화학 물질이 가장 큰 스트레스를 받음
    
- **스윗 스팟(Sweet Spot) 유지:** 배터리 효율이 가장 좋고 수명 저하가 적은 구간은 대략 **20%~80%** 사이라고 알려져 있다. AlDente는 강제로 충전을 80%에서 멈추게 하여 배터리가 고전압 상태에 머무는 시간을 원천 차단한다.

2025년 말 알덴테 앱은 무료기능의 제한을 더 크게 하여 기존에 가능했던
Mac 의 dock 에 아이콘을 생략할 수 있는 기능을 제한했고
심지어 macOS 진입시 앱 시작을 볼 수 있는 기능도 제한했다

따라서 아래와 같은 오픈 소스를 추천한다.

```cardlink
url: https://github.com/actuallymentor/battery
title: "GitHub - actuallymentor/battery: CLI/GUI for managing the battery charging status for Apple silicon (M1, M2, M3) Macs"
description: "CLI/GUI for managing the battery charging status for Apple silicon (M1, M2, M3) Macs - actuallymentor/battery"
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://opengraph.githubassets.com/3fff406a673d02d3518b3be8fd5cc2dbca8988071925de63572448f0e0389da6/actuallymentor/battery
```


gui 버전의 경우 압축을 풀고 어플리케이션 파일을 macos 의 application 폴더에 가져다 두면 될 듯 싶다.