# NovaPartners Hyper-Fluid Design Specification 2026

## Part 5/?? — Appendix + Full Motion Timeline Specification + Extended Notes

(본 문서는 Part 1~4에 이어지는 **Part 5**이며, 800줄 제한을 준수한 확장 문서입니다.)

---
# 16. APPENDIX A — GLOBAL MOTION TIMELINE

본 섹션은 NovaPartners 2026 Hyper-fluid System의 **전체 모션 시퀀스를 시간 기반으로 정리한 마스터 타임라인**이다.

모든 페이지에서 공통으로 사용되는 Global Motion Flow는 아래 5단계 구조를 가진다.

## 16.1 GLOBAL 5-STAGE FLOW
1. **Initialize** — 공간 활성화, 첫 레이어 등장
2. **Reveal** — 핵심 정보/타이포 등장
3. **Engage** — 카드/탭/인터랙션 활성화
4. **Process** — Scan/Validation/Highlight 단계
5. **Transition** — Wave 기반 Scene 이동

---
## 16.2 MASTER TIMELINE (0s ~ 3.5s)

### **0.00s – 0.20s** — Spatial Initialization
- Deep carbon background → Blue grid
- Refraction baseline 세팅

### **0.20s – 0.60s** — Plasma Beam Entry
- 첫 Beam 등장
- Hero 타이포 윤곽 드러남

### **0.40s – 1.00s** — Typography Reveal
- Density shift
- CTA 등장

### **0.80s – 1.40s** — Background Assembly
- Hero 구조물 재배열
- Pulse 시작

### **1.40s – 2.40s** — Interaction Activation
- Cards stagger-in
- Tabs depth-swap 가능 상태 진입

### **2.40s – 3.50s** — Continuous System
- Scroll-based transitions 가능
- Wave 준비 상태

---
# 17. APPENDIX B — FULL MOTION MAP (PAGE-LEVEL)

모든 페이지는 아래 Motion Map 포맷을 따라 정의된다.

## 17.1 MOTION MAP FORMAT
- **E(entry)** — 첫 등장 방식
- **A(active)** — 사용자 조작/스크롤 시 반응
- **X(exit)** — 다음 Scene으로 전환 시 모션
- **Z(z-depth)** — 공간적 위치
- **P(plasma)** — Beam / Pulse / Scan / Wave 적용 패턴

이 규칙은 Part 1~4의 모든 페이지에 이미 적용됨.

---
# 18. APPENDIX C — EXTENDED SYSTEM NOTES

## 18.1 EASING PRINCIPLES
- **FluidIn**: 시작은 빠르게 → 밀도 있는 정지
- **FluidOut**: 긴 이동 → 부드러운 멈춤
- **Magnetic**: 제조/조립 기반 연출에 핵심
- **Impulse**: CTA, 버튼의 반응 중심

## 18.2 COLOR MOTION RULES
- Plasma Blue는 모든 Beam과 Scan의 공통 기준색
- 산업별 Scene에서는 미묘한 Palette Shift만 허용
- 의료의 Purification White-Cyan은 특정 구간에서만 활성화

## 18.3 Z-DEPTH RULES
- Z 60~100: Hero/Scene 상단 레이어
- Z 20~40: 콘텐츠 카드/다이어그램
- Z 0~15: 백그라운드/Glass panel

## 18.4 LAYER TRANSITION
- Hero → Content: Wave 또는 Layer-fold 사용
- Tabs: Z-Swap motion
- Cards: Lift + Refraction

## 18.5 PERFORMANCE GUIDELINES
- 60fps target
- Refraction 효과는 GPU 우선 적용
- Scroll Trigger는 debounced 16–32ms interval

---
# 19. APPENDIX D — COMPONENT MOTION BLUEPRINT

## 19.1 BUTTONS
- Hover: brightness up
- Press: impulse snap
- Focus: plasma ring

## 19.2 INPUTS
- Focus: outer glow
- Validate: scan

## 19.3 CARDS
- Hover: lift + distortion
- Entry: stagger 50–120ms

## 19.4 TABS
- Beam underline
- Depth swap panel

## 19.5 LISTS
- Staggered drop

---
# 20. APPENDIX E — SPATIAL IDENTITY MODEL

NovaPartners의 시그니처 공간 표현 구조.

## 20.1 SPATIAL FRAMEWORK
- **Horizontal motion:** 금융·소매 중심
- **Vertical motion:** Hero typography, 제조 분해 조립
- **Depth motion:** Tabs, Hero → Content transition 핵심

## 20.2 REFRACTION LEVELS
- Hero: High
- Cards: Medium
- Utility: Low

## 20.3 GLASS LAYERED ENVIRONMENT
- Front Glass: 인터랙션 기반
- Mid Glass: 정보형 구조물
- Back Glass: ambience로 존재

---
# 21. APPENDIX F — ADVANCED INTERACTION RULES

## 21.1 SCROLL SPEED ADAPTATION
- velocity.slow → fade 기반
- velocity.medium → standard parallax
- velocity.fast → beam 확률 증가

## 21.2 USER INTENT PREDICTION (UI REACTION)
- 빠르게 하단으로 스크롤 시 Hero를 조기 축소
- 스크롤 멈추면 Pulse 강도 미세 증가

## 21.3 ACCESSIBILITY MOTION REDUCTION
- Reduced Motion 모드:
  - Beam intensity 0.85 → 0.30
  - Pulse amplitude 0.6 → 0.2
  - Wave 40% 축소

---
# 22. APPENDIX G — MOTION DEBUGGING GUIDE

## 22.1 THREE COMMON ISSUES
1. **Z-layer conflict** — 해결: Z-token 강제 적용
2. **Scan jitter** — 해결: FPS lock + GPU priority
3. **Refraction lag** — 해결: resolution adaptive scaling

## 22.2 PERFORMANCE CHECKPOINTS
- 스크롤 중 50ms 넘는 이벤트 없음
- CPU 점유율 30% 이하 유지
- GPU fallback 대비 blur~refraction 단계적 적용

---
# END OF PART 5

원하실 경우, Part 6(최종 Master Combined Version + Download Assembly)을 제작할 수 있습니다.
