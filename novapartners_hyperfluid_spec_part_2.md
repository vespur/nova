# NovaPartners Hyper-Fluid Design Specification 2026

## Part 2/?? — Motion Token System & Plasma Identity

(본 문서는 Part 1에 이어지는 **Part 2**이며, 분량 800줄 제한을 준수하여 분리된 문서입니다.)

---
# 5. MOTION TOKEN SYSTEM (2026 Hyper-fluid)

NovaPartners의 전체 페이지(23개)와 모든 UI/UX 행동을 관통하는 **근본적 모션 규칙 세트**.

아래 Motion Token들은 실제 개발, 모션 디자인, 프로토타입 제작 시 그대로 구현해도 되는 수준의 표준화된 값이다.

---
## 5.1 Global Easing Tokens
모든 움직임의 근본 리듬.

- **fluidIn:** 빠르게 시작해 점성 있게 멈춤
- **fluidOut:** 높은 관성 → 매끄러운 정지
- **snap:** 강한 임팩트가 필요한 순간
- **soft:** 의료 등 부드러운 장면용
- **magnetic:** 제조 조립/스냅 모션용
- **impulse:** CTA, 버튼 press 등

```
{
  "easing": {
    "fluidIn": "cubic-bezier(0.16, 0.0, 0.50, 0.0)",
    "fluidOut": "cubic-bezier(0.30, 1.20, 0.60, 1.0)",
    "snap": "cubic-bezier(0.20, 0.80, 0.40, 1.40)",
    "soft": "cubic-bezier(0.25, 0.10, 0.25, 1.0)",
    "magnetic": "cubic-bezier(0.10, 1.20, 0.20, 1.0)",
    "impulse": "cubic-bezier(0.50, 0.00, 0.10, 1.5)"
  }
}
```

---
## 5.2 Duration Tokens
2026 모션의 핵심: **짧은 인터랙션 + 긴 시퀀스**의 조화.

```
{
  "duration": {
    "xxs": 60,
    "xs": 120,
    "sm": 180,
    "md": 300,
    "lg": 480,
    "xl": 700,
    "xxl": 1100
  }
}
```

- Hero 전환: 700–1100ms
- 탭/내비: 200–300ms
- 카드 hover: 60–120ms

---
## 5.3 Z-Depth Tokens
NovaPartners의 공간감 구조.

```
{
  "z": {
    "bg": 0,
    "surface": 5,
    "card": 20,
    "panel": 30,
    "modalBase": 40,
    "stats": 45,
    "hero": 60,
    "heroForeground": 80,
    "overlay": 100,
    "critical": 200
  }
}
```

Z-depth는 페이지 구조 전체에 적용되는 통일 시스템이며, Hero가 항상 최상위 서사 레이어를 유지한다.

---
## 5.4 Scroll Trigger Tokens

```
{
  "scroll": {
    "threshold": {
      "enter": 0.15,
      "active": 0.45,
      "exit": 0.85
    },
    "parallax": {
      "slow": 0.2,
      "medium": 0.4,
      "fast": 0.6
    },
    "densityShift": {
      "low": 0.04,
      "mid": 0.08,
      "high": 0.12
    }
  }
}
```

스크롤은 NovaPartners의 **내러티브 기반 전환**의 중심.

---
## 5.5 Interaction Tokens (Hover, Press, Focus)

```
{
  "interaction": {
    "hover": {
      "scale": 1.02,
      "lift": 3,
      "brightness": 1.08,
      "glassDistortion": 0.2
    },
    "press": {
      "scale": 0.96,
      "duration": 80,
      "easing": "impulse"
    },
    "focus": {
      "ring": "plasmaThin",
      "intensity": 0.3
    }
  }
}
```

- Feature Card Hover = scale + lift + glassDistortion(0.2)
- CTA Press = impulse easing + 빠른 반응

---
## 5.6 Plasma / Light / Glass Tokens
NovaPartners의 브랜드 모션 정체성의 핵심.

