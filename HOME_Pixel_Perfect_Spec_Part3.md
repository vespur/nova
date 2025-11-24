# 🎨 노바파트너스 HOME 페이지 - 픽셀 퍼펙트 스펙 (Part 3/3 - 최종)

**마지막 섹션**: Testimonials → CTA → Footer  
**추가**: 반응형 Breakpoints + JavaScript Interactions  
**완성도**: 클로드 코드 즉시 코딩 가능 수준

---

## 7️⃣ TESTIMONIALS SECTION (높이: ~800px)

### 구조
- Padding: 120px 0
- Background: var(--white)
- 레이아웃: 상하 2단
  - 상단: 제목 (중앙)
  - 하단: 3열 Grid (각 380px)
- Carousel 슬라이드 (선택 사항)

### HTML 구조
```html
<section class="testimonials">
  <div class="testimonials-container">
    <!-- Section Header -->
    <div class="testimonials-header">
      <h2 class="section-title">고객의 목소리</h2>
      <p class="section-subtitle">
        실제 고객사의 생생한 변화 스토리
      </p>
    </div>
    
    <!-- Testimonials Grid -->
    <div class="testimonials-grid">
      <!-- Testimonial 1 -->
      <article class="testimonial-card">
        <div class="testimonial-rating">
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
        </div>
        <blockquote class="testimonial-quote">
          "6주 만에 AI 사기 탐지 시스템을 구축했고, 첫 달부터 120억원의 
          손실을 막았습니다. 정확도도 기존 시스템 대비 40% 향상됐어요."
        </blockquote>
        <div class="testimonial-author">
          <img src="/images/avatar-kim.jpg" alt="김영수" class="author-avatar" />
          <div class="author-info">
            <div class="author-name">김영수</div>
            <div class="author-title">리스크관리본부장, K은행</div>
          </div>
        </div>
      </article>
      
      <!-- Testimonial 2 -->
      <article class="testimonial-card">
        <div class="testimonial-rating">
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
        </div>
        <blockquote class="testimonial-quote">
          "제조 현장에 AI를 도입한다는 게 막막했는데, 노바파트너스 덕분에 
          불량률이 68% 줄었고 생산성도 크게 올랐습니다."
        </blockquote>
        <div class="testimonial-author">
          <img src="/images/avatar-park.jpg" alt="박민호" class="author-avatar" />
          <div class="author-info">
            <div class="author-name">박민호</div>
            <div class="author-title">스마트팩토리 담당, H자동차</div>
          </div>
        </div>
      </article>
      
      <!-- Testimonial 3 -->
      <article class="testimonial-card">
        <div class="testimonial-rating">
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
          <svg class="star">★</svg>
        </div>
        <blockquote class="testimonial-quote">
          "FDA 승인까지 지원받으며 의료 AI를 안전하게 도입했습니다. 
          환자 대기 시간이 60% 줄어 만족도가 크게 높아졌어요."
        </blockquote>
        <div class="testimonial-author">
          <img src="/images/avatar-lee.jpg" alt="이수진" class="author-avatar" />
          <div class="author-info">
            <div class="author-name">이수진</div>
            <div class="author-title">영상의학과장, S병원</div>
          </div>
        </div>
      </article>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* Testimonials Section */
.testimonials {
  padding: 120px 0;
  background: var(--white);
}

.testimonials-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

/* Testimonials Header */
.testimonials-header {
  text-align: center;
  margin-bottom: 80px;
}

/* Testimonials Grid */
.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

/* Testimonial Card */
.testimonial-card {
  position: relative;
  padding: 40px;
  background: var(--white);
  border: 1px solid var(--gray-100);
  border-radius: var(--radius-lg);
  transition: all var(--duration-normal) var(--ease);
  cursor: default;
}

.testimonial-card::before {
  content: '"';
  position: absolute;
  top: 32px;
  left: 32px;
  font-size: 80px;
  font-weight: 700;
  color: rgba(0, 85, 255, 0.08);
  line-height: 1;
  font-family: Georgia, serif;
}

.testimonial-card:hover {
  border-color: var(--primary-500);
  box-shadow: var(--shadow-lg);
  transform: translateY(-8px);
}

/* Rating Stars */
.testimonial-rating {
  display: flex;
  gap: 4px;
  margin-bottom: 24px;
  position: relative;
  z-index: 1;
}

.star {
  width: 20px;
  height: 20px;
  fill: #FFB800;
}

/* Quote */
.testimonial-quote {
  font-size: 16px;
  font-weight: 400;
  line-height: 26px;
  color: var(--gray-700);
  margin: 0 0 32px;
  position: relative;
  z-index: 1;
}

/* Author */
.testimonial-author {
  display: flex;
  align-items: center;
  gap: 16px;
  padding-top: 24px;
  border-top: 1px solid var(--gray-100);
}

.author-avatar {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--gray-100);
}

.author-info {
  flex: 1;
}

.author-name {
  font-size: 16px;
  font-weight: 600;
  color: var(--gray-900);
  margin-bottom: 4px;
}

.author-title {
  font-size: 14px;
  font-weight: 400;
  color: var(--gray-500);
  line-height: 20px;
}

/* Scroll Animation */
.testimonial-card {
  opacity: 0;
  transform: translateY(50px);
}

.testimonial-card.is-visible {
  animation: fade-in-up 0.8s var(--ease) forwards;
}

.testimonial-card:nth-child(1) { animation-delay: 0.1s; }
.testimonial-card:nth-child(2) { animation-delay: 0.2s; }
.testimonial-card:nth-child(3) { animation-delay: 0.3s; }
```

