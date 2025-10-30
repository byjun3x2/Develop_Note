---
link: "[[_Clipping]]"
title: "맥북에서 GitHub 계정 여러개 사용하는 방법!"
source: "https://somjang.tistory.com/entry/%EB%A7%A5%EB%B6%81%EC%97%90%EC%84%9C-GitHub-%EA%B3%84%EC%A0%95-%EC%97%AC%EB%9F%AC%EA%B0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95"
created: 2025-10-30
tags:
  - "clippings"
---
[본문 바로가기](https://somjang.tistory.com/entry/#dkBody)

---

**관리 메뉴**
- [글쓰기](https://somjang.tistory.com/manage/entry/post "글쓰기")
- [방명록](https://somjang.tistory.com/guestbook "방명록")
- [관리](https://somjang.tistory.com/manage "관리")

## 솜씨좋은장씨

## 맥북에서 GitHub 계정 여러개 사용하는 방법! 본문

### 맥북에서 GitHub 계정 여러개 사용하는 방법!

솜씨좋은장씨 2021. 8. 18. 20:29

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FcVjk1r%2Fbtrcs78UpHu%2FAAAAAAAAAAAAAAAAAAAAANSsumBNv4DA3_GO5MhxRocMw5FilPLr7buFPx73i5Ad%2Fimg.jpg%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3DzNyN4Mm0J9EzwrXcVM0OC0Uu%252BUs%253D)

이번 글에서는 최근 Git에서 GitHub 계정 로그인 방식이 패스워드 로그인 방식에서 Token 방식으로 변경되어

[2021.08.14 - \[유용한 정보/Git | GitHub\] - \[GitHub\] The requested URL returned error: 403 해결 방법! ( feat. macOS )](https://somjang.tistory.com/entry/GitHub-The-requested-URL-returned-error-403-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-feat-macOS)

포스팅을 한 겸사겸사!

또 Token 방식은 기한이 무제한이 아니라 일정 기간마다 다시 발급을 받아야한다는 점에서!

예전부터 해보고 싶었던 하나의 맥북에서 여러개의 GitHub 계정을 사용할 수 있는 설정을 해보고

이를 글로 남겨보기로 했습니다.

보통 회사의 계정과 본인 개인 계정 2개를 번갈아 가면서 사용하길 희망하시거나

아니면 따로 2개 이상의 계정을 운영하는 경우 이 방법을 추천 드립니다.

방법은 다음과 같습니다.

#### 1\. ssh-key 생성

먼저 **ssh 라는 이름을 가진 숨김 폴더로 이동** 합니다.

위치는 홈 디렉토리 ( ~ ) 에 위치해 있습니다.

만약 **존재하지 않는 다면 생성후에 이동** 하면 됩니다.

```bash
// 만약 ssh 폴더가 존재하지 않는다면 $ mkdir ~/.ssh 먼저 실행 후 진행
$ cd ~/.ssh
```

이동하였다면 이제 ssh-key를 생성합니다.

생성 명령어는 다음과 같습니다.

```bash
$ ssh-keygen -t [암호화 방식] -b [생성할 key의 크기] -C 'GitHub계정 등록 메일 주소'
```

하나씩 살펴보면 다음과 같습니다.

| **구분** | **내용** | **비고** |
| --- | --- | --- |
| **암호화 방식** | ssh-key의 암호화 방식 | rsa 방식 사용 |
| **생성할 Key의 크기** | 기본 3072 - 최대 4096 |  |
| **GitHub 계정 등록 메일 주소** | GitHub 생성 시 등록에 사용한 메일 주소 | 확인방법   우측 상단 프로필 이미지 클릭   \> Settings > Emails   \> Primary로 표시되어있는 메일 주소 |

그럼 위의 방법을 예시로 rsa 방식의 크기는 4096 그리고 GitHub 계정 등록 메일 주소가 jjdh11117@gmail.com 인

ssh-key를 생성한다고 하면 아래와 같습니다.

```bash
$ ssh-keygen -t rsa -b 4096 -C 'jjdh11117@gmail.com'
```

위의 명령어를 실행하면

```bash
Generating public/private rsa key pair.
```

public/private rsa key pair를 생성중이라는 내용이 나오고 잠시 기다리면

```bash
Enter file in which to save the key (/Users/donghyunjang/.ssh/id_rsa):
```

생성할 파일의 이름을 적어달라고 나옵니다.

이 때 그냥 엔터를 치면 id\_rsa로 저장되고 그렇지 않으면 내가 입력한 값이 저장됩니다.

저는 개인 계정은 id\_rsa\_somjang 회사 계정은 id\_rsa\_somjang\_work 로 설정하였습니다.

이 이름은 본인이 원하는 값을 마음대로 정하여 설정해주면 됩니다.

```bash
Enter passphrase (empty for no passphrase):
```

이름을 설정하고나면 해당 계정의 비밀번호를 입력하라고 나옵니다.

이 때 엔터를 눌러 넘어갑니다.

```bash
Enter same passphrase again:
```

또 한번 더 입력하라고 나오면 또 엔터를 눌러 넘어갑니다.

```bash
Your identification has been saved in id_rsa_somjang
Your public key has been saved in id_rsa_somjang.pub
The key fingerprint is:
SHA256:sha256sha256sha256sha256 jjdh11117@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|       .+*SO=    |
|         ..oM=.  |
|        o. ==+ . |
|       . Jan. .  |
|      o G o      |
|   o o + o .     |
|  o o = * +      |
|   o.. = G .     |
|   oo .   d      |
+----[SHA256]-----+
```

그리고 위와 같은 형태의 값이 출력되면 제대로 생성이 된 겁니다.

ls 명령어를 통해 잘 생성되었는지 확인해보면

```bash
$ ls
> id_rsa_somjang.pub    id_rsa_somjang
```

.pub 파일과 그냥 파일이 생성된 것을 볼 수 있습니다.

.pub 파일은 공개 ssh 파일 그냥 파일은 비공개 파일입니다.

GitHub에 등록할때는.pub 파일을 활용하여 등록합니다.

위와 같은 방법으로 다른 계정도 동일하게 ssh-key를 생성해주면 됩니다.

2개 계정에 대해서 생성했다면.pub 파일 그냥파일 2개 1쌍으로 2개의 쌍이 생성 되었을겁니다.

#### 2\. ssh-key 등록

이제 키를 생성했다면 이제 이 키를 등록해줄 차례입니다.

등록하는 방법은 ssh-add 명령어와 생성한 ssh-key의 경로를 활용하여 등록합니다.

```shell
$ ssh-add [생성한 ssh-key의 경로]
```

위의 방법을 통해 제 케이스에 대입해서 직접해보면 다음과 같습니다.

```shell
$ ssh-add ~/.ssh/id_rsa_somjang
```

명령어를 실행했을때

```shell
Identity added: /Users/donghyunjang/.ssh/id_rsa_somjang (jjdh11117@gmail.com)
```

위와 같이 나온다면 정상입니다.

```shell
Could not open a connection to your authentication agent.
```

만약 위와 같은 오류가 발생한다면

```shell
$ eval $(ssh-agent)
```

위와 같은 명령어로 ssh-agent를 실행하고 다시 실행하시면 됩니다.

#### 3\. ssh config 파일 작성

config 파일은 아까 ssh-key를 생성했던 위치인 ~/.ssh 위치에서 생성합니다.

```shell
$ vi ~/.ssh/config
```

vi 명령어를 통하여 config파일을 생성하고

```shell
#  깃헙계정 work
#  -------------------
Host github.com-work
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_somjang_work
  User SOMJANG-42MARU

# 깃헙계정 study
#  -------------------
Host github.com-somjang
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_somjang
  User SOMJANG
```

위와 같이 작성합니다.

작성하는 내용을 하나씩 살펴보면 다음과 같습니다.

| **구분** | **내용** | **비고** |
| --- | --- | --- |
| **Host github.com-\[사용할 이름\]** | 본인이 원하는 이름 지정 | 앞으로 자주 쓸 이름이므로   최대한 기억에 남는 이름으로 지정 필요! |
| **HostName** | github.com |  |
| **IdentityFile** | ssh-key 파일 경로 |  |
| **User** | GitHub 계정 이름 |  |

#### 4\. GitHub 계정 SSH 설정

먼저 생성한 ssh-key를 등록할 GitHub 계정 설정 페이지로 이동합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FoAEaU%2Fbtrcs9MNCaX%2FAAAAAAAAAAAAAAAAAAAAAKUwrjEP_cNXSFvn6fgjTJLqj8Z5Qv_SCsPn6yjTmFP_%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3DnLMxQB28qkkTNFioO3OLB9eS3N0%253D)

우측 상단에 있는 프로필 이미지를 클릭하고 Settings를 클릭합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FywmQM%2FbtrcB3cwwjo%2FAAAAAAAAAAAAAAAAAAAAALNKqFBd2xXWEhtMJf07nTDMER2oolVGwGMid1DW0cSi%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3DAZ942uqDymkYbEvZj4GmQC9MTOE%253D)

좌측 배너에서 SSH and GPG keys 메뉴를 선택하고 SSH keys 의 New SSH key를 클릭하여

새로운 SSH key를 설정합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FbnBqD5%2FbtrcB4icw3x%2FAAAAAAAAAAAAAAAAAAAAAGJcDtabnfKZrfB4PBIx_uePLWalCSTxw2qxVZaPZBFQ%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3D154rRMUouT3FRSidfxX8fwVZj1M%253D)

| **구분** | **내용** | **비고** |
| --- | --- | --- |
| **Title** | 본인이 원하는 이름 지정 | 나중에 봤을때 어떠한 키인지 구분 가능하도록 작성 |
| **Key** | 1번에서 생성한 ssh-key의 값 | cat ~/.ssh/id\_rsa\_somjang   ( cat ~/.ssh/ \[ 생성한 ssh-key 이름 \] )   을 실행하면 나오는 값 복사 > 붙여넣기 |

**Key 예시**

```shell
$ cat id_rsa_somjang.pub 
ssh-rsa RSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgabRSAgab+RSAgab+RSAgabRSAgab++RSAgab/RSAgab+RSAgab+RSAgab+RSAgab== jjdh11117@gmail.com
```

내용을 작성하였다면 Add SSH Key를 눌러 설정을 누르고

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FcxOagb%2FbtrcxJsPXwq%2FAAAAAAAAAAAAAAAAAAAAAI5ZW0B5IQ3iSo0bk-bx-YDWSdKWObahldcA5L-9k8tl%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3De%252FjAiM4aFQGGTo8bT2XzTbaQnMI%253D)

