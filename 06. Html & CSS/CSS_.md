CSS에서 `background`와 `background-color`는 얼핏 비슷해 보이지만, **단일 속성**이냐 **단축 속성(Shorthand)**이냐라는 큰 차이가 있습니다.

---

## 1. background-color (단일 속성)

이 속성은 오직 **배경 색상**만을 지정할 때 사용합니다. 다른 배경 관련 설정(이미지, 위치, 반복 등)에는 전혀 영향을 주지 않고 색상만 바꿉니다.

- **값:** 색상 이름, HEX 코드, RGB, HSL 등
    
- **특징:** 명확하게 색상만 제어하고 싶을 때 사용합니다.
    

CSS

```
div {
  background-color: #ff0000; /* 빨간색 배경 */
}
```

---

## 2. background (단축 속성)

이 속성은 배경과 관련된 **여러 가지 세부 속성들을 한 줄에** 모아서 쓸 수 있는 '종합 선물 세트' 같은 속성입니다.

- **포함되는 속성들:**
    
    - `background-color` (색상)
        
    - `background-image` (이미지)
        
    - `background-repeat` (반복 여부)
        
    - `background-attachment` (고정 여부)
        
    - `background-position` (위치)
        
    - `background-size` (크기 - `/` 기호와 함께 사용)
        

CSS

```
div {
  /* 색상, 이미지, 반복 안함, 중앙 정렬을 한 번에! */
  background: #ff0000 url("image.jpg") no-repeat center;
}
```

---

## 3. 핵심 차이점 및 주의사항

|**구분**|**background-color**|**background**|
|---|---|---|
|**범위**|색상만 지정|색상, 이미지, 위치 등 전체 지정|
|**기존 값 유지**|다른 배경 속성을 건드리지 않음|명시하지 않은 속성은 **기본값(초기화)**으로 덮어씀|
|**권장 용도**|배경색만 바꿀 때|배경 이미지를 넣거나 여러 설정을 한 번에 할 때|

> [!CAUTION]
> 
> **가장 주의해야 할 점: 초기화 현상**
> 
> 이미 `background-image`가 설정된 요소에 나중에 `background: blue;`를 선언하면, 이미지는 사라지고 파란 배경색만 남게 됩니다. `background` 속성이 "이미지는 없음(none)"이라는 기본값으로 덮어버리기 때문입니다. 단순히 색만 바꾸고 싶다면 반드시 `background-color`를 쓰는 것이 안전합니다.

---

혹시 특정 상황(예: 버튼 디자인이나 레이아웃 설정)에서 어떤 것을 써야 할지 고민 중이신가요? 구체적인 예시가 필요하시면 말씀해 주세요!