---

## 8️⃣ CTA SECTION (높이: ~400px)

### 구조
- Padding: 120px 0
- Background: Linear Gradient (Primary)
- 레이아웃: 중앙 정렬
- Content Width: 720px

### HTML 구조
```html
<section class="cta">
  <div class="cta-container">
    <div class="cta-content">
      <h2 class="cta-title">AI 전환, 지금 시작하세요</h2>
      <p class="cta-subtitle">
        무료 컨설팅으로 귀사에 최적화된 AI 솔루션을 제안합니다.
        <br>평균 6주 만에 운영을 시작할 수 있습니다.
      </p>
      <div class="cta-actions">
        <button class="btn-cta-primary">무료 상담 신청</button>
        <button class="btn-cta-secondary">데모 체험하기</button>
      </div>
      <div class="cta-info">
        <div class="cta-info-item">
          <svg width="20" height="20"><!-- Check Icon --></svg>
          <span>신용카드 불필요</span>
        </div>
        <div class="cta-info-item">
          <svg width="20" height="20"><!-- Check Icon --></svg>
          <span>30분 내 응답</span>
        </div>
        <div class="cta-info-item">
          <svg width="20" height="20"><!-- Check Icon --></svg>
          <span>맞춤 제안서 제공</span>
        </div>
      </div>
    </div>
  </div>
</section>
```