```
{
  "plasma": {
    "beam": {
      "thickness": 1.2,
      "speed": 0.8,
      "intensity": 0.85,
      "color": "rgba(0, 122, 255, 0.85)"
    },
    "scan": {
      "direction": "leftToRight",
      "duration": 700
    },
    "pulse": {
      "amplitude": 0.6,
      "frequency": 1.2
    }
  },
  "glass": {
    "blur": {
      "light": 8,
      "medium": 16,
      "heavy": 24
    },
    "refraction": {
      "low": 0.08,
      "mid": 0.15,
      "high": 0.28
    }
  }
}
```

---
## 5.7 Z-Swap Tokens (탭 장면 전환 핵심)

```
{
  "zSwap": {
    "distance": 40,
    "duration": 320,
    "easing": "fluidOut",
    "fade": true,
    "shadowBoost": 12
  }
}
```

---
## 5.8 Magnetic Motion Tokens (조립/스냅)

```
{
  "magnetic": {
    "strength": 0.6,
    "snapDistance": 24,
    "returnSpeed": 0.45
  }
}
```

---
## 5.9 Density Tokens (Typography Density Shift)

```
{
  "density": {
    "low": 0.85,
    "normal": 1.0,
    "high": 1.15
  }
}
```

---
## 5.10 Velocity Tokens

```
{
  "velocity": {
    "slow": 0.3,
    "medium": 0.7,
    "fast": 1.2
  }
}
```

---
# 6. PLASMA IDENTITY MOTION PROTOTYPE

NovaPartners의 모든 모션은 아래 4대 Plasma Motion Code로부터 파생된다.

1. **Plasma Beam** — 강조, 이동, 결정
2. **Plasma Pulse** — 생명력, 유지, 감정
3. **Plasma Scan** — 검증, 완료, 처리
4. **Plasma Wave** — 장면 전환, 흐름, 서사 연결

---
## 6.1 Plasma Beam — 브랜드의 직선적 에너지
- Hero 최초 진입
- Tabs 선택 시 강조
- CTA Hover 액션
- AI 플랫폼의 신호 전환

특징:
- 얇고 밝음
- 빠른 방향성
- 유리 굴절 잔상

---
## 6.2 Plasma Pulse — 브랜드의 생명 신호
- Hero에서 지속적 유지
- Metrics 뒤에서 약하게 동작
- Testimonials, Cards 배경에서 미세하게 존재

---
## 6.3 Plasma Scan — 검증 및 완료의 시각화
- Stats 증가 애니메이션
- Form validation
- Pricing 플랜 선택 시

---
## 6.4 Plasma Wave — 장면 간 유체형 전환
- Hero → Feature/Tabs 전환
- 산업별 Scene 전환
- Home → Solutions 이동

곡선형/직선형 모두 상황에 따라 변형.

---
# 7. HOME HERO MOTION SCENARIO (Full Scene)

본 섹션에서는 Home Hero의 **시간 기반 시퀀스**를 정의한다.

## 7.1 Intro (0.00s ~ 0.20s)
- 배경: Deep Carbon → Blue Grid 노출
- 텍스트/CTA 없음

## 7.2 Plasma Beam Entry (0.20s ~ 0.60s)
- 대각선 Beam + 굴절 잔상
- Beam 궤적 위에 헤드라인 윤곽 등장

## 7.3 Typography Unfold (0.40s ~ 1.00s)
- 밀도 증가(density 0.85→1.1)
- Y축 12px → 0
- CTA는 Beam 스침과 함께 등장

## 7.4 Background Assembly (0.80s ~ 1.40s)
- Hero 구조물 Z60→80 상승 후 정렬
- Pulse 시작

## 7.5 Idle State (1.40s 이후)
- 지속적 Pulse
- 마우스 refraction 반응

---
# 8. SOLUTIONS TABS — DEPTH SWAP PANEL SCENARIO

## 8.1 탭 클릭 시퀀스
1. Press scale-down 0.96
2. Plasma Beam Indicator Sweep
3. Old panel fade-out + Z20→10
4. New panel Z0→30 + opacity 0→1
5. 내부 콘텐츠 stagger-in

---
# 9. END OF PART 2

다음 파트(**Part 3**)에서는 아래 내용을 포함한다:
- 산업별 시그니처 모션 패턴(금융/제조/의료/소매)
- 산업별 Hero/Content/Transition 구조
- 각 산업 페이지의 전체 모션 흐름 구조

필요 시 “Part 3 만들어줘”라고 요청하면 바로 생성한다.
