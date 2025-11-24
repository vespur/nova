# 🎨 노바파트너스 HOME 페이지 - 픽셀 퍼펙트 스펙 (Part 1/3)

**작성 목적**: 클로드 코드가 바로 코딩 가능한 극도로 상세한 스펙  
**디자인 기준**: 1280px Container, 2026 Enterprise 트렌드  
**총 페이지 높이**: ~3800px (Desktop)

---

## 📐 전역 설정

### CSS Variables
```css
:root {
  /* Colors */
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
  
  /* Typography */
  --font-primary: 'Pretendard Variable', -apple-system, sans-serif;
  
  /* Spacing */
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-8: 48px;
  --space-10: 64px;
  --space-12: 80px;
  --space-15: 120px;
  
  /* Border Radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  
  /* Shadow */
  --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.08);
  --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.12);
  --shadow-lg: 0 8px 32px rgba(0, 0, 0, 0.16);
  
  /* Transition */
  --duration-fast: 0.2s;
  --duration-normal: 0.3s;
  --duration-slow: 0.6s;
  --ease: cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Container System
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

---

## 1️⃣ HEADER (Fixed, 80px 높이)

### 구조
- Position: Fixed, Top: 0
- Height: 80px
- Background: rgba(255,255,255,0.95) + Backdrop-blur
- Z-index: 1000
- Shadow: 0 2px 8px rgba(0,0,0,0.05)

### HTML 구조
```html
<header class="header">
  <div class="header-container">
    <div class="header-logo">
      <a href="/" class="logo">
        <img src="/logo.svg" alt="Nova Partners" />
      </a>
    </div>
    
    <nav class="header-nav">
      <ul class="nav-menu">
        <li class="nav-item">
          <a href="/solutions" class="nav-link has-dropdown">
            솔루션
          </a>
          <div class="dropdown-menu">
            <a href="/solutions/ai-platform" class="dropdown-item">AI 플랫폼</a>
            <a href="/solutions/industries" class="dropdown-item">산업별 솔루션</a>
          </div>
        </li>
        <li class="nav-item">
          <a href="/value" class="nav-link has-dropdown">가치</a>
        </li>
        <li class="nav-item">
          <a href="/support" class="nav-link has-dropdown">고객지원</a>
        </li>
        <li class="nav-item">
          <a href="/company" class="nav-link has-dropdown">회사소개</a>
        </li>
      </ul>
    </nav>
    
    <div class="header-actions">
      <button class="btn-search" aria-label="검색">
        <svg><!-- Search Icon --></svg>
      </button>
      <button class="btn-contact">문의하기</button>
      <button class="btn-support">기술지원</button>
    </div>
  </div>
</header>
```

### CSS 스펙
```css
/* Header Container */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 80px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  z-index: 1000;
  transition: all var(--duration-normal) var(--ease);
}

.header.scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.header-container {
  max-width: 1280px;
  height: 100%;
  margin: 0 auto;
  padding: 0 80px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* Logo */
.header-logo {
  flex-shrink: 0;
}

.logo {
  display: block;
  width: 200px;
  height: 60px;
  transition: opacity var(--duration-fast) ease;
}

.logo:hover {
  opacity: 0.8;
}

.logo img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

/* Navigation */
.header-nav {
  flex: 1;
  display: flex;
  justify-content: center;
  max-width: 560px;
  margin: 0 auto;
}

.nav-menu {
  display: flex;
  gap: 40px;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  position: relative;
}

.nav-link {
  display: block;
  padding: 28px 0;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  color: var(--gray-800);
  text-decoration: none;
  transition: color var(--duration-fast) ease;
  cursor: pointer;
}

.nav-link:hover {
  color: var(--primary-500);
}

/* Active Indicator */
.nav-link::after {
  content: '';
  position: absolute;
  bottom: 24px;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--primary-500);
  transform: scaleX(0);
  transform-origin: center;
  transition: transform var(--duration-normal) var(--ease);
}