### CSS 스펙
```css
/* CTA Section */
.cta {
  padding: 120px 0;
  background: linear-gradient(
    135deg,
    var(--primary-500) 0%,
    var(--primary-600) 50%,
    var(--primary-700) 100%
  );
  position: relative;
  overflow: hidden;
}

/* Background Pattern */
.cta::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle at 20% 50%, rgba(255,255,255,0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 50%, rgba(255,255,255,0.1) 0%, transparent 50%);
  pointer-events: none;
}

.cta-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
  position: relative;
  z-index: 1;
}

/* CTA Content */
.cta-content {
  max-width: 720px;
  margin: 0 auto;
  text-align: center;
}

.cta-title {
  font-size: 44px;
  font-weight: 700;
  line-height: 56px;
  letter-spacing: -0.5px;
  color: var(--white);
  margin-bottom: 24px;
}

.cta-subtitle {
  font-size: 18px;
  font-weight: 400;
  line-height: 28px;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 40px;
}

/* CTA Actions */
.cta-actions {
  display: flex;
  gap: 16px;
  justify-content: center;
  margin-bottom: 32px;
}

/* CTA Primary Button */
.btn-cta-primary {
  padding: 18px 36px;
  height: 60px;
  font-size: 17px;
  font-weight: 600;
  line-height: 24px;
  color: var(--primary-500);
  background: var(--white);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  transition: all var(--duration-normal) var(--ease);
  white-space: nowrap;
}

.btn-cta-primary:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.25);
  background: #F8F9FA;
}

/* CTA Secondary Button */
.btn-cta-secondary {
  padding: 18px 36px;
  height: 60px;
  font-size: 17px;
  font-weight: 600;
  line-height: 24px;
  color: var(--white);
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all var(--duration-normal) var(--ease);
  white-space: nowrap;
}

.btn-cta-secondary:hover {
  background: rgba(255, 255, 255, 0.25);
  border-color: rgba(255, 255, 255, 0.6);
  transform: translateY(-4px);
}

/* CTA Info */
.cta-info {
  display: flex;
  gap: 32px;
  justify-content: center;
  align-items: center;
}

.cta-info-item {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.9);
}

.cta-info-item svg {
  width: 20px;
  height: 20px;
  fill: rgba(255, 255, 255, 0.9);
}
```

---

## 9️⃣ FOOTER (높이: ~450px)

### 구조
- Padding: 80px 0 40px
- Background: var(--gray-900)
- 레이아웃: 4열 Grid + Copyright

### HTML 구조
```html
<footer class="footer">
  <div class="footer-container">
    <!-- Footer Main -->
    <div class="footer-main">
      <!-- Column 1: Logo & Info -->
      <div class="footer-column">
        <div class="footer-logo">
          <img src="/logo-white.svg" alt="Nova Partners" />
        </div>
        <p class="footer-description">
          신뢰할 수 있는 AI로<br>
          기업의 미래를 만듭니다.
        </p>
        <div class="footer-social">
          <a href="#" class="social-link" aria-label="LinkedIn">
            <svg width="24" height="24"><!-- LinkedIn --></svg>
          </a>
          <a href="#" class="social-link" aria-label="Twitter">
            <svg width="24" height="24"><!-- Twitter --></svg>
          </a>
          <a href="#" class="social-link" aria-label="YouTube">
            <svg width="24" height="24"><!-- YouTube --></svg>
          </a>
        </div>
      </div>
      
      <!-- Column 2: 솔루션 -->
      <div class="footer-column">
        <h3 class="footer-title">솔루션</h3>
        <ul class="footer-links">
          <li><a href="/solutions/ai-platform">AI 플랫폼</a></li>
          <li><a href="/solutions/finance">금융</a></li>
          <li><a href="/solutions/manufacturing">제조</a></li>
          <li><a href="/solutions/healthcare">의료</a></li>
          <li><a href="/solutions/retail">소매</a></li>
        </ul>
      </div>
      
      <!-- Column 3: 회사 -->
      <div class="footer-column">
        <h3 class="footer-title">회사</h3>
        <ul class="footer-links">
          <li><a href="/company/about">회사소개</a></li>
          <li><a href="/company/team">팀</a></li>
          <li><a href="/company/careers">채용</a></li>
          <li><a href="/company/news">뉴스</a></li>
          <li><a href="/company/contact">연락처</a></li>
        </ul>
      </div>
      
      <!-- Column 4: 고객지원 -->
      <div class="footer-column">
        <h3 class="footer-title">고객지원</h3>
        <ul class="footer-links">
          <li><a href="/support/docs">문서</a></li>
          <li><a href="/support/api">API</a></li>
          <li><a href="/support/faq">FAQ</a></li>
          <li><a href="/support/contact">문의하기</a></li>
        </ul>
        <div class="footer-contact">
          <div class="contact-item">
            <svg width="16" height="16"><!-- Phone --></svg>
            <span>02-1234-5678</span>
          </div>
          <div class="contact-item">
            <svg width="16" height="16"><!-- Email --></svg>
            <span>contact@novapartners.ai</span>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Footer Bottom -->
    <div class="footer-bottom">
      <div class="footer-copyright">
        © 2024 Nova Partners. All rights reserved.
      </div>
      <div class="footer-legal">
        <a href="/privacy">개인정보처리방침</a>
        <a href="/terms">이용약관</a>
        <a href="/security">보안정책</a>
      </div>
    </div>
  </div>
</footer>
```

