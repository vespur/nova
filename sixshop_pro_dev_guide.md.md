# 식스샵 프로 블록 메이커 종합 개발 가이드라인

**버전**: 3.0  
**최종 수정**: 2025-12-02  
**출처**: https://help.pro.sixshop.com/ 공식 문서 기반  
**대상**: 노바파트너스 웹사이트 템플릿 제작

---

## 📋 목차

1. [기본 개념](#1-기본-개념)
2. [블록 메이커 코드 구조](#2-블록-메이커-코드-구조)
3. [컨텍스트(Context) 시스템](#3-컨텍스트context-시스템)
4. [Handlebars.js 템플릿 문법](#4-handlebarsjs-템플릿-문법)
5. [세팅 타입 완전 가이드](#5-세팅-타입-완전-가이드)
6. [bm 객체 API 레퍼런스](#6-bm-객체-api-레퍼런스)
7. [템플릿 제작 필수 요건](#7-템플릿-제작-필수-요건)
8. [지원금 조건](#8-지원금-조건)
9. [커스텀 블록 품질 기준](#9-커스텀-블록-품질-기준)
10. [data 태그 - 외부 데이터 연동](#10-data-태그---외부-데이터-연동)
11. [에디터 프리뷰 지원](#11-에디터-프리뷰-지원)
12. [템플릿 마켓플레이스 판매](#12-템플릿-마켓플레이스-판매)
13. [개발 모범 사례](#13-개발-모범-사례)
14. [부록: 헬퍼 함수 전체 목록](#14-부록-헬퍼-함수-전체-목록)

---

## 1. 기본 개념

### 1.1 블록(Block)이란?

웹사이트를 구성하는 **재사용 가능한 콘텐츠 단위**.

- 하나의 행(Row) 전체를 차지하거나, 행 내의 열(Column)에 삽입 가능
- 독립적으로 편집 가능
- 여러 페이지에서 재사용 가능

### 1.2 블록 메이커(Block Maker)

커스텀 블록을 개발하는 도구.

**특징**:
- HTML/CSS/JavaScript로 블록 개발
- Handlebars.js 템플릿 엔진 사용
- 세팅 빌더로 비개발자도 편집 가능한 설정 패널 제공

### 1.3 세팅 빌더(Setting Builder)

블록의 설정 패널(GUI)을 정의하는 도구.

- 코드 수정 없이 블록 커스터마이징 지원
- 에디터 우측 패널에서 [설정 패널] 탭으로 접근

---

## 2. 블록 메이커 코드 구조

### 2.1 4대 최상위 태그

```html
<style>
  /* CSS 스타일 */
</style>

<template>
  <!-- HTML 템플릿 (Handlebars.js) -->
</template>

<script>
  // JavaScript 로직
</script>

<data value="$page" />
<data value="$customer" />
<data value="$cart" />
```

**규칙**:
- 각 태그(`<style>`, `<template>`, `<script>`)는 **하나씩만** 최상위에 존재
- `<data>` 태그는 필요한 경우에만 선언

### 2.2 `<style>` 태그

```html
<style>
  .hero-section {
    padding: 120px 0;
    background: linear-gradient(135deg, #0055FF 0%, #003399 100%);
  }
  
  .hero-title {
    color: {{property.titleColor}};
    font-size: {{property.titleSize}}px;
  }
</style>
```

**특징**:
- CSS 코드 입력
- 각 블록별로 **격리되어 적용**
- Handlebars.js로 동적 값 사용 가능
- 브라우저 기본 CSS가 **대부분 초기화(Reset)** 되어 있음

**주의**: 클래스명은 고유하게 작성 (`.title` (X) → `.hero-section-title` (O))

### 2.3 `<template>` 태그

```html
<template>
  <section class="hero-section">
    <h1 class="hero-title">{{property.headline}}</h1>
    <p>{{property.subtext}}</p>
    
    {{#if property.showButton}}
      <a href="{{property.buttonLink.value}}">{{property.buttonText}}</a>
    {{/if}}
  </section>
</template>
```

**특징**:
- HTML 템플릿 입력
- Handlebars.js 문법으로 동적 콘텐츠 구성
- **블록 컨테이너** 내부에 렌더링됨

### 2.4 `<script>` 태그

```html
<script>
  const container = bm.container;
  const context = bm.context;
  
  container.addEventListener('click', e => {
    e.preventDefault();
    if (e.target.matches('button')) {
      alert(context.property.message);
    }
  }, true);
</script>
```

**특징**:
- `<template>`과 `<style>`이 먼저 렌더링된 후 실행
- `bm` 객체로 블록 제어
- 순수 JavaScript(Vanilla JS) 권장 (외부 라이브러리는 속도 저하 원인)

**⚠️ 주의: DOM 이벤트 바인딩 방식**

```html
<!-- ✅ Good: 블록 컨테이너에 이벤트 위임 -->
<script>
  bm.container.addEventListener('click', e => {
    if (e.target.matches('button')) {
      alert('클릭!');
    }
  }, true);
</script>

<!-- ❌ Bad: 특정 요소에 직접 바인딩 -->
<script>
  const btn = bm.container.querySelector('button');
  btn.addEventListener('click', () => alert('클릭!'));
  // 동적으로 DOM이 변경되면 이벤트가 유실됨
</script>
```

---

## 3. 컨텍스트(Context) 시스템

### 3.1 컨텍스트란?

블록의 UI 렌더링과 동작에 필요한 **데이터 JSON 객체**.

```javascript
{
  "id": "block-unique-id-123",
  "property": {
    "headline": "AI가 만드는 신뢰할 수 있는 미래",
    "titleColor": "#FFFFFF",
    "titleSize": 48,
    "showButton": true
  },
  "page": { ... },      // <data value="$page" /> 사용 시
  "customer": { ... },  // <data value="$customer" /> 사용 시
  "cart": { ... }       // <data value="$cart" /> 사용 시
}
```

### 3.2 컨텍스트 접근 방법

| 태그 | 접근 방법 |
|------|----------|
| `<style>` | `{{property.myValue}}` |
| `<template>` | `{{property.myValue}}` |
| `<script>` | `bm.context.property.myValue` |

### 3.3 property 객체 구조

세팅 빌더에서 정의한 설정들이 `property` 객체에 저장됨.

**세팅 정의 (설정 패널 JSON)**:
```json
{
  "settings": [
    {
      "id": "style.headlineColor",
      "label": "헤드라인 색상",
      "type": "COLOR_PICKER"
    }
  ],
  "property": {
    "style": {
      "headlineColor": "#FFFFFF"
    }
  }
}
```

**템플릿에서 사용**:
```html
<h1 style="color: {{property.style.headlineColor}};">제목</h1>
```

---

## 4. Handlebars.js 템플릿 문법

### 4.1 기본 출력

```handlebars
{{property.title}}           <!-- 일반 텍스트 (HTML 이스케이프) -->
{{{property.htmlContent}}}   <!-- HTML 그대로 출력 -->
{{property.nested.value}}    <!-- 중첩 값 접근 -->
```

### 4.2 조건문

```handlebars
{{#if property.showButton}}
  <button>클릭</button>
{{else}}
  <span>버튼 없음</span>
{{/if}}

{{#unless property.hideTitle}}
  <h1>제목</h1>
{{/unless}}
```

**Falsy 값**: `false`, `undefined`, `null`, `""`, `0`, `[]`

### 4.3 헬퍼를 활용한 조건문

```handlebars
{{#if (eq property.status 'active')}}
  활성 상태
{{/if}}

{{#if (and (gte property.count 5) (lte property.count 10))}}
  5~10 사이
{{/if}}

{{#if (or property.flagA property.flagB)}}
  둘 중 하나 참
{{/if}}
```

### 4.4 반복문

```handlebars
{{#each property.items}}
  <div class="item">
    {{#if @first}}<span>첫 번째</span>{{/if}}
    {{#if @last}}<span>마지막</span>{{/if}}
    <p>{{@index}}: {{this.name}}</p>
  </div>
{{else}}
  <p>항목이 없습니다.</p>
{{/each}}
```

**특수 키워드**:
- `@index`: 0부터 시작하는 인덱스
- `@first`: 첫 번째 항목이면 true
- `@last`: 마지막 항목이면 true
- `this`: 현재 항목 객체

---

## 5. 세팅 타입 완전 가이드

### 5.1 세팅 JSON 구조

```json
{
  "settings": [
    // 설정 패널 UI 정의
  ],
  "property": {
    // 기본값 저장
  }
}
```

### 5.2 TITLE - 섹션 구분 제목

```json
{
  "type": "TITLE",
  "content": "🖼 전체 레이아웃 / 공통 설정"
}
```

⚠️ **`label`이 아닌 `content` 사용!**

### 5.3 TEXT - 한 줄 텍스트

```json
{
  "id": "headline",
  "label": "헤드라인 텍스트",
  "description": "히어로 섹션의 메인 카피입니다.",
  "type": "TEXT",
  "placeholder": "당신의 브랜드를 세계로"
}
```

### 5.4 TEXTAREA - 여러 줄 텍스트

```json
{
  "id": "description",
  "label": "설명",
  "type": "TEXTAREA",
  "placeholder": "자세한 설명을 입력하세요"
}
```

### 5.5 CHECKBOX - 체크박스

```json
{
  "id": "showButton",
  "label": "버튼 표시",
  "type": "CHECKBOX"
}
```

**property 기본값**: `true` 또는 `false`

### 5.6 RADIO - 라디오 버튼

```json
{
  "id": "textAlign",
  "label": "텍스트 정렬",
  "type": "RADIO",
  "options": [
    {"label": "왼쪽", "value": "left"},
    {"label": "가운데", "value": "center"},
    {"label": "오른쪽", "value": "right"}
  ]
}
```

### 5.7 SELECT - 드롭다운

```json
{
  "id": "animationType",
  "label": "애니메이션 타입",
  "type": "SELECT",
  "options": [
    {"label": "페이드", "value": "fade"},
    {"label": "슬라이드", "value": "slide"}
  ]
}
```

### 5.8 RANGE - 숫자 슬라이더

```json
{
  "id": "columns",
  "label": "열 개수",
  "type": "RANGE",
  "min": 1,
  "max": 6,
  "step": 1
}
```

**실무 권장**: TEXT 타입 + placeholder가 더 유연함

### 5.9 COLOR_PICKER - 색상 선택

```json
{
  "id": "style.backgroundColor",
  "label": "배경 색상",
  "type": "COLOR_PICKER"
}
```

**property 예시**: `"#FF6600"` 또는 `"rgba(0,0,0,0.6)"`

### 5.10 LINK - 링크 입력

```json
{
  "id": "ctaLink",
  "label": "버튼 링크",
  "type": "LINK"
}
```

**property 구조**:
```json
{
  "ctaLink": {
    "id": null,
    "type": "url",
    "label": "https://example.com",
    "value": "https://example.com"
  }
}
```

**템플릿 사용**:
```html
<a href="{{property.ctaLink.value}}">{{property.ctaLink.label}}</a>
```

### 5.11 IMAGE_PICKER - 이미지 선택

```json
{
  "id": "backgroundImage",
  "label": "배경 이미지",
  "type": "IMAGE_PICKER"
}
```

**property 예시**: `"https://example.org/image.png"`

### 5.12 VIDEO_PICKER - 비디오 선택

```json
{
  "id": "backgroundVideo",
  "label": "배경 비디오",
  "type": "VIDEO_PICKER"
}
```

### 5.13 LIST - 반복 가능한 리스트

```json
{
  "id": "slides",
  "label": "슬라이드 목록",
  "type": "LIST",
  "maxCount": 10,
  "settings": [
    {
      "id": "title",
      "label": "제목",
      "type": "TEXT"
    },
    {
      "id": "image",
      "label": "이미지",
      "type": "IMAGE_PICKER"
    }
  ]
}
```

**property 구조**:
```json
{
  "slides": [
    {"title": "슬라이드 1", "image": "https://..."},
    {"title": "슬라이드 2", "image": "https://..."}
  ]
}
```

### 5.14 RICH_TEXT - 서식 있는 텍스트

```json
{
  "id": "content",
  "label": "본문 내용",
  "type": "RICH_TEXT"
}
```

**property 예시**: `"<p>HTML <strong>텍스트</strong></p>"`

### 5.15 MENU - 네비게이션 메뉴

```json
{
  "id": "navMenus",
  "label": "메뉴 설정",
  "type": "MENU"
}
```

**property 구조**:
```json
{
  "navMenus": [
    {
      "id": "1",
      "name": "홈",
      "link": {"type": "url", "label": "/", "value": "/"},
      "childMenus": []
    }
  ]
}
```

### 5.16 PRODUCT - 상품 선택

```json
{
  "id": "featuredProducts",
  "label": "대표 상품",
  "type": "PRODUCT"
}
```

### 5.17 조건부 표시 (isVisible)

```json
{
  "id": "style.glowDirection",
  "label": "Glow 방향",
  "type": "RADIO",
  "options": [...],
  "isVisible": "property.style.hoverAnimation === 'glow'"
}
```

**규칙**:
- `property.` 접두사 필수
- JavaScript 표현식 사용
- ❌ Handlebars 문법 사용 불가

**예시**:
```json
// ✅ 올바름
"isVisible": "property.showButton === true"
"isVisible": "property.style.type === 'video'"
"isVisible": "property.count > 5 && property.enabled === true"

// ❌ 잘못됨
"isVisible": "{{showButton}}"
"isVisible": "showButton === true"
```

---

## 6. bm 객체 API 레퍼런스

### 6.1 bm.container

블록 컨테이너 DOM 요소 반환.

```javascript
const container = bm.container;
container.querySelector('.my-element');
container.addEventListener('click', handler, true);
```

### 6.2 bm.context

현재 컨텍스트 객체 반환.

```javascript
const context = bm.context;
console.log(context.property.title);
console.log(context.id);
```

### 6.3 bm.onContextChange

컨텍스트 변경 시 실행되는 콜백 함수.

```javascript
bm.onContextChange = () => {
  // 설정값 변경 시 UI 업데이트
  const title = bm.context.property.title;
  bm.container.querySelector('h1').textContent = title;
};
```

**호출 시점**:
- 사용자가 에디터에서 설정값 변경
- `<data>` 태그로 주입받은 데이터 변경
- `bm.apply()` 호출

### 6.4 bm.onDestroy

블록 제거 시 실행되는 콜백 함수.

```javascript
const interval = setInterval(() => console.log('실행 중'), 1000);

bm.onDestroy = () => {
  clearInterval(interval); // 정리 작업
};
```

**정리 대상**:
- `setInterval`, `setTimeout`
- 이벤트 리스너
- Observer 해제
- 전역 변수 초기화

### 6.5 bm.apply()

컨텍스트 변경 적용 및 재렌더링.

```javascript
bm.context.counter = (bm.context.counter || 0) + 1;
bm.apply(); // 블록 재렌더링 + onContextChange 실행
```

### 6.6 bm.do(action, params)

제공되는 액션 실행.

```javascript
bm.do('logout'); // 로그아웃 처리
```

**제공 액션**:
| 액션 | 설명 |
|------|------|
| `logout` | 로그인된 고객 로그아웃 |

### 6.7 bm.call(request)

HTTP 요청 전송.

```javascript
// GET 요청
bm.call({
  method: 'GET',
  url: 'https://api.example.org/data'
}).then(response => {
  bm.context.data = response.data;
  bm.apply();
});

// POST 요청
bm.call({
  method: 'POST',
  url: 'https://api.example.org/submit',
  data: { name: '홍길동' }
}).then(response => {
  console.log(response.data);
});
```

**기본 Content-Type**: `application/json`

### 6.8 bm.localStorage / bm.sessionStorage

자동 JSON 변환되는 스토리지.

```javascript
// 저장
bm.localStorage.setItem('user', { name: '홍길동', age: 30 });

// 조회
const user = bm.localStorage.getItem('user');
console.log(user.name); // "홍길동"

// 삭제
bm.localStorage.removeItem('user');
```

---

## 7. 템플릿 제작 필수 요건

### 7.1 편집 용이성

**목표**: 비개발자도 쉽게 편집 가능해야 합니다.

**체크리스트**:
- [ ] 모든 텍스트가 설정 패널에서 수정 가능
- [ ] 모든 이미지가 이미지 피커로 교체 가능
- [ ] 모든 색상이 색상 선택기로 변경 가능
- [ ] 모든 링크가 설정 패널에서 수정 가능

---

### 7.2 콘텐츠 구성

**금지 사항**:
- ❌ **통이미지 사용 금지** (텍스트가 이미지에 포함된 경우)
- ❌ **저작권 있는 이미지 사용 금지**

**권장 사항**:
- ✅ 텍스트는 HTML로 작성
- ✅ 이미지는 Unsplash, Pexels 등 무료 이미지 사용
- ✅ 아이콘은 Font Awesome, Lucide 등 무료 아이콘 사용

---

### 7.3 이미지 품질

**권장 해상도**:
- 배경 이미지: 1920x1080px 이상
- 카드 이미지: 800x600px 이상
- 썸네일: 400x300px 이상

**최적화**:
- WebP 형식 권장 (용량 감소)
- 파일 크기 500KB 이하 권장

---

### 7.4 일관성

**디자인 일관성**:
- 색상 팔레트 통일
- 타이포그래피 일관성
- 여백(Spacing) 규칙 일관성
- 버튼 스타일 일관성

---

## 8. 지원금 조건

### 8.1 기본 지원금: 50만원

**조건**:
- ✅ 커스텀 블록 **5개 이상** 제작
- ✅ 각 블록마다 **설정 패널** 포함
- ✅ "내 페이지" **3개 이상** 포함

**"내 페이지"란?**  
템플릿에 포함된 완성된 페이지 (예: HOME, 회사소개, 문의하기)

---

### 8.2 추가 지원금: 1만원 ~ 200만원

**조건**:
- ✅ 커스텀 블록 **10개 이상** 제작
- ✅ 그 중 **5개 이상**이 **신규 제작** 블록
- ✅ 각 블록마다 **고급 설정 패널** 포함

**"신규 제작"이란?**  
기존 템플릿에 없는 독창적인 블록 (단순 복사/수정 X)

---

## 9. 커스텀 블록 품질 기준

### 9.1 설정 패널 정리

**체크리스트**:
- [ ] 설정 항목이 **논리적으로 그룹핑**되어 있음
- [ ] 각 설정 항목에 **명확한 라벨**이 있음
- [ ] **TITLE 타입**으로 섹션을 구분함
- [ ] **DESCRIPTION 타입**으로 섹션 설명 추가
- [ ] 기본값이 **2026 트렌드**를 반영함

**예시**:
```json
{
  "type": "TITLE",
  "content": "🧩 헤드라인 / 본문"
},
{
  "type": "DESCRIPTION",
  "content": "메인 메시지, 서브텍스트, 신뢰 문구와 텍스트 정렬을 설정하실 수 있습니다."
},
{
  "id": "headline",
  "label": "헤드라인 텍스트",
  "description": "히어로 섹션의 메인 카피입니다.",
  "type": "TEXT",
  "placeholder": "당신의 브랜드를 세계로"
}
```

---

### 9.2 블록 동작 점검

**체크리스트**:
- [ ] 모든 설정 항목 변경 시 **즉시 반영**됨
- [ ] **반응형 디자인** 적용 (모바일/태블릿/데스크톱)
- [ ] **호버 효과** 정상 작동
- [ ] **애니메이션** 부드럽게 작동
- [ ] JavaScript 에러 없음

---

### 9.3 테마 설정 상속

**체크리스트**:
- [ ] 테마 색상을 **상속**받아 사용
- [ ] 테마 폰트를 **상속**받아 사용
- [ ] 개별 설정으로 **재정의** 가능

**예시**:
```css
.hero {
  /* 테마 색상 상속 */
  background: var(--theme-primary-color, #0055FF);
  
  /* 또는 개별 설정 */
  background: {{backgroundColor}};
}
```

---

### 9.4 개별 설정 점검

**체크리스트**:
- [ ] 색상: 모든 색상 요소 변경 가능
- [ ] 크기: 폰트 크기, 여백, 높이 조절 가능
- [ ] 정렬: 좌/중/우 정렬 옵션
- [ ] 표시/숨김: 선택적 요소 제어 가능

---

### 9.5 헤더/푸터 특수 요건

**헤더 블록**:
- [ ] 스크롤 시 고정(Fixed) 옵션
- [ ] 투명 배경 옵션
- [ ] 메뉴 아이템 추가/삭제 가능
- [ ] 로고 이미지 변경 가능
- [ ] 모바일 메뉴(햄버거) 작동

**푸터 블록**:
- [ ] 다단 레이아웃 지원 (2-4열)
- [ ] SNS 아이콘 링크 설정 가능
- [ ] 저작권 텍스트 수정 가능

---

## 10. data 태그 - 외부 데이터 연동

### 10.1 사용 가능한 데이터

```html
<data value="$page" />
<data value="$customer" />
<data value="$cart" />
```

### 10.2 $page - 현재 페이지 정보

```json
{
  "name": "HOME",
  "path": "/"
}
```

**주요 페이지 구분자**:
| 페이지 | name | path |
|--------|------|------|
| 홈페이지 | HOME | / |
| 커스텀 | CUSTOM | /:param |
| 상품 목록(전체) | PRODUCT_LIST | /categories/all |
| 상품 상세 | PRODUCT_DETAIL | /products/:param |
| 장바구니 | CART | /cart |
| 주문서 | CHECKOUT | /checkout |
| 로그인 | LOGIN | /auth/login |
| 회원가입 | SIGNUP | /auth/signup |

### 10.3 $customer - 로그인 고객 정보

```json
{
  "id": "customer-id-123",
  "name": {
    "full": "홍길동"
  }
}
```

**로그인하지 않은 경우**: `null`

### 10.4 $cart - 장바구니 정보

```json
{
  "count": 3,
  "total": {
    "items": {
      "price": {
        "original": 100000,
        "sale": 85000
      },
      "discounted": 15000
    }
  }
}
```

### 10.5 활용 예시

```html
<data value="$page" />
<data value="$customer" />
<data value="$cart" />

<template>
  {{#if (eq page.name "HOME")}}
    <h1>환영합니다!</h1>
  {{/if}}
  
  {{#if customer}}
    <p>안녕하세요, {{customer.name.full}}님!</p>
    <button class="logout-btn">로그아웃</button>
  {{else}}
    <a href="/auth/login">로그인</a>
  {{/if}}
  
  <p>장바구니: {{cart.count}}개</p>
</template>

<script>
  bm.container.addEventListener('click', e => {
    if (e.target.matches('.logout-btn')) {
      bm.do('logout');
    }
  }, true);
  
  bm.onContextChange = () => {
    console.log('페이지:', bm.context.page);
    console.log('고객:', bm.context.customer);
    console.log('장바구니:', bm.context.cart);
  };
</script>
```

---

## 11. 에디터 프리뷰 지원

### 11.1 자동 반영 (template, style)

`<template>`과 `<style>` 태그에서 `{{property.*}}`로 사용된 값은 **자동으로 프리뷰에 반영**.

### 11.2 수동 반영 (script)

`<script>` 태그에서 동적으로 변경한 내용은 `bm.onContextChange`에서 처리 필요.

```html
<template>
  <p id="dynamic-content"></p>
</template>

<script>
  const p = bm.container.querySelector('#dynamic-content');
  
  // 최초 렌더링
  p.innerHTML = bm.context.property.content;
  
  // 설정 변경 시 프리뷰 업데이트
  bm.onContextChange = () => {
    p.innerHTML = bm.context.property.content;
  };
</script>
```

---

## 12. 템플릿 마켓플레이스 판매

### 12.1 파트너 활동 가이드

1. 식스샵 프로 상점에서 블록/템플릿 제작
2. 패키징하여 마켓플레이스로 제출/배포
3. 사용자가 다운로드(구매)하여 사용

### 12.2 수익 배분

- **파트너**: 판매 대금의 **85%**
- **식스샵**: 판매 대금의 **15%** (수수료)

### 12.3 정산 절차

| 단계 | 시기 | 내용 |
|------|------|------|
| 내역 고지 | 익월 5일까지 | 회사 → 파트너 정산 내역 고지 |
| 세금계산서 | 익월 10일까지 | 파트너 → 회사 세금계산서 발행 |
| 수익금 지급 | 익월 20일까지 | 회사 → 파트너 지정 계좌 지급 |

---

## 13. 개발 모범 사례

### 13.1 CSS 클래스명 규칙

```css
/* ✅ Good: 고유한 접두사 사용 */
.nova-hero-section { }
.nova-hero-title { }
.nova-feature-card { }

/* ❌ Bad: 일반적인 이름 */
.hero { }
.title { }
.card { }
```

### 13.2 이벤트 위임 패턴

```javascript
// ✅ Good: 컨테이너에 위임
bm.container.addEventListener('click', e => {
  if (e.target.matches('.btn-primary')) { ... }
  if (e.target.matches('.btn-secondary')) { ... }
}, true);

// ❌ Bad: 개별 요소에 직접 바인딩
document.querySelector('.btn').addEventListener('click', ...);
```

### 13.3 설정 패널 구조화

```json
{
  "settings": [
    {"type": "TITLE", "content": "📝 콘텐츠 설정"},
    {"id": "headline", "label": "헤드라인", "type": "TEXT"},
    {"id": "subtext", "label": "서브텍스트", "type": "TEXTAREA"},
    
    {"type": "TITLE", "content": "🎨 디자인 설정"},
    {"id": "style.bgColor", "label": "배경 색상", "type": "COLOR_PICKER"},
    {"id": "style.textAlign", "label": "정렬", "type": "RADIO", "options": [...]},
    
    {"type": "TITLE", "content": "📱 반응형 설정"},
    {"id": "style.paddingDesktop", "label": "여백 (데스크톱)", "type": "TEXT"},
    {"id": "style.paddingMobile", "label": "여백 (모바일)", "type": "TEXT"}
  ]
}
```

### 13.4 CSS 내 동적 값 사용 주의

```css
/* ✅ Good: 단순 값 치환 */
.hero {
  background-color: {{property.style.bgColor}};
  padding: {{property.style.padding}}px;
}

/* ❌ Bad: JavaScript 삼항연산자 (파싱 에러) */
.hero {
  margin: {{property.align === 'center' ? 'auto' : '0'}};
}
```

**조건부 스타일 해결책**:
```html
<!-- template에서 클래스 분기 -->
<div class="hero {{#if (eq property.align 'center')}}hero--centered{{/if}}">
```

```css
/* style에서 각 클래스 정의 */
.hero { margin: 0; }
.hero--centered { margin: 0 auto; }
```

### 13.5 리소스 정리

```javascript
// 타이머 정리
const timer = setInterval(() => { ... }, 1000);
bm.onDestroy = () => clearInterval(timer);

// Observer 정리
const observer = new IntersectionObserver(...);
observer.observe(element);
bm.onDestroy = () => observer.disconnect();
```

---

## 14. 부록: 헬퍼 함수 전체 목록

### 조건 헬퍼 (Conditionals)

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `and` | `{{#if (and a b)}}` | 모두 true면 true |
| `or` | `{{#if (or a b)}}` | 하나라도 true면 true |
| `eq` | `{{#if (eq a b)}}` | 같으면 true |
| `gt` | `{{#if (gt a b)}}` | a > b면 true |
| `gte` | `{{#if (gte a b)}}` | a >= b면 true |
| `lt` | `{{#if (lt a b)}}` | a < b면 true |
| `lte` | `{{#if (lte a b)}}` | a <= b면 true |
| `isNil` | `{{#if (isNil a)}}` | null/undefined면 true |
| `isEmpty` | `{{#if (isEmpty a)}}` | 비어있으면 true |
| `inRange` | `{{#if (inRange v 1 10)}}` | 범위 내면 true |
| `startsWith` | `{{#if (startsWith s "Hi")}}` | 시작 문자열 확인 |
| `endsWith` | `{{#if (endsWith s "!")}}` | 끝 문자열 확인 |
| `includes` | `{{#if (includes s "text")}}` | 포함 여부 확인 |

### 숫자 헬퍼 (Number)

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `ceil` | `{{ceil 4.2}}` → 5 | 올림 |
| `floor` | `{{floor 4.8}}` → 4 | 내림 |
| `round` | `{{round 4.5}}` → 5 | 반올림 |
| `add` | `{{add 2 3}}` → 5 | 더하기 |
| `subtract` | `{{subtract 5 2}}` → 3 | 빼기 |
| `multiply` | `{{multiply 3 4}}` → 12 | 곱하기 |
| `divide` | `{{divide 10 2}}` → 5 | 나누기 |
| `sumBy` | `{{sumBy items "price"}}` | 속성 합계 |
| `meanBy` | `{{meanBy items "score"}}` | 속성 평균 |
| `minBy` | `{{minBy items "age"}}` | 최솟값 항목 |
| `maxBy` | `{{maxBy items "score"}}` | 최댓값 항목 |

### 문자열 헬퍼 (String)

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `toLower` | `{{toLower "HELLO"}}` → hello | 소문자 변환 |
| `toUpper` | `{{toUpper "hello"}}` → HELLO | 대문자 변환 |
| `capitalize` | `{{capitalize "hello"}}` → Hello | 첫 글자 대문자 |
| `trim` | `{{trim " hello "}}` → hello | 공백 제거 |
| `padStart` | `{{padStart "1" 3 "0"}}` → 001 | 앞 채우기 |
| `padEnd` | `{{padEnd "a" 3 "_"}}` → a__ | 뒤 채우기 |
| `join` | `{{join items ", "}}` | 배열 연결 |
| `split` | `{{split text ","}}` | 문자열 분할 |
| `camelCase` | `{{camelCase "hello world"}}` → helloWorld | camelCase |
| `kebabCase` | `{{kebabCase "Hello World"}}` → hello-world | kebab-case |
| `snakeCase` | `{{snakeCase "Hello World"}}` → hello_world | snake_case |

### 배열 헬퍼 (Array)

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `first` | `{{first items}}` | 첫 번째 항목 |
| `last` | `{{last items}}` | 마지막 항목 |
| `size` | `{{size items}}` | 길이/개수 |
| `slice` | `{{slice items 1 3}}` | 일부 추출 |
| `concat` | `{{concat arr1 arr2}}` | 배열 합치기 |
| `orderBy` | `{{orderBy items "name" "asc"}}` | 정렬 |
| `filter` | `{{filter items "isActive"}}` | 필터링 |
| `reject` | `{{reject items "isDone"}}` | 제외 필터링 |
| `chunk` | `{{chunk items 2}}` | 청크 분할 |

### 랜덤 헬퍼 (Random)

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `random` | `{{random 1 10}}` | 랜덤 숫자 |
| `shuffle` | `{{shuffle items}}` | 배열 섞기 |
| `sample` | `{{sample items}}` | 랜덤 1개 선택 |
| `sampleSize` | `{{sampleSize items 3}}` | 랜덤 n개 선택 |

### 기타 헬퍼

| 헬퍼 | 예시 | 설명 |
|------|------|------|
| `range` | `{{range 0 5}}` → [0,1,2,3,4] | 범위 배열 생성 |
| `defaultTo` | `{{defaultTo val "기본"}}` | 기본값 설정 |
| `toInteger` | `{{toInteger "42"}}` → 42 | 정수 변환 |
| `toNumber` | `{{toNumber "3.14"}}` → 3.14 | 숫자 변환 |
| `toString` | `{{toString 123}}` → "123" | 문자열 변환 |
| `toJSON` | `{{toJSON obj}}` | JSON 문자열화 |
| `fromJSON` | `{{fromJSON str}}` | JSON 파싱 |

---

## ✅ 개발 체크리스트

### 개발 전
- [ ] 블록 메이커 문법 숙지
- [ ] 필요한 이미지 에셋 준비 (5MB 이하)
- [ ] 비디오 에셋 준비 (50MB 이하, MP4)

### 개발 중
- [ ] HTML 시맨틱하게 작성
- [ ] CSS 클래스명 고유하게 (접두사 사용)
- [ ] DOM 이벤트 컨테이너에 위임
- [ ] 설정 패널 논리적으로 그룹핑 (TITLE 활용)
- [ ] isVisible 조건 `property.` 접두사 확인

### 개발 후
- [ ] 데스크톱 (1920px) 테스트
- [ ] 태블릿 (768px) 테스트
- [ ] 모바일 (375px) 테스트
- [ ] 모든 설정 변경 테스트
- [ ] 에디터 프리뷰 정상 작동 확인
- [ ] bm.onDestroy로 리소스 정리 확인
- [ ] 브라우저 호환성 테스트

---

**문서 끝**
