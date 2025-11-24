# 🎨 노바파트너스 디자인 시스템 2026

**목적**: 23개 전체 페이지에서 재사용 가능한 컴포넌트 라이브러리  
**기준**: HOME 픽셀 퍼펙트 스펙에서 추출 + 확장  
**적용**: Claude Code가 모든 페이지 개발 시 참조

---

## 📋 목차

1. [전역 설정](#1-전역-설정)
2. [레이아웃 시스템](#2-레이아웃-시스템)
3. [버튼 컴포넌트](#3-버튼-컴포넌트)
4. [카드 컴포넌트](#4-카드-컴포넌트)
5. [섹션 레이아웃](#5-섹션-레이아웃)
6. [내비게이션](#6-내비게이션)
7. [폼 요소](#7-폼-요소)
8. [타이포그래피](#8-타이포그래피)
9. [애니메이션](#9-애니메이션)
10. [반응형 규칙](#10-반응형-규칙)

---

## 1. 전역 설정

### 1.1 CSS Variables

```css
:root {
  /* === Colors === */
  --primary-500: #0055FF;
  --primary-600: #0044CC;
  --primary-700: #003399;
  
  --gray-50: #F8F9FA;
  --gray-100: #E9ECEF;
  --gray-200: #DEE2E6;
  --gray-500: #6C757D;
  --gray-700: #495057;
  --gray-800: #343A40;
  --gray-900: #212529;
  
  --white: #FFFFFF;
  --black: #000000;
  
  /* Semantic Colors */
  --success: #28A745;
  --warning: #FFC107;
  --error: #DC3545;
  --info: #17A2B8;
  
  /* === Typography === */
  --font-primary: 'Pretendard Variable', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: 'JetBrains Mono', 'Courier New', monospace;
  
  /* Font Sizes */
  --text-xs: 12px;
  --text-sm: 14px;
  --text-base: 16px;
  --text-lg: 18px;
  --text-xl: 20px;
  --text-2xl: 24px;
  --text-3xl: 28px;
  --text-4xl: 32px;
  --text-5xl: 40px;
  --text-6xl: 48px;
  
  /* Line Heights */
  --leading-tight: 1.25;
  --leading-snug: 1.375;
  --leading-normal: 1.5;
  --leading-relaxed: 1.625;
  --leading-loose: 2;
  
  /* === Spacing === */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-8: 48px;
  --space-10: 64px;
  --space-12: 80px;
  --space-15: 120px;
  --space-20: 160px;
  
  /* === Border Radius === */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  --radius-2xl: 32px;
  --radius-full: 9999px;
  
  /* === Shadows === */
  --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.08);
  --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.12);
  --shadow-lg: 0 8px 32px rgba(0, 0, 0, 0.16);
  --shadow-xl: 0 12px 48px rgba(0, 0, 0, 0.20);
  
  /* Primary Glow */
  --shadow-primary: 0 4px 16px rgba(0, 85, 255, 0.25);
  --shadow-primary-lg: 0 8px 24px rgba(0, 85, 255, 0.35);
  
  /* === Transitions === */
  --duration-fast: 0.2s;
  --duration-normal: 0.3s;
  --duration-slow: 0.6s;
  --ease: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  
  /* === Z-index === */
  --z-base: 1;
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-fixed: 300;
  --z-modal-backdrop: 400;
  --z-modal: 500;
  --z-popover: 600;
  --z-tooltip: 700;
}
```

### 1.2 Reset & Base Styles

```css
/* Box Sizing */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* Body */
body {
  font-family: var(--font-primary);
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--gray-900);
  background: var(--white);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Images */
img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* Links */
a {
  color: inherit;
  text-decoration: none;
}

/* Lists */
ul, ol {
  list-style: none;
}

/* Buttons */
button {
  font-family: inherit;
  cursor: pointer;
  border: none;
  background: none;
}
```

---

## 2. 레이아웃 시스템

### 2.1 Container

```css
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

@media (max-width: 1199px) {
  .container { padding: 0 48px; }
}

@media (max-width: 767px) {
  .container { padding: 0 24px; }
}
```

### 2.2 Section Spacing

```css
/* Section Padding Presets */
.section-sm {
  padding: 60px 0;
}

.section-md {
  padding: 80px 0;
}

.section-lg {
  padding: 120px 0;
}

.section-xl {
  padding: 160px 0;
}

/* Mobile Adjustments */
@media (max-width: 767px) {
  .section-sm { padding: 40px 0; }
  .section-md { padding: 60px 0; }
  .section-lg { padding: 80px 0; }
  .section-xl { padding: 100px 0; }
}
```

### 2.3 Grid System

```css
/* 2 Column Grid */
.grid-2 {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 32px;
}

/* 3 Column Grid */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

/* 4 Column Grid */
.grid-4 {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
}

/* Responsive Grid */
@media (max-width: 991px) {
  .grid-3 { grid-template-columns: repeat(2, 1fr); }
  .grid-4 { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 767px) {
  .grid-2,
  .grid-3,
  .grid-4 {
    grid-template-columns: 1fr;
    gap: 16px;
  }
}
```

---

## 3. 버튼 컴포넌트

### 3.1 Primary Button

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 32px;
  height: 56px;
  font-size: 16px;
  font-weight: 600;
  line-height: 24px;
  color: var(--white);
  background: var(--primary-500);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  box-shadow: var(--shadow-primary);
  transition: all var(--duration-normal) var(--ease);
  white-space: nowrap;
}

.btn-primary:hover {
  background: var(--primary-600);
  transform: translateY(-3px);
  box-shadow: var(--shadow-primary-lg);
}

.btn-primary:active {
  transform: translateY(-1px);
}

.btn-primary:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none;
}
```

### 3.2 Secondary Button

```css
.btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 32px;
  height: 56px;
  font-size: 16px;
  font-weight: 600;
  line-height: 24px;
  color: var(--primary-500);
  background: var(--white);
  border: 2px solid var(--gray-100);
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all var(--duration-normal) var(--ease);
  white-space: nowrap;
}

.btn-secondary:hover {
  background: var(--gray-50);
  border-color: var(--primary-500);
  transform: translateY(-3px);
  box-shadow: 0 4px 12px rgba(0, 85, 255, 0.1);
}
```

### 3.3 Outline Button

```css
.btn-outline {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 32px;
  height: 56px;
  font-size: 16px;
  font-weight: 600;
  line-height: 24px;
  color: var(--primary-500);
  background: transparent;
  border: 2px solid var(--primary-500);
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all var(--duration-normal) var(--ease);
  white-space: nowrap;
}

.btn-outline:hover {
  color: var(--white);
  background: var(--primary-500);
  transform: translateY(-2px);
  box-shadow: var(--shadow-primary);
}
```

### 3.4 Ghost Button

```css
.btn-ghost {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  height: 48px;
  font-size: 15px;
  font-weight: 600;
  color: var(--gray-700);
  background: transparent;
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
}

.btn-ghost:hover {
  color: var(--primary-500);
  background: rgba(0, 85, 255, 0.05);
}
```

### 3.5 Small Button

```css
.btn-sm {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  padding: 10px 20px;
  height: 40px;
  font-size: 14px;
  font-weight: 600;
  color: var(--white);
  background: var(--primary-500);
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
}

.btn-sm:hover {
  background: var(--primary-600);
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 85, 255, 0.2);
}
```

### 3.6 Button with Icon

```css
.btn-icon {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.btn-icon svg {
  width: 20px;
  height: 20px;
  fill: currentColor;
  transition: transform var(--duration-fast) ease;
}

.btn-icon:hover svg {
  transform: translateX(4px);
}
```

---

## 4. 카드 컴포넌트

### 4.1 Feature Card

```css
.card-feature {
  position: relative;
  padding: 40px;
  background: var(--white);
  border: 1px solid var(--gray-100);
  border-radius: var(--radius-lg);
  transition: all var(--duration-normal) var(--ease);
  cursor: default;
}

.card-feature::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: var(--radius-lg);
  border: 2px solid var(--primary-500);
  opacity: 0;
  transition: opacity var(--duration-normal) ease;
}

.card-feature:hover {
  border-color: transparent;
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

.card-feature:hover::before {
  opacity: 1;
}

.card-feature-icon {
  width: 64px;
  height: 64px;
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #E6F0FF 0%, #F0F7FF 100%);
  border-radius: var(--radius-md);
  transition: all var(--duration-normal) var(--ease);
}

.card-feature:hover .card-feature-icon {
  background: linear-gradient(135deg, var(--primary-500) 0%, #0099FF 100%);
  transform: scale(1.1) rotate(5deg);
}

.card-feature-icon svg {
  width: 48px;
  height: 48px;
  fill: var(--primary-500);
  transition: fill var(--duration-normal) ease;
}

.card-feature:hover .card-feature-icon svg {
  fill: var(--white);
}

.card-feature-title {
  font-size: 22px;
  font-weight: 600;
  line-height: 30px;
  color: var(--gray-900);
  margin-bottom: 16px;
}

.card-feature-description {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-500);
  margin-bottom: 24px;
}

.card-feature-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 600;
  color: var(--primary-500);
  text-decoration: none;
  transition: all var(--duration-fast) ease;
}

.card-feature-link:hover {
  gap: 12px;
  color: var(--primary-600);
}
```

### 4.2 Portfolio Card

```css
.card-portfolio {
  background: var(--white);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: all var(--duration-normal) var(--ease);
  cursor: pointer;
}

.card-portfolio:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

.card-portfolio-image {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.card-portfolio-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--duration-slow) ease;
}

.card-portfolio:hover .card-portfolio-image img {
  transform: scale(1.08);
}

.card-portfolio-category {
  position: absolute;
  top: 20px;
  left: 20px;
  padding: 6px 12px;
  font-size: 12px;
  font-weight: 600;
  color: var(--white);
  background: rgba(0, 85, 255, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 6px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.card-portfolio-content {
  padding: 32px;
}

.card-portfolio-title {
  font-size: 22px;
  font-weight: 700;
  line-height: 32px;
  color: var(--gray-900);
  margin-bottom: 16px;
  transition: color var(--duration-fast) ease;
}

.card-portfolio:hover .card-portfolio-title {
  color: var(--primary-500);
}

.card-portfolio-description {
  font-size: 15px;
  font-weight: 400;
  line-height: 24px;
  color: var(--gray-500);
  margin-bottom: 24px;
}

.card-portfolio-metrics {
  display: flex;
  gap: 24px;
  padding: 24px 0;
  border-top: 1px solid var(--gray-100);
  border-bottom: 1px solid var(--gray-100);
  margin-bottom: 24px;
}

.card-portfolio-metric {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.card-portfolio-metric-value {
  font-size: 24px;
  font-weight: 700;
  color: var(--primary-500);
  line-height: 28px;
}

.card-portfolio-metric-label {
  font-size: 13px;
  font-weight: 500;
  color: var(--gray-500);
  line-height: 18px;
}
```

### 4.3 Testimonial Card

```css
.card-testimonial {
  position: relative;
  padding: 40px;
  background: var(--white);
  border: 1px solid var(--gray-100);
  border-radius: var(--radius-lg);
  transition: all var(--duration-normal) var(--ease);
}

.card-testimonial::before {
  content: '"';
  position: absolute;
  top: 32px;
  left: 32px;
  font-size: 80px;
  font-weight: 700;
  color: rgba(0, 85, 255, 0.08);
  line-height: 1;
  font-family: Georgia, serif;
  z-index: 0;
}

.card-testimonial:hover {
  border-color: var(--primary-500);
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

.card-testimonial-rating {
  display: flex;
  gap: 4px;
  margin-bottom: 24px;
  position: relative;
  z-index: 1;
}

.card-testimonial-star {
  width: 20px;
  height: 20px;
  fill: #FFB800;
}

.card-testimonial-quote {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-700);
  margin: 0 0 32px;
  position: relative;
  z-index: 1;
}

.card-testimonial-author {
  display: flex;
  align-items: center;
  gap: 16px;
  padding-top: 24px;
  border-top: 1px solid var(--gray-100);
}

.card-testimonial-avatar {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--gray-100);
}

.card-testimonial-info {
  flex: 1;
}

.card-testimonial-name {
  font-size: 16px;
  font-weight: 600;
  color: var(--gray-900);
  margin-bottom: 4px;
}

.card-testimonial-title {
  font-size: 14px;
  font-weight: 400;
  color: var(--gray-500);
  line-height: 20px;
}
```

### 4.4 Simple Card

```css
.card-simple {
  padding: 32px;
  background: var(--white);
  border: 1px solid var(--gray-100);
  border-radius: var(--radius-md);
  transition: all var(--duration-normal) var(--ease);
}

.card-simple:hover {
  border-color: var(--primary-500);
  box-shadow: var(--shadow-md);
}
```

---

## 5. 섹션 레이아웃

### 5.1 Section Header (중앙 정렬)

```css
.section-header {
  text-align: center;
  margin-bottom: 80px;
}

.section-title {
  font-size: 40px;
  font-weight: 700;
  line-height: 48px;
  letter-spacing: -0.5px;
  color: var(--gray-900);
  margin-bottom: 16px;
}

.section-subtitle {
  font-size: 18px;
  font-weight: 400;
  line-height: 28px;
  color: var(--gray-500);
}

@media (max-width: 767px) {
  .section-header {
    margin-bottom: 48px;
  }
  
  .section-title {
    font-size: 28px;
    line-height: 36px;
  }
  
  .section-subtitle {
    font-size: 16px;
    line-height: 24px;
  }
}
```

### 5.2 Hero Layout (Type 1: 좌우 분할)

```css
.hero-split {
  display: flex;
  align-items: center;
  gap: 80px;
  min-height: 600px;
}

.hero-split-left {
  flex: 1;
  max-width: 560px;
}

.hero-split-right {
  flex: 1;
  max-width: 640px;
}

@media (max-width: 991px) {
  .hero-split {
    flex-direction: column;
    gap: 48px;
    min-height: auto;
  }
  
  .hero-split-left,
  .hero-split-right {
    max-width: 100%;
  }
}
```

### 5.3 Hero Layout (Type 2: 중앙 정렬)

```css
.hero-center {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  min-height: 600px;
  padding: 120px 0;
}

.hero-center-content {
  max-width: 800px;
}
```

### 5.4 Content + Sidebar Layout

```css
.layout-sidebar {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 48px;
}

@media (max-width: 991px) {
  .layout-sidebar {
    grid-template-columns: 1fr;
  }
}
```

### 5.5 Two Column Layout

```css
.layout-two-column {
  display: grid;
  grid-template-columns: 480px 1fr;
  gap: 120px;
  align-items: flex-start;
}

@media (max-width: 991px) {
  .layout-two-column {
    grid-template-columns: 1fr;
    gap: 48px;
  }
}
```

---

## 6. 내비게이션

### 6.1 Breadcrumb

```css
.breadcrumb {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 16px 0;
  font-size: 14px;
  color: var(--gray-500);
}

.breadcrumb-item {
  display: flex;
  align-items: center;
  gap: 12px;
}

.breadcrumb-link {
  color: var(--gray-500);
  transition: color var(--duration-fast) ease;
}

.breadcrumb-link:hover {
  color: var(--primary-500);
}

.breadcrumb-separator {
  color: var(--gray-500);
}

.breadcrumb-current {
  color: var(--gray-900);
  font-weight: 600;
}
```

### 6.2 Pagination

```css
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 40px 0;
}

.pagination-item {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  font-size: 14px;
  font-weight: 600;
  color: var(--gray-700);
  background: var(--white);
  border: 1px solid var(--gray-200);
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
}

.pagination-item:hover {
  border-color: var(--primary-500);
  color: var(--primary-500);
}

.pagination-item.active {
  color: var(--white);
  background: var(--primary-500);
  border-color: var(--primary-500);
}

.pagination-item:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
```

### 6.3 Tab Navigation

```css
.tabs {
  display: flex;
  gap: 8px;
  background: var(--white);
  padding: 8px;
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
}

.tab-button {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 16px;
  height: 48px;
  font-size: 14px;
  font-weight: 600;
  color: var(--gray-500);
  background: transparent;
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
}

.tab-button:hover {
  color: var(--primary-500);
  background: rgba(0, 85, 255, 0.05);
}

.tab-button.active {
  color: var(--white);
  background: var(--primary-500);
  box-shadow: 0 2px 8px rgba(0, 85, 255, 0.25);
}
```

---

## 7. 폼 요소

### 7.1 Input

```css
.form-input {
  width: 100%;
  padding: 14px 16px;
  height: 48px;
  font-size: 15px;
  font-weight: 400;
  color: var(--gray-900);
  background: var(--white);
  border: 1px solid var(--gray-200);
  border-radius: var(--radius-sm);
  transition: all var(--duration-fast) var(--ease);
}

.form-input::placeholder {
  color: var(--gray-500);
}

.form-input:focus {
  outline: none;
  border-color: var(--primary-500);
  box-shadow: 0 0 0 3px rgba(0, 85, 255, 0.1);
}

.form-input:disabled {
  background: var(--gray-50);
  cursor: not-allowed;
}

.form-input.error {
  border-color: var(--error);
}
```

### 7.2 Textarea

```css
.form-textarea {
  width: 100%;
  padding: 14px 16px;
  min-height: 120px;
  font-size: 15px;
  font-weight: 400;
  color: var(--gray-900);
  background: var(--white);
  border: 1px solid var(--gray-200);
  border-radius: var(--radius-sm);
  resize: vertical;
  transition: all var(--duration-fast) var(--ease);
}

.form-textarea::placeholder {
  color: var(--gray-500);
}

.form-textarea:focus {
  outline: none;
  border-color: var(--primary-500);
  box-shadow: 0 0 0 3px rgba(0, 85, 255, 0.1);
}
```

### 7.3 Select

```css
.form-select {
  width: 100%;
  padding: 14px 16px;
  height: 48px;
  font-size: 15px;
  font-weight: 400;
  color: var(--gray-900);
  background: var(--white);
  border: 1px solid var(--gray-200);
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%236C757D' d='M6 9L1 4h10z'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 16px center;
  padding-right: 40px;
}

.form-select:focus {
  outline: none;
  border-color: var(--primary-500);
  box-shadow: 0 0 0 3px rgba(0, 85, 255, 0.1);
}
```

### 7.4 Checkbox

```css
.form-checkbox {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
}

.form-checkbox-input {
  width: 20px;
  height: 20px;
  border: 2px solid var(--gray-200);
  border-radius: 4px;
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
}

.form-checkbox-input:checked {
  background: var(--primary-500);
  border-color: var(--primary-500);
}

.form-checkbox-label {
  font-size: 15px;
  color: var(--gray-700);
}
```

### 7.5 Form Group

```css
.form-group {
  margin-bottom: 24px;
}

.form-label {
  display: block;
  font-size: 14px;
  font-weight: 600;
  color: var(--gray-900);
  margin-bottom: 8px;
}

.form-label-required::after {
  content: '*';
  color: var(--error);
  margin-left: 4px;
}

.form-help {
  display: block;
  font-size: 13px;
  color: var(--gray-500);
  margin-top: 6px;
}

.form-error {
  display: block;
  font-size: 13px;
  color: var(--error);
  margin-top: 6px;
}
```

---

## 8. 타이포그래피

### 8.1 Headings

```css
.heading-1 {
  font-size: 48px;
  font-weight: 700;
  line-height: 56px;
  letter-spacing: -0.5px;
  color: var(--gray-900);
}

.heading-2 {
  font-size: 40px;
  font-weight: 700;
  line-height: 48px;
  letter-spacing: -0.5px;
  color: var(--gray-900);
}

.heading-3 {
  font-size: 32px;
  font-weight: 700;
  line-height: 40px;
  letter-spacing: -0.3px;
  color: var(--gray-900);
}

.heading-4 {
  font-size: 28px;
  font-weight: 600;
  line-height: 36px;
  color: var(--gray-900);
}

.heading-5 {
  font-size: 24px;
  font-weight: 600;
  line-height: 32px;
  color: var(--gray-900);
}

.heading-6 {
  font-size: 20px;
  font-weight: 600;
  line-height: 28px;
  color: var(--gray-900);
}

/* Mobile Adjustments */
@media (max-width: 767px) {
  .heading-1 { font-size: 32px; line-height: 40px; }
  .heading-2 { font-size: 28px; line-height: 36px; }
  .heading-3 { font-size: 24px; line-height: 32px; }
  .heading-4 { font-size: 22px; line-height: 30px; }
  .heading-5 { font-size: 20px; line-height: 28px; }
  .heading-6 { font-size: 18px; line-height: 26px; }
}
```

### 8.2 Body Text

```css
.text-lg {
  font-size: 18px;
  font-weight: 400;
  line-height: 28px;
  color: var(--gray-700);
}

.text-base {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-700);
}

.text-sm {
  font-size: 14px;
  font-weight: 400;
  line-height: 22px;
  color: var(--gray-700);
}

.text-xs {
  font-size: 12px;
  font-weight: 400;
  line-height: 18px;
  color: var(--gray-700);
}
```

### 8.3 Gradient Text

```css
.text-gradient-primary {
  background: linear-gradient(135deg, var(--primary-500) 0%, #0099FF 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## 9. 애니메이션

### 9.1 Fade Animations

```css
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fade-in-down {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fade-in-left {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fade-in-right {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
```

### 9.2 Scale Animations

```css
@keyframes scale-in {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes zoom-in {
  from { transform: scale(1.1); }
  to { transform: scale(1); }
}
```

### 9.3 Special Animations

```css
@keyframes blob-float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
  }
  50% {
    transform: translate(30px, -30px) scale(1.05);
    border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
  }
}

@keyframes glow-pulse {
  0%, 100% { opacity: 0.6; }
  50% { opacity: 0.8; }
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### 9.4 Scroll Animation Utility

```css
.fade-in-on-scroll {
  opacity: 0;
  transform: translateY(50px);
}

.fade-in-on-scroll.is-visible {
  animation: fade-in-up 0.8s var(--ease) forwards;
}
```

---

## 10. 반응형 규칙

### 10.1 Breakpoints

```css
/* Tablet */
@media (max-width: 1199px) {
  /* 768px ~ 1199px */
}

@media (max-width: 991px) {
  /* 768px ~ 991px */
}

/* Mobile */
@media (max-width: 767px) {
  /* ~ 767px */
}
```

### 10.2 Touch Target (Mobile)

```css
@media (max-width: 767px) {
  /* Minimum 48px touch target */
  .btn-primary,
  .btn-secondary,
  .btn-outline,
  .form-input,
  .form-select,
  a {
    min-height: 48px;
    min-width: 48px;
  }
}
```

---

## 📚 컴포넌트 조합 예시

### Example 1: Feature Section

```html
<section class="section-lg">
  <div class="container">
    <div class="section-header">
      <h2 class="section-title">핵심 기능</h2>
      <p class="section-subtitle">검증된 AI 솔루션의 주요 기능</p>
    </div>
    
    <div class="grid-3">
      <div class="card-feature fade-in-on-scroll">
        <div class="card-feature-icon">
          <svg>...</svg>
        </div>
        <h3 class="card-feature-title">빠른 분석</h3>
        <p class="card-feature-description">실시간 데이터 분석...</p>
        <a href="#" class="card-feature-link">자세히 보기</a>
      </div>
      <!-- More cards... -->
    </div>
  </div>
</section>
```

### Example 2: Hero Section

```html
<section class="section-xl">
  <div class="container">
    <div class="hero-split">
      <div class="hero-split-left">
        <h1 class="heading-1">
          AI가 만드는 <span class="text-gradient-primary">신뢰할 수 있는 미래</span>
        </h1>
        <p class="text-lg">금융, 제조, 의료 모든 산업에서...</p>
        <div style="display: flex; gap: 16px; margin-top: 40px;">
          <button class="btn-primary">데모 신청하기</button>
          <button class="btn-secondary">솔루션 보기</button>
        </div>
      </div>
      <div class="hero-split-right">
        <img src="..." alt="..." />
      </div>
    </div>
  </div>
</section>
```

---

## ✅ 사용 가이드

### 새 페이지 개발 시

1. **레이아웃 선택**: `hero-split`, `hero-center`, `layout-two-column` 등
2. **섹션 간격**: `section-sm`, `section-md`, `section-lg`
3. **그리드**: `grid-2`, `grid-3`, `grid-4`
4. **카드 선택**: `card-feature`, `card-portfolio`, `card-testimonial`
5. **버튼**: `btn-primary`, `btn-secondary`, `btn-outline`
6. **타이포그래피**: `heading-1` ~ `heading-6`, `text-lg`, `text-base`

### 애니메이션 적용

```javascript
// Scroll Animation 적용
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('is-visible');
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.fade-in-on-scroll').forEach(el => {
  observer.observe(el);
});
```

---

**🎉 디자인 시스템 완성!**  
**이제 23개 페이지 개발 시 이 컴포넌트들을 조합하여 빠르게 구현 가능합니다.**