### CSS 스펙
```css
/* Footer */
.footer {
  padding: 80px 0 40px;
  background: var(--gray-900);
  color: var(--white);
}

.footer-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 80px;
}

/* Footer Main */
.footer-main {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1.5fr;
  gap: 64px;
  padding-bottom: 64px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

/* Footer Column */
.footer-column {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

/* Footer Logo */
.footer-logo {
  width: 180px;
  margin-bottom: 8px;
}

.footer-logo img {
  width: 100%;
  height: auto;
}

/* Footer Description */
.footer-description {
  font-size: 14px;
  font-weight: 400;
  line-height: 22px;
  color: rgba(255, 255, 255, 0.7);
  margin: 0;
}

/* Social Links */
.footer-social {
  display: flex;
  gap: 12px;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: var(--radius-sm);
  background: rgba(255, 255, 255, 0.08);
  transition: all var(--duration-fast) var(--ease);
}

.social-link:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
}

.social-link svg {
  width: 24px;
  height: 24px;
  fill: rgba(255, 255, 255, 0.8);
}

/* Footer Title */
.footer-title {
  font-size: 16px;
  font-weight: 600;
  line-height: 24px;
  color: var(--white);
  margin: 0;
}

/* Footer Links */
.footer-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links a {
  font-size: 14px;
  font-weight: 400;
  line-height: 20px;
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  transition: all var(--duration-fast) ease;
}

.footer-links a:hover {
  color: var(--white);
  padding-left: 4px;
}

/* Footer Contact */
.footer-contact {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 8px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.7);
}

.contact-item svg {
  width: 16px;
  height: 16px;
  fill: rgba(255, 255, 255, 0.5);
}

/* Footer Bottom */
.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 32px;
}

.footer-copyright {
  font-size: 14px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.5);
}

/* Footer Legal */
.footer-legal {
  display: flex;
  gap: 24px;
}

.footer-legal a {
  font-size: 14px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.5);
  text-decoration: none;
  transition: color var(--duration-fast) ease;
}

.footer-legal a:hover {
  color: rgba(255, 255, 255, 0.8);
}
```

---

## 🔟 반응형 Breakpoints

### Tablet (768px ~ 1199px)
```css
@media (max-width: 1199px) {
  /* Container */
  .container,
  .hero-container,
  .features-container,
  .solutions-container,
  .trust-container,
  .portfolio-container,
  .testimonials-container,
  .cta-container,
  .footer-container {
    padding: 0 48px;
  }
  
  /* Header */
  .header-container {
    padding: 0 48px;
  }
  
  .nav-menu {
    gap: 24px;
  }
  
  .nav-link {
    font-size: 15px;
  }
  
  /* Hero */
  .hero-container {
    gap: 48px;
  }
  
  .hero-left {
    flex: 0 0 460px;
  }
  
  .hero-title {
    font-size: 40px;
    line-height: 48px;
  }
  
  /* Features Grid */
  .features-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
  }
  
  .feature-card {
    padding: 32px;
  }
  
  /* Solutions */
  .solutions-container {
    gap: 64px;
  }
  
  .solutions-left {
    flex: 0 0 400px;
  }
  
  /* Trust Logos */
  .trust-logos {
    gap: 32px 24px;
  }
  
  /* Portfolio Grid */
  .portfolio-grid {
    gap: 24px;
  }
  
  /* Testimonials Grid */
  .testimonials-grid {
    gap: 24px;
  }
  
  /* Footer */
  .footer-main {
    gap: 48px;
  }
}

@media (max-width: 991px) {
  /* Solutions: Stack to Single Column */
  .solutions-container {
    flex-direction: column;
    gap: 48px;
  }
  
  .solutions-left {
    flex: 1;
    max-width: 100%;
  }
  
  .solutions-right {
    max-width: 100%;
  }
  
  /* Footer: 2x2 Grid */
  .footer-main {
    grid-template-columns: repeat(2, 1fr);
    gap: 40px;
  }
}
```

