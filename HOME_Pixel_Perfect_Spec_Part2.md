# 🎨 노바파트너스 HOME 페이지 - 픽셀 퍼펙트 스펙 (Part 2/3)

**이어서 작성**: Features → Solutions → Trust Signal → Portfolio  
**기준**: 1280px Container, 픽셀 단위 정확도

---

## 3️⃣ FEATURES SECTION (높이: ~700px)

### 구조
- Padding: 120px 0
- Background: var(--white)
- 제목 영역: 중앙 정렬
- Feature Cards: Grid 3열 (각 380px)
- Gap: 32px

### HTML 구조
```html
<section class="features">
  <div class="features-container">
    <!-- Section Header -->
    <div class="features-header">
      <h2 class="section-title">왜 노바파트너스인가</h2>
      <p class="section-subtitle">
        기업의 AI 혁신을 완성하는 4가지 핵심 가치
      </p>
    </div>
    
    <!-- Feature Cards Grid -->
    <div class="features-grid">
      <!-- Feature Card 1 -->
      <div class="feature-card">
        <div class="feature-icon">
          <svg width="48" height="48"><!-- Trust Icon --></svg>
        </div>
        <h3 class="feature-title">검증된 신뢰성</h3>
        <p class="feature-description">
          금융권 99.8% 정확도, 의료 분야 FDA 인증 획득. 실제 비즈니스에서 입증된 성능.
        </p>
        <a href="/value/trust" class="feature-link">
          자세히 보기 
          <svg width="16" height="16"><!-- Arrow --></svg>
        </a>
      </div>
      
      <!-- Feature Card 2 -->
      <div class="feature-card">
        <div class="feature-icon">
          <svg width="48" height="48"><!-- Speed Icon --></svg>
        </div>
        <h3 class="feature-title">빠른 도입</h3>
        <p class="feature-description">
          평균 6주 만에 운영 시작. 레거시 시스템과의 원활한 통합으로 비즈니스 중단 없이 전환.
        </p>
        <a href="/value/speed" class="feature-link">
          자세히 보기 
          <svg width="16" height="16"><!-- Arrow --></svg>
        </a>
      </div>
      
      <!-- Feature Card 3 -->
      <div class="feature-card">
        <div class="feature-icon">
          <svg width="48" height="48"><!-- Security Icon --></svg>
        </div>
        <h3 class="feature-title">완전한 보안</h3>
        <p class="feature-description">
          ISO 27001, SOC2 Type II 인증. On-premise 및 프라이빗 클라우드 지원으로 데이터 주권 보장.
        </p>
        <a href="/value/security" class="feature-link">
          자세히 보기 
          <svg width="16" height="16"><!-- Arrow --></svg>
        </a>
      </div>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Features Section */
.features {
  padding: 120px 0;
  background: var(--white);
}

.features-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

/* Section Header (재사용 가능) */
.features-header {
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

/* Features Grid */
.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

/* Feature Card */
.feature-card {
  position: relative;
  padding: 40px;
  background: var(--white);
  border: 1px solid var(--gray-100);
  border-radius: var(--radius-lg);
  transition: all var(--duration-normal) var(--ease);
  cursor: default;
}

.feature-card::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: var(--radius-lg);
  border: 2px solid var(--primary-500);
  opacity: 0;
  transition: opacity var(--duration-normal) ease;
}

.feature-card:hover {
  border-color: transparent;
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

.feature-card:hover::before {
  opacity: 1;
}

/* Feature Icon */
.feature-icon {
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

.feature-card:hover .feature-icon {
  background: linear-gradient(135deg, var(--primary-500) 0%, #0099FF 100%);
  transform: scale(1.1) rotate(5deg);
}

.feature-icon svg {
  width: 48px;
  height: 48px;
  fill: var(--primary-500);
  transition: fill var(--duration-normal) ease;
}

.feature-card:hover .feature-icon svg {
  fill: var(--white);
}

/* Feature Title */
.feature-title {
  font-size: 22px;
  font-weight: 600;
  line-height: 30px;
  color: var(--gray-900);
  margin-bottom: 16px;
}

/* Feature Description */
.feature-description {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-500);
  margin-bottom: 24px;
}

/* Feature Link */
.feature-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 600;
  color: var(--primary-500);
  text-decoration: none;
  transition: all var(--duration-fast) ease;
}

.feature-link:hover {
  gap: 12px;
  color: var(--primary-600);
}

.feature-link svg {
  width: 16px;
  height: 16px;
  fill: currentColor;
  transition: transform var(--duration-fast) ease;
}

.feature-link:hover svg {
  transform: translateX(4px);
}

/* Scroll Animation */
.feature-card {
  opacity: 0;
  transform: translateY(50px);
}

.feature-card.is-visible {
  animation: fade-in-up 0.8s var(--ease) forwards;
}

.feature-card:nth-child(1) { animation-delay: 0.1s; }
.feature-card:nth-child(2) { animation-delay: 0.2s; }
.feature-card:nth-child(3) { animation-delay: 0.3s; }
```

