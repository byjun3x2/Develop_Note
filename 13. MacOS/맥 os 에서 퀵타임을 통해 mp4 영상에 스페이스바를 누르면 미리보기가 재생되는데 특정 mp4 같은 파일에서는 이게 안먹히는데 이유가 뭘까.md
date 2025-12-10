---
link: "[[_MacOS_Start]]"
title: 맥 os 에서 퀵타임을 통해 mp4 영상에 스페이스바를 누르면 미리보기가 재생되는데 특정 mp4 같은 파일에서는 이게 안먹히는데 이유가 뭘까
source: https://www.perplexity.ai/search/maeg-os-eseo-kwigtaimeul-tongh-I0Tkl_.gSoynbA1MJl9.sA
created: 2025-12-06
tags:
  - Mac
  - mp4
  - 미리보기
  - preview
---
## 맥 os 에서 퀵타임을 통해 mp4 영상에 스페이스바를 누르면 미리보기가 재생되는데 특정 mp4 같은 파일에서는 이게 안먹히는데 이유가 뭘까

4단계 완료

맥 OS의 퀵타임(QuickTime) 및 퀵룩(Quick Look, 스페이스바 미리보기)은 MP4 **컨테이너** 를 지원하지만, 그 안에 담긴 **코덱** 이나 **메타데이터 태그** 에 따라 재생 가능 여부가 결정됩니다.

특히 개발자이시고 `yt-dlp` 등을 사용하신다면 가장 유력한 원인은 **코덱 태그 불일치(hev1 vs hvc1)** 또는 **미지원 코덱(VP9/AV1)** 문제입니다.

## 1\. 가장 흔한 원인: HEVC 코덱 태그 (hev1 vs hvc1)

애플의 네이티브 플레이어(QuickTime, Preview)는 H.265(HEVC) 영상을 재생할 때, 코덱 태그가 `hvc1` 으로 지정된 파일만 공식 지원하는 경향이 있습니다.[discussions.apple +1](https://discussions.apple.com/thread/255515409)

- **현상:** 영상이 검은색으로 나오거나, 미리보기가 전혀 뜨지 않음. (VLC나 IINA에서는 잘 재생됨)
- **이유:** 윈도우나 웹 소스(혹은 `yt-dlp` 로 받은 일부 포맷)는 종종 `hev1` 태그를 사용합니다. macOS는 이를 비표준으로 간주하여 미리보기를 거부할 수 있습니다.[stackoverflow](https://stackoverflow.com/questions/32152090/encode-h265-to-hvc1-codec)

## 2\. 미지원 코덱 사용 (VP9, AV1)

MP4는 상자(Container)일 뿐입니다. `yt-dlp` 로 유튜브 영상을 받을 때 "Best Quality"를 선택하면 종종 **VP9** 이나 **AV1** 코덱으로 다운로드되는데, 이를 MP4로 포장만 바꿀 경우(remux) 문제가 발생합니다.

- **VP9:** macOS 퀵룩에서 기본 지원하지 않습니다. (유튜브의 주력 코덱)
- **AV1:** 최신 M3/M4 칩셋이나 macOS Sequoia 등에서 하드웨어 가속 지원이 추가되고 있으나, 퀵룩에서의 소프트웨어 지원은 여전히 제한적일 수 있습니다.[reddit](https://www.reddit.com/r/MacOSBeta/comments/1lg3y22/does_av1_playback_in_quicklook_work_on_tahoe_on/)

---

## 해결 방법 (개발자용)

터미널 사용이 익숙하시므로 `ffmpeg` 를 사용한 해결책을 권장합니다.

## 1\. 원인 확인하기

해당 파일이 어떤 코덱과 태그를 쓰는지 확인해보세요.

```
bash
ffprobe -v error -select_streams v:0 -show_entries stream=codec_name,codec_tag_string input.mp4
```

결과가 `hevc / hev1` 이라면 태그 문제입니다. `vp9` 이라면 코덱 호환성 문제입니다.

## 2\. 코덱 태그만 변경 (재인코딩 X, 화질 저하 X, 1초 소요)

가장 추천하는 방법입니다. 영상 데이터를 건드리지 않고 포장지의 태그만 `hev1` 에서 Apple이 좋아하는 `hvc1` 으로 바꿔줍니다.

```
bash
ffmpeg -i input.mp4 -c copy -tag:v hvc1 output.mp4
```

이 명령어를 실행한 후 `output.mp4` 를 스페이스바로 확인해보세요.[reddit +1](https://www.reddit.com/r/ffmpeg/comments/1gin9d6/hev1_vs_hvc1_is_hvc1_apple_only/)

## 3\. 코덱 변환 (재인코딩 O)

만약 코덱 자체가 VP9/AV1이라서 재생이 안 된다면, 범용성 높은 H.264로 변환해야 합니다.

```
bash
ffmpeg -i input.mp4 -c:v libx264 -crf 23 -c:a copy output.mp4
```

## 기타: 시스템 글리치 해결

파일 문제가 아니라 단순히 macOS의 미리보기 서비스가 꼬인 경우일 수도 있습니다. 이 경우 Finder를 재실행하면 해결됩니다.

- **터미널:**`killall Finder`
- **GUI:**`Option` + `Command` + `Esc` → Finder 선택 → 재실행 [discussions.apple +1](https://discussions.apple.com/thread/253305348)