### Mobile (< 768px)
```css
@media (max-width: 767px) {
  /* Container */
  .container,
  .hero-container,
  .features-container,
  .solutions-container,
  .trust-container,
  .portfolio-container,
  .testimonials-container,
  .cta-container,
  .footer-container {
    padding: 0 24px;
  }
  
  /* Header */
  .header {
    height: 64px;
  }
  
  .header-container {
    padding: 0 24px;
  }
  
  .logo {
    width: 140px;
    height: 48px;
  }
  
  /* Hide Desktop Nav */
  .header-nav {
    display: none;
  }
  
  /* Mobile Menu Button */
  .btn-mobile-menu {
    display: flex;
  }
  
  /* Hero */
  .hero {
    padding: 80px 0 60px;
    min-height: auto;
  }
  
  .hero-container {
    flex-direction: column;
    gap: 40px;
  }
  
  .hero-left,
  .hero-right {
    flex: 1;
    max-width: 100%;
  }
  
  .hero-title {
    font-size: 32px;
    line-height: 40px;
  }
  
  .hero-subtitle {
    font-size: 16px;
    line-height: 24px;
  }
  
  .hero-actions {
    flex-direction: column;
    gap: 12px;
  }
  
  .btn-hero-primary,
  .btn-hero-secondary {
    width: 100%;
  }
  
  .hero-visual {
    height: 300px;
  }
  
  /* Features */
  .features {
    padding: 80px 0;
  }
  
  .features-header {
    margin-bottom: 48px;
  }
  
  .section-title {
    font-size: 28px;
    line-height: 36px;
  }
  
  .section-subtitle {
    font-size: 16px;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
  
  /* Solutions */
  .solutions {
    padding: 80px 0;
  }
  
  .solutions-stats {
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
  
  .stat-number {
    font-size: 28px;
    line-height: 36px;
  }
  
  .solutions-tabs {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 8px;
  }
  
  .tab-visual {
    height: 240px;
  }
  
  /* Trust Signal */
  .trust-signal {
    padding: 60px 0;
  }
  
  .trust-title {
    font-size: 24px;
    line-height: 32px;
  }
  
  .trust-logos {
    grid-template-columns: repeat(2, 1fr);
    gap: 32px 24px;
  }
  
  /* Portfolio */
  .portfolio {
    padding: 80px 0;
  }
  
  .portfolio-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
  
  .portfolio-image {
    height: 220px;
  }
  
  .portfolio-content {
    padding: 24px;
  }
  
  .portfolio-metrics {
    gap: 16px;
  }
  
  /* Testimonials */
  .testimonials {
    padding: 80px 0;
  }
  
  .testimonials-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
  
  .testimonial-card {
    padding: 32px 24px;
  }
  
  /* CTA */
  .cta {
    padding: 80px 0;
  }
  
  .cta-title {
    font-size: 32px;
    line-height: 40px;
  }
  
  .cta-subtitle {
    font-size: 16px;
    line-height: 24px;
  }
  
  .cta-actions {
    flex-direction: column;
    gap: 12px;
  }
  
  .btn-cta-primary,
  .btn-cta-secondary {
    width: 100%;
  }
  
  .cta-info {
    flex-direction: column;
    gap: 12px;
  }
  
  /* Footer */
  .footer {
    padding: 60px 0 32px;
  }
  
  .footer-main {
    grid-template-columns: 1fr;
    gap: 40px;
    padding-bottom: 40px;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }
  
  .footer-legal {
    flex-direction: column;
    gap: 12px;
  }
}

/* Touch Targets (Mobile) */
@media (max-width: 767px) {
  /* Minimum 48px touch target */
  .btn-search,
  .btn-contact,
  .btn-support,
  .nav-link,
  .feature-link,
  .portfolio-link,
  .footer-links a {
    min-height: 48px;
    display: flex;
    align-items: center;
  }
}
```