.nav-link:hover::after,
.nav-link.active::after {
  transform: scaleX(1);
}

/* Dropdown Arrow */
.nav-link.has-dropdown {
  padding-right: 16px;
  position: relative;
}

.nav-link.has-dropdown::before {
  content: '';
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid currentColor;
  transition: transform var(--duration-fast) ease;
}

.nav-item:hover .nav-link.has-dropdown::before {
  transform: translateY(-50%) rotate(180deg);
}

/* Dropdown Menu */
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%) translateY(8px);
  min-width: 220px;
  background: var(--white);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-md);
  padding: 16px 0;
  opacity: 0;
  visibility: hidden;
  transition: all var(--duration-normal) var(--ease);
  pointer-events: none;
}

.nav-item:hover .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) translateY(0);
  pointer-events: auto;
}

.dropdown-item {
  display: block;
  padding: 12px 24px;
  font-size: 14px;
  font-weight: 400;
  color: var(--gray-800);
  text-decoration: none;
  transition: all var(--duration-fast) ease;
}

.dropdown-item:hover {
  background: var(--gray-50);
  color: var(--primary-500);
  padding-left: 28px;
}

/* Header Actions */
.header-actions {
  display: flex;
  gap: 12px;
  align-items: center;
}

/* Search Button */
.btn-search {
  width: 40px;
  height: 40px;
  border-radius: var(--radius-sm);
  border: none;
  background: transparent;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background var(--duration-fast) ease;
}

.btn-search:hover {
  background: var(--gray-50);
}

/* Contact Button */
.btn-contact {
  padding: 10px 20px;
  height: 40px;
  font-size: 14px;
  font-weight: 600;
  color: var(--primary-500);
  background: var(--white);
  border: 2px solid var(--primary-500);
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all var(--duration-fast) var(--ease);
  white-space: nowrap;
}

.btn-contact:hover {
  background: #E6F0FF;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0, 85, 255, 0.15);
}

/* Support Button */
.btn-support {
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
  box-shadow: 0 2px 8px rgba(0, 85, 255, 0.2);
  white-space: nowrap;
}

.btn-support:hover {
  background: var(--primary-600);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 85, 255, 0.3);
}

.btn-support:active {
  transform: translateY(0);
}
```

---

## 2️⃣ HERO SECTION (100vh, min 600px)

### 구조
- Height: 100vh (min-height: 600px)
- Padding: 120px 0 80px (Header 고려)
- Background: Gradient + Blob
- Layout: Flex (좌우 2열)
  - 좌측: 560px (콘텐츠)
  - 우측: 640px (비주얼)
  - Gap: 80px

### HTML 구조
```html
<section class="hero">
  <div class="hero-blob"></div>
  <div class="hero-container">
    <div class="hero-left">
      <h1 class="hero-title">
        AI가 만드는 
        <span class="hero-title-highlight">신뢰할 수 있는 미래</span>
      </h1>
      <p class="hero-subtitle">
        금융, 제조, 의료, 소매 모든 산업에서 검증된 AI 솔루션으로
        데이터를 신뢰로 바꾸세요.
      </p>
      <div class="hero-actions">
        <button class="btn-hero-primary">데모 신청하기</button>
        <button class="btn-hero-secondary">솔루션 보기</button>
      </div>
    </div>
    
    <div class="hero-right">
      <div class="hero-visual">
        <video class="hero-video" autoplay muted loop playsinline>
          <source src="/videos/hero-bg.mp4" type="video/mp4">
        </video>
        <div class="hero-visual-glow"></div>
      </div>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Hero Container */
.hero {
  position: relative;
  min-height: 100vh;
  min-height: 600px;
  display: flex;
  align-items: center;
  padding: 120px 0 80px;
  background: linear-gradient(
    135deg,
    rgba(0, 85, 255, 0.03) 0%,
    rgba(248, 249, 250, 1) 100%
  );
  overflow: hidden;
}