비밀번호를 입력하여 설정을 완료합니다.

설정이 완료되면

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FwuXMu%2FbtrczJTo3qi%2FAAAAAAAAAAAAAAAAAAAAAInXry1Dsf9oIqrSY5f3K9YbZ7n4RsVIDb6-Q-s2DZbI%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3DTnjKPJx8OpE%252FmeJx%252B13BoGq1PaE%253D)

위와 같이 설정된 키의 모습이 보입니다.

1번에서 생성했던 키들을 동일한 방법으로 모두 설정해줍니다.

#### 5\. 설정이 제대로 되었는지 확인하는 방법

이렇게 설정을 하였다면 과연 제대로 설정이 되었는지 확인해볼 필요가 있습니다.

```shell
$ ssh -T git@github.com-[3번에서 github.com-(지정값) 여기서 지정한 지정값]
```

확인은 위와 같은 명령어로 진행합니다.

저는 github.com-somjang / github.com-work 이 두가지로 설정을 하였으므로

```shell
$ ssh -T git@github.com-somjang
$ ssh -T git@github.com-work
```

위 처럼 확인을 하면 됩니다.

명령어를 실행하면

```shell
The authenticity of host 'github.com (15.164.81.167)' can't be established.
RSA key fingerprint is SHA256:sha256sha256sha256sha256sha256sha256sha256
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

위와 같이 계속 연결하겠냐는 질문이 나오고 yes를 입력하면됩니다.

```shell
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
Hi SOMJANG! You've successfully authenticated, but GitHub does not provide shell access.
```

그떄 위와 같은 내용이 나오면 설정 완료!

#### 6\. ssh-key를 활용하여 GitHub 프로젝트 설정하기!

저는 기존에 맥에서 관리하던 [코딩 1일 1문제](https://github.com/SOMJANG/CODINGTEST_PRACTICE) 프로젝트를 이 ssh-key를 활용해서 다시 설정해보기로 했습니다.

먼저 GitHub 의 해당 레포지토리 페이지로 이동합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2Fc76ZVJ%2FbtrcB4oYYY1%2FAAAAAAAAAAAAAAAAAAAAAIDZUuFizfD0Q6TlTzzjiEN0Q_2APWlBMlOy10MueMZ7%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1761922799%26allow_ip%3D%26allow_referer%3D%26signature%3Du5T3RFT4jUHpHwNHaKpZGSn1Cd0%253D)

이동 후에 평소처럼 초록색 Code 버튼을 클릭하는데

이제 HTTPS가 아닌 SSH 를 클릭하고 그 값을 복사합니다.

복사한 값을 보면

```shell
git@github.com:SOMJANG/CODINGTEST_PRACTICE.git
```

위와 같은데 아까 3번에서 SOMJANG 계정에 대한 설정을 github.com-somjang으로 했으므로

이 복사한 값을

```shell
git@github.com-somjang:SOMJANG/CODINGTEST_PRACTICE.git
```

위와 같이 수정하여 사용하면 됩니다.

이 복사한 값을 어떻게 사용하느냐

**신규 프로젝트일 경우**

```shell
$ git remote add origin git@github.com-somjang:SOMJANG/CODINGTEST_PRACTICE.git
```

**신규 프로젝트를 Clone 할 경우**

```shell
$ git clone git@github.com-somjang:SOMJANG/CODINGTEST_PRACTICE.git
```

**기존 프로젝트일 경우**

```shell
$ git remote set-url origin git@github.com-somjang:SOMJANG/CODINGTEST_PRACTICE.git
```

위와 같이 사용하면 됩니다.

읽어주셔서 감사합니다.

모두 ssh-key 설정으로 편한 개발 환경 구축하시길 바랍니다~

#### ' > ' 카테고리의 다른 글

| [\[GitHub\] 내 블로그 최신글 깃헙 프로필에 자동으로 표시하는 방법! ( feat. Python / GitHub Actions )](https://somjang.tistory.com/entry/GitHub-%EB%82%B4-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EC%B5%9C%EC%8B%A0%EA%B8%80-%EA%B9%83%ED%97%99-%ED%94%84%EB%A1%9C%ED%95%84%EC%97%90-%EC%9E%90%EB%8F%99%EC%9C%BC%EB%A1%9C-%ED%91%9C%EC%8B%9C%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-feat-Python-GitHub-Actions) (6) | 2021.08.22 |
| --- | --- |
| [\[GitHub\] commit 메세지에 이모티콘 넣는 방법! 🤩](https://somjang.tistory.com/entry/GitHub-commit-%EB%A9%94%EC%84%B8%EC%A7%80%EC%97%90-%EC%9D%B4%EB%AA%A8%ED%8B%B0%EC%BD%98-%EB%84%A3%EB%8A%94-%EB%B0%A9%EB%B2%95-%F0%9F%A4%A9) (0) | 2021.08.21 |
| [\[GitHub\] The requested URL returned error: 403 해결 방법! ( feat. macOS )](https://somjang.tistory.com/entry/GitHub-The-requested-URL-returned-error-403-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-feat-macOS) (0) | 2021.08.14 |
| [\[GitHub\] GitHub 프로필에 내 commit 시간 기록 남겨보기!](https://somjang.tistory.com/entry/GitHub-GitHub-%ED%94%84%EB%A1%9C%ED%95%84%EC%97%90-%EB%82%B4-commit-%EC%8B%9C%EA%B0%84-%EA%B8%B0%EB%A1%9D-%EB%82%A8%EA%B2%A8%EB%B3%B4%EA%B8%B0)(0) | 2021.07.01 |
| [\[Git\] Git의 기본 branch를 master에서 main으로 변경하는 방법!](https://somjang.tistory.com/entry/Git-Git%EC%9D%98-%EA%B8%B0%EB%B3%B8-branch%EB%A5%BC-master%EC%97%90%EC%84%9C-main%EC%9C%BC%EB%A1%9C-%EB%B3%80%EA%B2%BD%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)(2) | 2021.06.28 |

Tag

, , , , , , , , ,

**14 Comments**

[솜씨좋은장씨](https://somjang.tistory.com/) [솜장이 직접 경험해보고 공유하는 개발, 맛집, 각종 리뷰 공유 블로그!🤩](https://somjang.tistory.com/)

- 익명 2021.08.18 21:06 비밀댓글입니다.
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2021.08.18 21:06 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6195340) 감사합니다~
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6195340) [수정/삭제](https://somjang.tistory.com/entry/#none)
- 최고에요 2022.01.17 14:52 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6326749) 정말 최고입니다!! 예시가 정말 도움 됐어요
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.01.17 15:05 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6326768) 감사합니다~
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6326768) [수정/삭제](https://somjang.tistory.com/entry/#none)
- [두라미](https://durami.tistory.com/) 2022.02.24 09:51 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6366985) 복 받으세요
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.02.24 09:54 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6366990) 감사합니다~ 복 많이 받으세요~!
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6366990) [수정/삭제](https://somjang.tistory.com/entry/#none)
- SHSF 2022.03.06 00:19 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6376839) 넘나 감사합니다! 정말 많은 도움이 됐습니다.
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.03.06 08:52 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6376934) 감사합니다~~ 즐거운 주말 보내세요!
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6376934) [수정/삭제](https://somjang.tistory.com/entry/#none)
- [sunnmerday](https://42ssss.tistory.com/) 2022.04.20 17:58 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6417362) 정말 감사합니다 ㅠㅠ~~
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.04.22 16:22 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6419006) 감사합니다🥲
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6419006) [수정/삭제](https://somjang.tistory.com/entry/#none)
- [stuckyi](https://ziyun.tistory.com/) 2022.09.25 16:47 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6558163) 덕분에 문제 해결했습니다! 감사합니다!
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.09.25 23:04 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6558646) 감사합니다~
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6558646) [수정/삭제](https://somjang.tistory.com/entry/#none)
- [쑥라떼:\]](https://sook-latte.tistory.com/) 2022.11.08 18:29 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6597915) 감사합니다! 너무 많은 도움이 됐어요~!!!
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
- [솜씨좋은장씨](https://somjang.tistory.com/) 2022.11.08 21:25 [신고](https://somjang.tistory.com/toolbar/popup/abuseReport/?entryId=846&commentId=6598022) 감사합니다~
	[댓글 메뉴 보기](https://somjang.tistory.com/entry/#none)
	[댓글주소](https://somjang.tistory.com/846#comment6598022) [수정/삭제](https://somjang.tistory.com/entry/#none)

---

Blog is powered by [kakao](http://www.kakaocorp.com/) / Designed by [Tistory](http://www.tistory.com/)