---

## 4️⃣ SOLUTIONS SECTION (높이: ~900px)

### 구조
- Padding: 120px 0
- Background: var(--gray-50)
- 레이아웃: 좌우 2열
  - 좌측: 480px (콘텐츠)
  - 우측: 680px (Tabs + 비주얼)
  - Gap: 120px

### HTML 구조
```html
<section class="solutions">
  <div class="solutions-container">
    <!-- Left Content -->
    <div class="solutions-left">
      <div class="solutions-tag">SOLUTIONS</div>
      <h2 class="solutions-title">모든 산업을 위한<br>맞춤형 AI 솔루션</h2>
      <p class="solutions-description">
        금융, 제조, 의료, 소매까지. 각 산업의 특성과 규제를 완벽히 이해한 
        맞춤형 솔루션으로 AI 전환을 성공시킵니다.
      </p>
      
      <div class="solutions-stats">
        <div class="stat-item">
          <div class="stat-number">150+</div>
          <div class="stat-label">구축 프로젝트</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">99.2%</div>
          <div class="stat-label">고객 만족도</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">6주</div>
          <div class="stat-label">평균 도입 기간</div>
        </div>
      </div>
      
      <a href="/solutions" class="btn-solutions">
        모든 솔루션 보기
        <svg width="20" height="20"><!-- Arrow --></svg>
      </a>
    </div>
    
    <!-- Right Visual (Tabs) -->
    <div class="solutions-right">
      <div class="solutions-tabs">
        <button class="tab-button active" data-tab="finance">
          <svg width="24" height="24"><!-- Icon --></svg>
          금융
        </button>
        <button class="tab-button" data-tab="manufacturing">
          <svg width="24" height="24"><!-- Icon --></svg>
          제조
        </button>
        <button class="tab-button" data-tab="healthcare">
          <svg width="24" height="24"><!-- Icon --></svg>
          의료
        </button>
        <button class="tab-button" data-tab="retail">
          <svg width="24" height="24"><!-- Icon --></svg>
          소매
        </button>
      </div>
      
      <div class="solutions-content">
        <!-- Finance Tab Content -->
        <div class="tab-content active" data-content="finance">
          <div class="tab-visual">
            <img src="/images/solutions-finance.jpg" alt="금융 AI 솔루션" />
          </div>
          <div class="tab-info">
            <h3 class="tab-title">금융권 AI 플랫폼</h3>
            <p class="tab-description">
              실시간 사기 탐지, 신용평가 자동화, 투자 리스크 분석. 
              금융권 특화 AI로 업무 효율 300% 향상.
            </p>
            <ul class="tab-features">
              <li>99.8% 이상 정확도</li>
              <li>규제 완전 준수</li>
              <li>실시간 모니터링</li>
            </ul>
          </div>
        </div>
        
        <!-- Manufacturing Tab Content -->
        <div class="tab-content" data-content="manufacturing">
          <div class="tab-visual">
            <img src="/images/solutions-manufacturing.jpg" alt="제조 AI 솔루션" />
          </div>
          <div class="tab-info">
            <h3 class="tab-title">스마트 팩토리</h3>
            <p class="tab-description">
              예측 정비, 품질 검사 자동화, 생산 최적화. 
              제조 공정 전반에 AI를 통합합니다.
            </p>
            <ul class="tab-features">
              <li>불량률 40% 감소</li>
              <li>가동률 25% 증가</li>
              <li>에너지 비용 절감</li>
            </ul>
          </div>
        </div>
        
        <!-- Healthcare Tab Content -->
        <div class="tab-content" data-content="healthcare">
          <div class="tab-visual">
            <img src="/images/solutions-healthcare.jpg" alt="의료 AI 솔루션" />
          </div>
          <div class="tab-info">
            <h3 class="tab-title">의료 진단 지원</h3>
            <p class="tab-description">
              영상 분석, 진단 보조, 환자 모니터링. 
              FDA 인증 받은 의료 AI로 진료 품질을 높입니다.
            </p>
            <ul class="tab-features">
              <li>FDA 인증 획득</li>
              <li>진단 시간 60% 단축</li>
              <li>정확도 96.5%</li>
            </ul>
          </div>
        </div>
        
        <!-- Retail Tab Content -->
        <div class="tab-content" data-content="retail">
          <div class="tab-visual">
            <img src="/images/solutions-retail.jpg" alt="소매 AI 솔루션" />
          </div>
          <div class="tab-info">
            <h3 class="tab-title">개인화 추천 엔진</h3>
            <p class="tab-description">
              고객 행동 분석, 재고 최적화, 수요 예측. 
              소매 비즈니스 전 영역을 AI로 혁신합니다.
            </p>
            <ul class="tab-features">
              <li>전환율 180% 증가</li>
              <li>재고 회전률 개선</li>
              <li>고객 만족도 향상</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Solutions Section */
.solutions {
  padding: 120px 0;
  background: var(--gray-50);
}

.solutions-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
  display: flex;
  align-items: flex-start;
  gap: 120px;
}

/* Left Content */
.solutions-left {
  flex: 0 0 480px;
}

.solutions-tag {
  display: inline-block;
  padding: 6px 12px;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.5px;
  color: var(--primary-500);
  background: rgba(0, 85, 255, 0.08);
  border-radius: 4px;
  margin-bottom: 24px;
  text-transform: uppercase;
}

.solutions-title {
  font-size: 40px;
  font-weight: 700;
  line-height: 52px;
  letter-spacing: -0.5px;
  color: var(--gray-900);
  margin-bottom: 24px;
}

.solutions-description {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-500);
  margin-bottom: 48px;
}

/* Stats Grid */
.solutions-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  margin-bottom: 48px;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 36px;
  font-weight: 700;
  line-height: 44px;
  color: var(--primary-500);
  margin-bottom: 8px;
}

.stat-label {
  font-size: 14px;
  font-weight: 500;
  color: var(--gray-500);
  line-height: 20px;
}

/* Solutions Button */
.btn-solutions {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 28px;
  height: 48px;
  font-size: 16px;
  font-weight: 600;
  color: var(--white);
  background: var(--primary-500);
  border: none;
  border-radius: var(--radius-md);
  text-decoration: none;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 85, 255, 0.2);
  transition: all var(--duration-normal) var(--ease);
}

.btn-solutions:hover {
  background: var(--primary-600);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 85, 255, 0.3);
  gap: 12px;
}

.btn-solutions svg {
  width: 20px;
  height: 20px;
  fill: currentColor;
}

/* Right Visual Area */
.solutions-right {
  flex: 1;
  max-width: 680px;
}

/* Tabs Navigation */
.solutions-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 32px;
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

.tab-button svg {
  width: 24px;
  height: 24px;
  fill: currentColor;
  transition: all var(--duration-fast) ease;
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

.tab-button.active svg {
  fill: var(--white);
}

/* Tab Content Container */
.solutions-content {
  position: relative;
  min-height: 560px;
}

.tab-content {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  opacity: 0;
  visibility: hidden;
  transform: translateY(20px);
  transition: all var(--duration-normal) var(--ease);
  pointer-events: none;
}

.tab-content.active {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
  pointer-events: auto;
}

/* Tab Visual */
.tab-visual {
  position: relative;
  width: 100%;
  height: 360px;
  margin-bottom: 32px;
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-md);
}

.tab-visual img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--duration-slow) ease;
}

.tab-content.active .tab-visual img {
  animation: zoom-in 0.8s var(--ease) forwards;
}

@keyframes zoom-in {
  from {
    transform: scale(1.1);
  }
  to {
    transform: scale(1);
  }
}

/* Gradient Overlay */
.tab-visual::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(0, 0, 0, 0) 0%,
    rgba(0, 0, 0, 0.3) 100%
  );
}

/* Tab Info */
.tab-info {
  padding: 0 8px;
}

.tab-title {
  font-size: 28px;
  font-weight: 700;
  line-height: 36px;
  color: var(--gray-900);
  margin-bottom: 16px;
}

.tab-description {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-500);
  margin-bottom: 24px;
}

/* Tab Features List */
.tab-features {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.tab-features li {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 500;
  color: var(--gray-700);
  padding: 8px 16px;
  background: rgba(0, 85, 255, 0.08);
  border-radius: 20px;
}

.tab-features li::before {
  content: '✓';
  display: flex;
  align-items: center;
  justify-content: center;
  width: 18px;
  height: 18px;
  font-size: 12px;
  font-weight: 700;
  color: var(--white);
  background: var(--primary-500);
  border-radius: 50%;
}
```

