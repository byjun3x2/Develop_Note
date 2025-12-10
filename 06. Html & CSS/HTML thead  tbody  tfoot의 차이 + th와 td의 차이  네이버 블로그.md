---
link: "[[_Clipping]]"
title: HTML thead  tbody  tfoot의 차이 + th와 td의 차이  네이버 블로그
source: https://m.blog.naver.com/ksk1908/222373612674
created: 2025-12-09
tags:
  - HTML5
  - HTML
  - CSS
  - Table
  - table
  - thead
  - tbody
  - th
  - td
---
[본문 바로가기](https://m.blog.naver.com/ksk1908/#ct)

## 블로그

## 카테고리 이동

[HTML 요소](https://m.blog.naver.com/PostList.naver?blogId=ksk1908&categoryNo=14&logCode=0&categoryName=HTML+%EC%9A%94%EC%86%8C#postlist_block)

\[HTML\] <thead> / <tbody> / <tfoot>의 차이 + <th>와 <td>의 차이

[![프로필](https://blogpfthumb-phinf.pstatic.net/MjAyMTA1MzBfNzIg/MDAxNjIyMzcwNDgxNTI0.lQZiY2lTorVwXuVCJGghbXBbKwwoqeKyZg5ry6Hetzcg.pA4gakNfqo00l87jiB0gfRffrv8Zywy0k-ZA2XOmC8Mg.JPEG.ksk1908/KakaoTalk_20210530_192711684.jpg?type=s1)](https://m.blog.naver.com/PostList.naver?blogId=ksk1908)

[**ksk1908**](https://m.blog.naver.com/PostList.naver?blogId=ksk1908)

2021\. 5. 29. 17:25

> **<thead> / <tbody> / <tfoot>의 차이**

> thead와 tbody, tfoot의 기능적인 차이는 없다.
> 
> thead와 tfoot은 tbody의 앞 뒤로
> 
> 한 번씩만 사용 가능하다.
> 
> tbody는 여러 번 사용 가능하다.

실제로 thead와 tbody, tfoot를 사용하지 않아도 충분히 테이블을 만들 수 있다.

하지만 이 세가지 태그를 사용하는 이유는 테이블 내용을 그룹화하여 개발자가 코드를 읽을 때 명확하게 구분을 해주는 역할 을 하기도 하고 상위 태그에 속성을 부여하는 경우 하위 태그까지 일괄적으로 적용되므로 각 개별 행, 열마다 속성을 부여하지 않아도 되는 편리함이 있기 때문이다.

이를 간단하게 표현하면 아래와 같은 구조가 된다.

```javascript
<table style="width:30%;">
    <thead>
        <tr>
            <th>여기가 thead </th>
            <th>여기가 thead </th>
            <th>여기가 thead </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>  tbody line 1 </td>
            <td>  tbody line 1 </td>
            <td>  tbody line 1 </td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td>  tbody line 2 </td>
            <td>  tbody line 2 </td>
            <td>  tbody line 2 </td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td>  tbody line 3 </td>
            <td>  tbody line 3 </td>
            <td>  tbody line 3 </td>
        </tr>
    </tbody>
    <tbody>
        <tr>
            <td>  tbody line 4 </td>
            <td>  tbody line 4 </td>
            <td>  tbody line 4 </td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td> tfoot </td>
            <td> tfoot </td>
            <td> tfoot </td>
        </tr>
    <tfoot>
</table>
```

위 코드를 실행 시키면 아래와 같다.

위 코드 구조를 통해 한가지 더 알 수 있는 점이 있다.

> **<th>와 <td>의 차이**

<th>요소와 <td>요소의 차이를 알 수 있는데 둘 다 <tr>: 테이블의 행 하위에서 열을 삽입하기 위한 태그이지만

<td>의 경우 별도의 서식 없이 기본 값으로 열에 텍스트가 입력되는 반면

<th>는 **'텍스트 굵게'** 기능과 **'가운데 정렬'** 기능이 탑재되어있는 것을 알 수 있다.

- [# th](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=th)
- [# td](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=td)
- [# 차이](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=%EC%B0%A8%EC%9D%B4)
- [# thead](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=thead)
- [# tbody](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=tbody)
- [# tfoot](https://m.blog.naver.com/BlogTagView.naver?orderType=date&tagName=tfoot)