---

## 1️⃣1️⃣ JavaScript Interactions

### Core Interactions
```javascript
// ======================
// 1. Header Scroll Effect
// ======================
const header = document.querySelector('.header');
let lastScroll = 0;

window.addEventListener('scroll', () => {
  const currentScroll = window.pageYOffset;
  
  // Add scrolled class
  if (currentScroll > 50) {
    header.classList.add('scrolled');
  } else {
    header.classList.remove('scrolled');
  }
  
  lastScroll = currentScroll;
});

// ======================
// 2. Scroll-triggered Animations
// ======================
const observerOptions = {
  threshold: 0.1,
  rootMargin: '0px 0px -50px 0px'
};

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('is-visible');
    }
  });
}, observerOptions);

// Observe all animatable elements
const animatableElements = document.querySelectorAll(
  '.feature-card, .portfolio-card, .testimonial-card, .logo-item'
);

animatableElements.forEach(el => observer.observe(el));

// ======================
// 3. Solutions Tabs
// ======================
const tabButtons = document.querySelectorAll('.tab-button');
const tabContents = document.querySelectorAll('.tab-content');

tabButtons.forEach(button => {
  button.addEventListener('click', () => {
    const targetTab = button.dataset.tab;
    
    // Remove active from all
    tabButtons.forEach(btn => btn.classList.remove('active'));
    tabContents.forEach(content => content.classList.remove('active'));
    
    // Add active to clicked
    button.classList.add('active');
    document.querySelector(`[data-content="${targetTab}"]`).classList.add('active');
  });
});

// ======================
// 4. Smooth Scroll for Anchor Links
// ======================
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    
    if (target) {
      const offsetTop = target.offsetTop - 80; // Header height
      window.scrollTo({
        top: offsetTop,
        behavior: 'smooth'
      });
    }
  });
});

// ======================
// 5. Button Ripple Effect
// ======================
document.querySelectorAll('.btn-hero-primary').forEach(button => {
  button.addEventListener('click', function(e) {
    const rect = this.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    
    const ripple = document.createElement('span');
    ripple.className = 'ripple';
    ripple.style.left = x + 'px';
    ripple.style.top = y + 'px';
    
    this.appendChild(ripple);
    
    setTimeout(() => ripple.remove(), 600);
  });
});

// ======================
// 6. Mobile Menu Toggle
// ======================
const mobileMenuBtn = document.querySelector('.btn-mobile-menu');
const mobileMenu = document.querySelector('.mobile-menu');

if (mobileMenuBtn && mobileMenu) {
  mobileMenuBtn.addEventListener('click', () => {
    mobileMenu.classList.toggle('active');
    document.body.classList.toggle('menu-open');
  });
}

// ======================
// 7. Search Modal (Optional)
// ======================
const searchBtn = document.querySelector('.btn-search');
const searchModal = document.querySelector('.search-modal');
const searchClose = document.querySelector('.search-close');

if (searchBtn && searchModal) {
  searchBtn.addEventListener('click', () => {
    searchModal.classList.add('active');
    document.querySelector('.search-input').focus();
  });
  
  searchClose.addEventListener('click', () => {
    searchModal.classList.remove('active');
  });
  
  // ESC key to close
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape' && searchModal.classList.contains('active')) {
      searchModal.classList.remove('active');
    }
  });
}

// ======================
// 8. Lazy Load Images
// ======================
if ('loading' in HTMLImageElement.prototype) {
  // Browser supports lazy loading natively
  const images = document.querySelectorAll('img[loading="lazy"]');
  images.forEach(img => {
    img.src = img.dataset.src;
  });
} else {
  // Fallback for older browsers
  const lazyImageObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const img = entry.target;
        img.src = img.dataset.src;
        lazyImageObserver.unobserve(img);
      }
    });
  });
  
  const images = document.querySelectorAll('img[data-src]');
  images.forEach(img => lazyImageObserver.observe(img));
}

// ======================
// 9. Performance: Debounce Scroll
// ======================
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

// Apply debounce to scroll events
const handleScroll = debounce(() => {
  // Your scroll logic here
}, 10);

window.addEventListener('scroll', handleScroll);
```

