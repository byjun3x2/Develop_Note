[[_Browser Settings]]

Youtube
```
	@-moz-document domain("youtube.com") {
	   *:not(.fa) {
	        font-family: 'AaHapjeongSansNormal', sans-serif;
	        font-size: 1.5rem;
	    }
	}

```

FMKOREA
```
@-moz-document url-prefix("https://www.fmkorea.com") {
	::selection {
		color: white; /* 선택된 텍스트 색상 */
		background: #6667ab; /* 선택된 배경 색상 */
	}
    
    *:not(.fa) {
        font-family: 'AaHapjeongSansNormal' !important;
        font-size: 1.04rem;
        font-weight: 200;
    }

    .fm_hot_key .li_alt .num  {
        height: 20px;
    }
      .fm_hot_key .li {
        font-family: 'AaHapjeongSansNormal';
        font-size:16px; /* 원하는 폰트 크기로 설정 */
        height: 22px;
    }
    
    .bd .img_tx a { 
        font-size: 1rem;
    }
      /*  오른쪽 단축키 패널  단축키 버튼 부분*/
    .fm_hot_key .li .num {
        height: 19px;
        font-size: 17px;
    }
    
    /*  오른쪽 단축키 패널  댓글쓰기 글 쓰기 댓글 등록 부분 글자 크기 부분*/
    .fm_hot_key .li .name {
        font-size: 16px;
    }
    
    /* 하단 검색창 */
    .bd .itx, .bd select, .bd textarea, .exForm input { 
        font-size: 19px;
    }
}
```