/* Background Blob */
.hero-blob {
  position: absolute;
  top: -200px;
  right: -200px;
  width: 800px;
  height: 800px;
  background: radial-gradient(
    circle,
    rgba(0, 85, 255, 0.08) 0%,
    rgba(0, 85, 255, 0) 70%
  );
  border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
  filter: blur(60px);
  animation: blob-float 20s ease-in-out infinite;
  pointer-events: none;
}

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

/* Hero Content Container */
.hero-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 80px;
  width: 100%;
}

/* Left Column */
.hero-left {
  flex: 0 0 560px;
  z-index: 2;
}

/* Right Column */
.hero-right {
  flex: 1;
  max-width: 640px;
  z-index: 1;
}

/* Hero Title */
.hero-title {
  font-size: 48px;
  font-weight: 700;
  line-height: 56px;
  letter-spacing: -0.5px;
  color: var(--gray-900);
  margin-bottom: 24px;
  
  /* Animation */
  opacity: 0;
  transform: translateY(30px);
  animation: fade-in-up 0.8s var(--ease) 0.2s forwards;
}

@keyframes fade-in-up {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Gradient Text Highlight */
.hero-title-highlight {
  background: linear-gradient(135deg, var(--primary-500) 0%, #0099FF 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Hero Subtitle */
.hero-subtitle {
  font-size: 18px;
  font-weight: 400;
  line-height: 28px;
  color: var(--gray-500);
  margin-bottom: 40px;
  max-width: 480px;
  
  /* Animation (Delayed) */
  opacity: 0;
  transform: translateY(30px);
  animation: fade-in-up 0.8s var(--ease) 0.4s forwards;
}

/* Hero Actions */
.hero-actions {
  display: flex;
  gap: 16px;
  
  /* Animation (Delayed) */
  opacity: 0;
  transform: translateY(30px);
  animation: fade-in-up 0.8s var(--ease) 0.6s forwards;
}

/* Primary Button */
.btn-hero-primary {
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
  box-shadow: 0 4px 16px rgba(0, 85, 255, 0.25);
  transition: all var(--duration-normal) var(--ease);
  position: relative;
  overflow: hidden;
  white-space: nowrap;
}

/* Ripple Effect */
.btn-hero-primary::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
  transform: translate(-50%, -50%);
  transition: width 0.6s ease, height 0.6s ease;
}

.btn-hero-primary:hover::before {
  width: 300px;
  height: 300px;
}

.btn-hero-primary:hover {
  background: var(--primary-600);
  transform: translateY(-3px);
  box-shadow: 0 8px 24px rgba(0, 85, 255, 0.35);
}

.btn-hero-primary:active {
  transform: translateY(-1px);
}

/* Secondary Button */
.btn-hero-secondary {
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

.btn-hero-secondary:hover {
  background: var(--gray-50);
  border-color: var(--primary-500);
  transform: translateY(-3px);
  box-shadow: 0 4px 12px rgba(0, 85, 255, 0.1);
}

/* Hero Visual */
.hero-visual {
  position: relative;
  width: 100%;
  height: 500px;
  border-radius: var(--radius-xl);
  overflow: hidden;
  
  /* Animation */
  opacity: 0;
  transform: translateX(50px);
  animation: fade-in-right 1s var(--ease) 0.4s forwards;
}

@keyframes fade-in-right {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Background Video */
.hero-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Glow Effect */
.hero-visual::after {
  content: '';
  position: absolute;
  inset: -4px;
  background: linear-gradient(
    135deg,
    rgba(0, 85, 255, 0.4) 0%,
    rgba(0, 153, 255, 0.4) 100%
  );
  border-radius: var(--radius-xl);
  filter: blur(20px);
  opacity: 0.6;
  z-index: -1;
  animation: glow-pulse 3s ease-in-out infinite;
}

@keyframes glow-pulse {
  0%, 100% { opacity: 0.6; }
  50% { opacity: 0.8; }
}
```

---

**Part 1 완료. Part 2에서 계속...**