---

## 1️⃣2️⃣ 추가 CSS Utilities

### Animation Utilities
```css
/* Fade In Animations */
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

/* Scale Animations */
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

/* Rotation */
@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* Pulse */
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

/* Bounce */
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
```

### Focus Styles (Accessibility)
```css
/* Focus Visible for Keyboard Navigation */
*:focus-visible {
  outline: 2px solid var(--primary-500);
  outline-offset: 2px;
  border-radius: 4px;
}

/* Remove outline for mouse users */
*:focus:not(:focus-visible) {
  outline: none;
}

/* Skip to Content Link */
.skip-to-content {
  position: absolute;
  top: -100px;
  left: 0;
  padding: 16px;
  background: var(--primary-500);
  color: var(--white);
  text-decoration: none;
  z-index: 10000;
  transition: top 0.3s ease;
}

.skip-to-content:focus {
  top: 0;
}
```

### Loading States
```css
/* Skeleton Loader */
.skeleton {
  background: linear-gradient(
    90deg,
    var(--gray-100) 0%,
    var(--gray-50) 50%,
    var(--gray-100) 100%
  );
  background-size: 200% 100%;
  animation: skeleton-loading 1.5s ease-in-out infinite;
  border-radius: var(--radius-sm);
}

@keyframes skeleton-loading {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

/* Spinner */
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid var(--gray-100);
  border-top-color: var(--primary-500);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

---

## 📋 최종 체크리스트

### ✅ 완료 항목
- [x] 전역 CSS Variables 정의
- [x] Container System 구축
- [x] Header (Fixed, Dropdown)
- [x] Hero Section (Video BG, Gradient Text)
- [x] Features Grid (3열, Hover Effects)
- [x] Solutions Tabs (Interactive)
- [x] Trust Signal (Logo Grid)
- [x] Portfolio Cards (2x2 Grid)
- [x] Testimonials (3열, Ratings)
- [x] CTA (Gradient Background)
- [x] Footer (4열, Social Links)
- [x] 반응형 (Desktop, Tablet, Mobile)
- [x] JavaScript Interactions
- [x] Scroll Animations
- [x] Accessibility (Focus States)
- [x] Performance (Lazy Load, Debounce)

### 🎯 2026 트렌드 반영
- [x] Glow Effects (hero-visual)
- [x] Glassmorphism (Header blur, CTA buttons)
- [x] Organic Shapes (blob animation)
- [x] Bold Typography (48px+)
- [x] Micro Interactions (Ripple, Hover)
- [x] Smooth Scroll Triggers
- [x] Video Background
- [x] Gradient Text
- [x] Card Hover 3D Effects

### 📱 접근성 & 성능
- [x] 48px 최소 터치 타겟
- [x] Focus-visible Styles
- [x] Skip to Content Link
- [x] Lazy Loading Images
- [x] Debounced Scroll Events
- [x] Semantic HTML
- [x] ARIA Labels

---

## 🚀 다음 단계

1. **클로드 코드**에 3개 파일 제공:
   - Part 1 (전역 설정 + Header + Hero)
   - Part 2 (Features ~ Portfolio)
   - Part 3 (Testimonials ~ Footer + 반응형 + JS)

2. **즉시 코딩 가능**: 모든 픽셀, 색상, 애니메이션 스펙 완료

3. **추가 작업** (선택):
   - 실제 이미지/비디오 에셋 삽입
   - SVG 아이콘 세트 완성
   - 백엔드 API 연동 (문의 폼 등)

---

**🎉 HOME 페이지 픽셀 퍼펙트 스펙 완성!**  
**총 3개 파일로 2026년 수준 엔터프라이즈 사이트 구현 준비 완료.**