---

## 5️⃣ TRUST SIGNAL SECTION (높이: ~400px)

### 구조
- Padding: 80px 0
- Background: var(--white)
- 레이아웃: 상하 2단
  - 상단: 제목 + 설명 (중앙)
  - 하단: Logo Grid (5열)

### HTML 구조
```html
<section class="trust-signal">
  <div class="trust-container">
    <div class="trust-header">
      <h2 class="trust-title">신뢰하는 기업들</h2>
      <p class="trust-subtitle">
        글로벌 Top 100 기업 중 32개사가 노바파트너스를 선택했습니다
      </p>
    </div>
    
    <div class="trust-logos">
      <div class="logo-item">
        <img src="/logos/samsung.svg" alt="Samsung" />
      </div>
      <div class="logo-item">
        <img src="/logos/hyundai.svg" alt="Hyundai" />
      </div>
      <div class="logo-item">
        <img src="/logos/lg.svg" alt="LG" />
      </div>
      <div class="logo-item">
        <img src="/logos/sk.svg" alt="SK" />
      </div>
      <div class="logo-item">
        <img src="/logos/posco.svg" alt="POSCO" />
      </div>
      <div class="logo-item">
        <img src="/logos/hana.svg" alt="Hana Financial" />
      </div>
      <div class="logo-item">
        <img src="/logos/kb.svg" alt="KB" />
      </div>
      <div class="logo-item">
        <img src="/logos/shinhan.svg" alt="Shinhan" />
      </div>
      <div class="logo-item">
        <img src="/logos/naver.svg" alt="Naver" />
      </div>
      <div class="logo-item">
        <img src="/logos/kakao.svg" alt="Kakao" />
      </div>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Trust Signal Section */
.trust-signal {
  padding: 80px 0;
  background: var(--white);
  border-top: 1px solid var(--gray-100);
}

.trust-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

/* Trust Header */
.trust-header {
  text-align: center;
  margin-bottom: 64px;
}

.trust-title {
  font-size: 32px;
  font-weight: 700;
  line-height: 40px;
  color: var(--gray-900);
  margin-bottom: 12px;
}

.trust-subtitle {
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  color: var(--gray-500);
}

/* Logos Grid */
.trust-logos {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 48px 32px;
  align-items: center;
}

/* Logo Item */
.logo-item {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 64px;
  padding: 0 16px;
  opacity: 0.5;
  transition: all var(--duration-normal) var(--ease);
  cursor: default;
}

.logo-item:hover {
  opacity: 1;
  transform: scale(1.1);
}

.logo-item img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  filter: grayscale(100%);
  transition: filter var(--duration-normal) ease;
}

.logo-item:hover img {
  filter: grayscale(0%);
}

/* Scroll Animation */
.logo-item {
  opacity: 0;
  transform: translateY(30px);
}

.logo-item.is-visible {
  animation: fade-in-up 0.6s var(--ease) forwards;
}

.logo-item:nth-child(1) { animation-delay: 0.05s; }
.logo-item:nth-child(2) { animation-delay: 0.1s; }
.logo-item:nth-child(3) { animation-delay: 0.15s; }
.logo-item:nth-child(4) { animation-delay: 0.2s; }
.logo-item:nth-child(5) { animation-delay: 0.25s; }
.logo-item:nth-child(6) { animation-delay: 0.3s; }
.logo-item:nth-child(7) { animation-delay: 0.35s; }
.logo-item:nth-child(8) { animation-delay: 0.4s; }
.logo-item:nth-child(9) { animation-delay: 0.45s; }
.logo-item:nth-child(10) { animation-delay: 0.5s; }
```

---

## 6️⃣ PORTFOLIO SECTION (높이: ~900px)

### 구조
- Padding: 120px 0
- Background: var(--gray-50)
- 제목 영역: 중앙 정렬
- Cards: Grid 2열 (각 600px)
- Gap: 32px

### HTML 구조
```html
<section class="portfolio">
  <div class="portfolio-container">
    <!-- Section Header -->
    <div class="portfolio-header">
      <h2 class="section-title">검증된 성공 사례</h2>
      <p class="section-subtitle">
        다양한 산업에서 입증된 ROI와 비즈니스 성과
      </p>
    </div>
    
    <!-- Portfolio Grid -->
    <div class="portfolio-grid">
      <!-- Case 1 -->
      <article class="portfolio-card">
        <div class="portfolio-image">
          <img src="/images/case-finance.jpg" alt="금융권 사기 탐지 시스템" />
          <div class="portfolio-category">금융</div>
        </div>
        <div class="portfolio-content">
          <h3 class="portfolio-title">
            실시간 사기 탐지로 연간 120억원 손실 방지
          </h3>
          <p class="portfolio-description">
            K은행은 노바파트너스 AI로 이상 거래 탐지 정확도를 
            99.8%까지 끌어올렸습니다.
          </p>
          <div class="portfolio-metrics">
            <div class="metric">
              <span class="metric-value">99.8%</span>
              <span class="metric-label">정확도</span>
            </div>
            <div class="metric">
              <span class="metric-value">120억</span>
              <span class="metric-label">손실 방지</span>
            </div>
            <div class="metric">
              <span class="metric-value">0.3초</span>
              <span class="metric-label">처리 시간</span>
            </div>
          </div>
          <a href="/portfolio/case-finance" class="portfolio-link">
            사례 자세히 보기
            <svg width="16" height="16"><!-- Arrow --></svg>
          </a>
        </div>
      </article>
      
      <!-- Case 2 -->
      <article class="portfolio-card">
        <div class="portfolio-image">
          <img src="/images/case-manufacturing.jpg" alt="제조 품질 검사 자동화" />
          <div class="portfolio-category">제조</div>
        </div>
        <div class="portfolio-content">
          <h3 class="portfolio-title">
            AI 품질 검사로 불량률 68% 감소
          </h3>
          <p class="portfolio-description">
            H자동차는 비전 AI 도입 후 검사 시간을 85% 단축하고 
            불량률을 획기적으로 낮췄습니다.
          </p>
          <div class="portfolio-metrics">
            <div class="metric">
              <span class="metric-value">68%</span>
              <span class="metric-label">불량률 감소</span>
            </div>
            <div class="metric">
              <span class="metric-value">85%</span>
              <span class="metric-label">시간 단축</span>
            </div>
            <div class="metric">
              <span class="metric-value">12억</span>
              <span class="metric-label">비용 절감</span>
            </div>
          </div>
          <a href="/portfolio/case-manufacturing" class="portfolio-link">
            사례 자세히 보기
            <svg width="16" height="16"><!-- Arrow --></svg>
          </a>
        </div>
      </article>
      
      <!-- Case 3 -->
      <article class="portfolio-card">
        <div class="portfolio-image">
          <img src="/images/case-healthcare.jpg" alt="의료 진단 보조 AI" />
          <div class="portfolio-category">의료</div>
        </div>
        <div class="portfolio-content">
          <h3 class="portfolio-title">
            AI 진단 보조로 조기 발견율 42% 향상
          </h3>
          <p class="portfolio-description">
            S병원은 영상 분석 AI를 통해 진단 정확도를 높이고 
            환자 대기 시간을 60% 줄였습니다.
          </p>
          <div class="portfolio-metrics">
            <div class="metric">
              <span class="metric-value">96.5%</span>
              <span class="metric-label">진단 정확도</span>
            </div>
            <div class="metric">
              <span class="metric-value">42%</span>
              <span class="metric-label">조기 발견</span>
            </div>
            <div class="metric">
              <span class="metric-value">60%</span>
              <span class="metric-label">대기시간 단축</span>
            </div>
          </div>
          <a href="/portfolio/case-healthcare" class="portfolio-link">
            사례 자세히 보기
            <svg width="16" height="16"><!-- Arrow --></svg>
          </a>
        </div>
      </article>
      
      <!-- Case 4 -->
      <article class="portfolio-card">
        <div class="portfolio-image">
          <img src="/images/case-retail.jpg" alt="소매 추천 엔진" />
          <div class="portfolio-category">소매</div>
        </div>
        <div class="portfolio-content">
          <h3 class="portfolio-title">
            개인화 추천으로 전환율 280% 증가
          </h3>
          <p class="portfolio-description">
            N쇼핑은 AI 추천 엔진 도입 후 구매 전환율이 급증하고 
            고객당 평균 구매액이 2.8배 증가했습니다.
          </p>
          <div class="portfolio-metrics">
            <div class="metric">
              <span class="metric-value">280%</span>
              <span class="metric-label">전환율 증가</span>
            </div>
            <div class="metric">
              <span class="metric-value">2.8배</span>
              <span class="metric-label">구매액 증가</span>
            </div>
            <div class="metric">
              <span class="metric-value">180억</span>
              <span class="metric-label">매출 증대</span>
            </div>
          </div>
          <a href="/portfolio/case-retail" class="portfolio-link">
            사례 자세히 보기
            <svg width="16" height="16"><!-- Arrow --></svg>
          </a>
        </div>
      </article>
    </div>
    
    <!-- View All Button -->
    <div class="portfolio-footer">
      <a href="/portfolio" class="btn-view-all">
        모든 사례 보기 (32+)
        <svg width="20" height="20"><!-- Arrow --></svg>
      </a>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Portfolio Section */
.portfolio {
  padding: 120px 0;
  background: var(--gray-50);
}

.portfolio-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

/* Portfolio Header */
.portfolio-header {
  text-align: center;
  margin-bottom: 80px;
}

/* Portfolio Grid */
.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 32px;
  margin-bottom: 64px;
}

/* Portfolio Card */
.portfolio-card {
  background: var(--white);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: all var(--duration-normal) var(--ease);
  cursor: pointer;
}

.portfolio-card:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

/* Portfolio Image */
.portfolio-image {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.portfolio-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--duration-slow) ease;
}

.portfolio-card:hover .portfolio-image img {
  transform: scale(1.08);
}

/* Category Badge */
.portfolio-category {
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

/* Portfolio Content */
.portfolio-content {
  padding: 32px;
}

.portfolio-title {
  font-size: 22px;
  font-weight: 700;
  line-height: 32px;
  color: var(--gray-900);
  margin-bottom: 16px;
  transition: color var(--duration-fast) ease;
}

.portfolio-card:hover .portfolio-title {
  color: var(--primary-500);
}

.portfolio-description {
  font-size: 15px;
  font-weight: 400;
  line-height: 24px;
  color: var(--gray-500);
  margin-bottom: 24px;
}

/* Metrics Grid */
.portfolio-metrics {
  display: flex;
  gap: 24px;
  padding: 24px 0;
  border-top: 1px solid var(--gray-100);
  border-bottom: 1px solid var(--gray-100);
  margin-bottom: 24px;
}

.metric {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.metric-value {
  font-size: 24px;
  font-weight: 700;
  color: var(--primary-500);
  line-height: 28px;
}

.metric-label {
  font-size: 13px;
  font-weight: 500;
  color: var(--gray-500);
  line-height: 18px;
}

/* Portfolio Link */
.portfolio-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 15px;
  font-weight: 600;
  color: var(--primary-500);
  text-decoration: none;
  transition: all var(--duration-fast) ease;
}

.portfolio-link:hover {
  gap: 12px;
  color: var(--primary-600);
}

.portfolio-link svg {
  width: 16px;
  height: 16px;
  fill: currentColor;
  transition: transform var(--duration-fast) ease;
}

.portfolio-link:hover svg {
  transform: translateX(4px);
}

/* Portfolio Footer */
.portfolio-footer {
  text-align: center;
}

.btn-view-all {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 16px 32px;
  height: 56px;
  font-size: 16px;
  font-weight: 600;
  color: var(--primary-500);
  background: var(--white);
  border: 2px solid var(--primary-500);
  border-radius: var(--radius-md);
  text-decoration: none;
  cursor: pointer;
  transition: all var(--duration-normal) var(--ease);
}

.btn-view-all:hover {
  color: var(--white);
  background: var(--primary-500);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 85, 255, 0.3);
  gap: 16px;
}

.btn-view-all svg {
  width: 20px;
  height: 20px;
  fill: currentColor;
}

/* Scroll Animation */
.portfolio-card {
  opacity: 0;
  transform: translateY(50px);
}

.portfolio-card.is-visible {
  animation: fade-in-up 0.8s var(--ease) forwards;
}

.portfolio-card:nth-child(1) { animation-delay: 0.1s; }
.portfolio-card:nth-child(2) { animation-delay: 0.2s; }
.portfolio-card:nth-child(3) { animation-delay: 0.3s; }
.portfolio-card:nth-child(4) { animation-delay: 0.4s; }
```

---

**Part 2 완료.**  
Part 3에서 Testimonials, CTA, Footer + 반응형 + JavaScript 완성합니다.
