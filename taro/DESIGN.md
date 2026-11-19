# TARO Design System

> Midnight Tarot — 별빛이 머무는 밤, 나를 비추는 한 장의 카드

이 문서는 타로카드 서비스의 화면·컴포넌트·스타일 구현을 위한 단일 디자인 기준이다. 구현 시 이 문서의 토큰과 컴포넌트 규칙을 우선 적용한다.

- **제품:** 오늘의 타로 — 설치·회원가입 없이 1분 안에 한 장의 타로와 개인화된 짧은 해석을 확인하고 저장·공유하는 모바일 웹서비스
- **테마:** Dark-first
- **디자인 키워드:** 신비로움, 차분함, 몰입, 따뜻한 안내, 신뢰
- **기준 화면:** 모바일 393 × 852px
- **기술 스타일 기준:** Tailwind CSS v4 유틸리티·CSS 변수 방식, shadcn/ui의 의미 기반 토큰 및 접근성 패턴을 참고한다.

---

## 1. Brand & Visual Direction

### 1.1 디자인 컨셉

**Midnight Tarot**는 깊은 밤하늘 위에 떠 있는 한 장의 타로 카드를 마주하는 경험이다. 어두운 배경은 집중과 몰입을 만들고, 보랏빛 오로라와 은은한 샴페인 골드는 신비로움과 따뜻함을 더한다. 카드와 결과는 무대 중앙에 놓인 오브제처럼 표현한다.

AuthKit 레퍼런스의 어두운 캔버스, 반투명 유리 표면, 낮은 대비의 헤어라인, 은은한 광원을 계승하되 타로의 상징인 별·달·아치·카드 프레임을 고유한 시각 언어로 사용한다.

### 1.2 경험 원칙

1. **카드가 주인공:** 시작 화면과 결과 화면에서 타로 카드가 가장 먼저 눈에 들어와야 한다.
2. **짧고 쉬운 흐름:** 한 화면에서 한 가지 핵심 행동을 유도한다. 가입·로그인은 만들지 않는다.
3. **신비롭지만 읽기 쉬움:** 장식은 배경에 머물고 입력, 해석, 버튼은 충분한 대비를 유지한다.
4. **안심할 수 있는 개인정보 안내:** 입력 화면과 결과 화면에 정보 미저장 안내를 반복해서 제공한다.
5. **오락 콘텐츠의 경계:** 예언이나 전문 조언처럼 보이지 않도록 오락용 안내를 결과·이미지·공유 문구에 표시한다.
6. **모바일 우선:** 한 손 조작, 세로 스크롤, 터치 영역을 우선 설계한다.

### 1.3 Do / Don't

**Do**
- 넓고 깊은 네이비 배경에 보랏빛·푸른빛 광원을 아주 약하게 사용한다.
- 타로 카드에는 독립적인 프레임, 얇은 장식선, 별자리·아르카나 표기를 적용한다.
- 유리 표면은 패널과 보조 카드에만 사용하고 본문 가독성을 우선한다.
- 주요 행동 버튼은 한 화면에 하나의 시각적 우선순위로 둔다.
- 상태는 색상뿐 아니라 텍스트·아이콘·테두리로 함께 전달한다.

**Don't**
- 형광 보라, 무지개 그라데이션, 강한 네온을 여러 곳에 동시에 쓰지 않는다.
- 카드 본문이나 해석 텍스트 뒤에 복잡한 패턴을 깔지 않는다.
- 모든 컨테이너를 유리 카드로 만들지 않는다. 평면 배경과 여백을 함께 사용한다.
- 건강·재물 관련 결과를 확정적 예언이나 행동 지시로 표현하지 않는다.
- 생년월일, 전공 원문, 기타 개인정보를 저장 이미지나 공유 메시지에 넣지 않는다.

---

## 2. Color Tokens

색상은 컴포넌트에서 직접 임의 지정하지 않고 역할 토큰을 사용한다. 기본은 다크 테마이며, 기능 상태 색상은 브랜드 장식색보다 명확해야 한다.

### 2.1 Brand palette

| Name | Hex | CSS token | Role |
|---|---|---|---|
| Midnight Ink | `#080A18` | `--taro-midnight` | 앱 전체 배경 |
| Deep Night | `#101329` | `--taro-night` | 주요 섹션·하단 배경 |
| Twilight Panel | `#171B35` | `--taro-panel` | 카드·패널 표면 |
| Raised Panel | `#202544` | `--taro-panel-raised` | 입력·선택·보조 표면 |
| Mystic Violet | `#8B72E8` | `--taro-violet` | 주요 브랜드 액션·선택 강조 |
| Violet Glow | `#B7A8FF` | `--taro-violet-soft` | 포커스·광원·보조 강조 |
| Moon Lavender | `#D8D0FF` | `--taro-lavender` | 주요 장식·카드 하이라이트 |
| Starlight | `#F4F0FF` | `--taro-starlight` | 주요 텍스트 |
| Moon Mist | `#C4C5D8` | `--taro-moon-mist` | 본문·보조 텍스트 |
| Dust Gray | `#9296B0` | `--taro-muted` | 설명·플레이스홀더 |
| Champagne Gold | `#D8B978` | `--taro-gold` | 카드 테두리·아르카나 장식에 제한 사용 |
| Soft Gold | `#F0DCA8` | `--taro-gold-soft` | 금색 텍스트·미세한 빛 |
| Glass Edge | `rgba(210, 216, 255, 0.14)` | `--taro-border` | 유리 표면의 얇은 경계 |
| Glass Fill | `rgba(185, 190, 255, 0.07)` | `--taro-glass` | 반투명 패널 |
| Focus Ring | `#B7A8FF` | `--taro-focus` | 키보드 포커스 |

### 2.2 Semantic tokens (shadcn/ui mapping)

| Semantic token | Dark value | Usage |
|---|---|---|
| `--background` | `#080A18` | 페이지 배경 |
| `--foreground` | `#F4F0FF` | 기본 텍스트 |
| `--card` | `#171B35` | 카드 표면 |
| `--card-foreground` | `#F4F0FF` | 카드 텍스트 |
| `--popover` | `#171B35` | 팝오버·메뉴 |
| `--popover-foreground` | `#F4F0FF` | 팝오버 텍스트 |
| `--primary` | `#8B72E8` | 주요 버튼·선택 상태 |
| `--primary-foreground` | `#FFFFFF` | 주요 버튼 텍스트 |
| `--secondary` | `#202544` | 보조 버튼·칩 배경 |
| `--secondary-foreground` | `#E7E3FF` | 보조 버튼 텍스트 |
| `--muted` | `#202544` | 비활성·약한 배경 |
| `--muted-foreground` | `#9296B0` | 보조 텍스트 |
| `--accent` | `#2B2850` | hover·선택 보조 표면 |
| `--accent-foreground` | `#F4F0FF` | 강조 표면 텍스트 |
| `--destructive` | `#D96B7A` | 삭제·오류 |
| `--destructive-foreground` | `#FFFFFF` | 오류 표면 텍스트 |
| `--border` | `rgba(210,216,255,0.14)` | 기본 경계 |
| `--input` | `rgba(210,216,255,0.18)` | 입력 경계 |
| `--ring` | `#B7A8FF` | 포커스 링 |

상태 색상은 의미를 우선한다. 성공은 차분한 세이지 그린(`#83B9A0`), 경고는 앰버(`#D8B978`), 오류는 로즈(`#D96B7A`)를 사용한다. 이 색상은 상태 메시지에만 사용하고 브랜드 장식색으로 확장하지 않는다.

### 2.3 Gradient system

- **Night Aura:** `radial-gradient(ellipse at 50% 0%, rgba(139,114,232,.20), transparent 62%)` — 시작 화면 상단의 약한 광원.
- **Card Foil:** `linear-gradient(145deg, rgba(240,220,168,.24), rgba(183,168,255,.10) 45%, rgba(139,114,232,.18))` — 카드 프레임의 미세한 반사.
- **Moonlight Text:** `linear-gradient(180deg, #F4F0FF 0%, #C4B9F7 100%)` — 큰 제목이나 서비스 워드마크에만 사용.
- **Glass Wash:** `linear-gradient(145deg, rgba(210,216,255,.09), rgba(139,114,232,.035))` — 패널 표면.

그라데이션은 제목·카드 프레임·배경 광원에 제한한다. 일반 본문, 입력값, 버튼 라벨에는 단색을 사용한다.

---

## 3. Typography

### 3.1 Font family

- **UI / Body:** Pretendard 우선, 대체 `Inter, ui-sans-serif, system-ui, sans-serif`.
- **Display / Tarot title:** `Cormorant Garamond` 또는 `Noto Serif KR`를 카드명·아르카나 영문명 등 짧은 디스플레이 텍스트에 제한적으로 사용한다.
- **Numerals:** UI 폰트의 tabular numerals를 사용해 날짜·숫자 폭을 안정적으로 유지한다.

한글 본문과 입력 UI는 산세리프를 사용한다. 세리프는 카드 이름과 장식적인 제목에만 사용해 읽기 흐름을 해치지 않는다.

### 3.2 Type scale

| Role | Size | Weight | Line height | Usage |
|---|---:|---:|---:|---|
| Display | 36px / 2.25rem | 600 | 1.15 | 시작 화면 서비스 타이틀 |
| H1 | 30px / 1.875rem | 600 | 1.25 | 화면 제목 |
| H2 | 24px / 1.5rem | 600 | 1.3 | 결과 카드 제목·섹션 제목 |
| H3 | 20px / 1.25rem | 600 | 1.35 | 패널·카드 제목 |
| Body Large | 18px / 1.125rem | 400 | 1.55 | 핵심 안내·해석 |
| Body | 16px / 1rem | 400 | 1.5 | 기본 본문·입력값 |
| Body Small | 14px / .875rem | 400 | 1.45 | 설명·버튼 |
| Caption | 12px / .75rem | 400 | 1.4 | 개인정보·오락용 안내 |
| Eyebrow | 11px / .6875rem | 600 | 1.4 | 영문 섹션 라벨·카테고리 |

### 3.3 Typography rules

- 화면 제목은 한 화면에서 하나만 H1로 사용한다.
- 카드 이름은 세리프 24–30px, 한글은 산세리프 22–26px까지 허용한다.
- 해석 3줄은 15–16px, line-height 1.6으로 편안하게 읽히게 한다.
- 본문은 최소 14px, 개인정보·오락용 안내는 12px보다 작게 쓰지 않는다.
- 긴 설명은 폭 32자 안팎에서 줄바꿈되도록 한다.
- 600 이상의 굵기는 제목과 버튼에만 사용하고, 모든 텍스트를 굵게 만들지 않는다.

---

## 4. Spacing, Layout & Shape

### 4.1 Spacing scale

4px 기반의 일관된 간격을 사용한다.

| Token | Value | Typical use |
|---|---:|---|
| `--space-1` | 4px | 아이콘과 라벨 사이 |
| `--space-2` | 8px | 라벨·헬퍼 텍스트 |
| `--space-3` | 12px | 폼 필드 내부 그룹 |
| `--space-4` | 16px | 기본 컴포넌트 간격 |
| `--space-5` | 20px | 카드 내부 요소 |
| `--space-6` | 24px | 카드 padding |
| `--space-8` | 32px | 섹션 내부 간격 |
| `--space-10` | 40px | 화면 주요 그룹 |
| `--space-12` | 48px | 화면 상하 여백 |
| `--space-16` | 64px | 주요 섹션 분리 |

### 4.2 Responsive layout

- 모바일 기준 폭: 320–430px.
- 모바일 페이지 좌우 padding: 20px (320px 이하에서는 16px).
- 주요 콘텐츠 최대 폭: 480px, 넓은 화면에서는 가운데 정렬.
- 결과 카드 저장 영역: 1080 × 1350px 비율(4:5)을 유지한다.
- 데스크톱에서는 화면을 무리하게 넓히지 말고 중앙의 모바일 경험을 유지한다.
- 주요 CTA는 모바일에서 가능한 한 전체 폭으로 배치한다.
- 하단 고정 CTA를 사용할 경우 콘텐츠가 가려지지 않도록 safe-area와 하단 padding을 확보한다.

### 4.3 Radius

| Element | Radius |
|---|---:|
| Small control / badge | 6px |
| Input / Select | 10px |
| Button | 999px |
| Topic chip | 999px |
| Standard card | 16px |
| Tarot result card | 20px |
| Modal / Dialog | 20px |
| Tarot card artwork frame | 14px |
| Circular icon container | 9999px |

컴포넌트 종류별 radius를 고정한다. 같은 종류의 버튼에 서로 다른 radius를 섞지 않는다.

### 4.4 Borders & elevation

- 기본 경계: 1px solid `rgba(210,216,255,.14)`.
- 카드 안쪽 하이라이트: `inset 0 1px 0 rgba(255,255,255,.08)`.
- 유리 패널: `inset 0 1px 0 rgba(255,255,255,.08), 0 16px 40px rgba(0,0,0,.24)`.
- 타로 카드: `0 18px 50px rgba(0,0,0,.42), 0 0 28px rgba(139,114,232,.12)`.
- 버튼 hover는 배경 밝기와 투명도만 소폭 변화시킨다.

그림자는 계층을 구분하는 데만 사용한다. 모든 요소에 glow를 적용하지 않는다.

---

## 5. Core Components

컴포넌트 API는 shadcn/ui의 조합 가능한 구조를 참고한다. 실제 구현에서는 `Button`, `Card`, `Input`, `Label`, `Badge`, `RadioGroup`, `Dialog` 등의 기본 접근성 패턴을 유지하고, 서비스 전용 컴포넌트는 기본 컴포넌트를 조합한다.

### 5.1 Button

**Variants**

| Variant | Appearance | Usage |
|---|---|---|
| default | Mystic Violet 배경, 흰색 텍스트 | 카드 한 장 뽑기, 타로 시작 |
| secondary | Raised Panel 배경, 밝은 텍스트 | 결과 공유, 보조 행동 |
| outline | 투명 배경, Glass Edge 경계 | 다시 뽑기, 취소 |
| ghost | 투명 배경, hover 시 약한 보라 표면 | 뒤로 가기, 텍스트 액션 |
| destructive | Rose 배경 | 입력 정보 초기화 확인 등 파괴적 행동 |

**Sizes**
- sm: height 36px, horizontal padding 12px, text 14px.
- default: height 44px, horizontal padding 18px, text 14px.
- lg: height 52px, horizontal padding 24px, text 16px.
- icon: 40 × 40px.

**States**
- Default / Hover / Focus-visible / Active / Disabled / Loading.
- Disabled는 opacity만 낮추지 말고 비활성 표면과 텍스트 대비를 확보한다.
- Loading 중 중복 제출을 막고 라벨을 유지하거나 짧은 진행 문구를 보여 준다.
- 터치 타깃은 최소 44 × 44px을 권장한다.

### 5.2 Input & Label

- 높이 48px, radius 10px, 좌우 padding 14px.
- 배경 `rgba(255,255,255,.045)`, 경계 `--input`, 입력 텍스트 `--foreground`.
- placeholder는 `--muted-foreground`.
- focus-visible 시 `--ring` 2px 외곽 링을 사용한다.
- 라벨은 입력 위에 배치하고 placeholder를 라벨 대용으로 사용하지 않는다.
- 오류는 입력 아래에 오류 메시지와 아이콘을 함께 표시한다.
- 생년월일은 실제 날짜인지 검증하고, 날짜 입력이 어렵다면 세그먼트형 날짜 선택 UI를 제공한다.
- 이름은 최대 10자, 닉네임 사용을 안내한다.
- 전공은 선택 입력임을 라벨과 보조 문구에 명시한다.

### 5.3 Topic Chip / Selection

주제 6개 중 하나를 선택하는 단일 선택 컴포넌트다.

- 커리어, 재물, 연애, 건강, 학업, 종합.
- 기본: Raised Panel 배경, 1px Glass Edge, Moon Mist 텍스트.
- 선택: 보라색 계열의 약한 배경, Violet Glow 경계, 밝은 텍스트, 체크 또는 선택 아이콘.
- hover: 배경 밝기만 소폭 증가.
- 선택 여부는 색상뿐 아니라 체크 아이콘 또는 selected 상태로도 전달한다.
- 2열 또는 3열 그리드로 구성하되 좁은 모바일에서 라벨이 줄바꿈되지 않도록 한다.
- 키보드 사용 시 RadioGroup 패턴과 방향키 선택을 지원한다.

### 5.4 Card

**Base Card**
- 배경 `--card`, radius 16px, padding 20–24px.
- 얇은 반투명 경계와 상단 inset highlight.
- 카드 안의 제목·설명·행동 영역을 분리한다.

**Glass Panel**
- 배경 `rgba(185,190,255,.07)`.
- backdrop blur는 지원 환경에서 12–18px.
- 경계는 `rgba(210,216,255,.14)`.
- 본문 가독성이 낮아질 정도로 투명하게 만들지 않는다.

**Tarot Result Card**
- 결과 화면의 핵심 오브젝트. 4:5 비율의 카드 아트워크와 결과 정보를 하나의 저장 단위로 구성한다.
- 외곽 배경은 Deep Night, 프레임은 Champagne Gold 또는 Moon Lavender의 미세한 라인.
- 카드명, 로마 숫자, 별자리, 해석 3줄, 오락용 안내를 일정한 순서로 배치한다.
- 카드 그림은 직접 제작하거나 사용 허가가 명확한 에셋만 사용한다.
- 카드 내부 텍스트는 이미지 저장 후에도 읽을 수 있는 크기를 유지한다.

### 5.5 Badge

- radius 6px, padding 4px 8px, font 12px / weight 500.
- 배경 `rgba(183,168,255,.14)`, 텍스트 `#D8D0FF`.
- 주제, 별자리, 정방향, 아르카나 분류 등에 사용한다.
- 중요 경고나 개인정보 안내를 badge만으로 표현하지 않는다.

### 5.6 Divider

- 1px `rgba(210,216,255,.12)`.
- 장식 구분선은 중앙으로 갈수록 밝아지는 얇은 그라데이션을 사용할 수 있다.
- OR 구분 등 정보 구조를 나눌 때만 사용하고 장식선을 과도하게 반복하지 않는다.

### 5.7 Dialog / Alert Dialog

- radius 20px, 배경 `#171B35`, padding 24px.
- 배경 scrim은 `rgba(3,4,12,.72)`.
- [처음으로]처럼 입력 정보를 삭제하는 행동에는 확인 대화상자를 사용한다.
- 취소와 확인 버튼을 분리하고, 파괴적 행동은 destructive variant로 표현한다.
- 닫기 버튼과 ESC, 바깥 클릭 정책을 명확히 하고 키보드 포커스를 다이얼로그 안에 유지한다.

### 5.8 Toast / Feedback

- 하단 safe-area 위에 표시, 최대 2줄.
- 저장 성공: “이미지를 저장했어요”.
- 저장 불가: 이미지를 화면에 표시하고 “이미지를 길게 눌러 저장해 주세요”.
- 공유 메뉴 없음 + 복사 성공: “결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요”.
- 복사 실패: 공유 메시지를 화면에 표시해 직접 선택·복사할 수 있게 한다.
- 토스트만으로 중요한 개인정보·오류 설명을 대체하지 않는다.

### 5.9 Iconography

- Lucide 계열의 일관된 outline 아이콘을 사용한다.
- 기본 stroke 1.75–2px, 20–24px.
- 별·달·열쇠·카드·공유·다운로드 아이콘을 우선한다.
- 이모지는 주제 선택 라벨의 보조 요소로만 사용하고, 기능 아이콘과 혼용하지 않는다.
- 아이콘 단독 버튼에는 accessible label을 제공한다.

---

## 6. Tarot-specific Visual Language

### 6.1 Card artwork

- 카드 외곽은 세로형 2:3 비율을 기본으로 한다.
- 얇은 이중 프레임, 네 모서리의 작은 별 장식, 상단 로마 숫자, 하단 카드 이름을 공통 구조로 한다.
- 카드 그림의 시각적 중심은 중앙 60% 영역에 둔다.
- 카드별 컬러 변주는 허용하지만 전체 채도는 낮게 유지하고, 브랜드 UI 색상 체계와 충돌하지 않게 한다.
- 22장 메이저 아르카나의 그림은 한 세트처럼 일관된 선 굵기·질감·명암으로 제작한다.

### 6.2 Motifs

- **별자리:** 작은 별점 연결선, 별자리 심볼.
- **달:** 얇은 초승달 실루엣, 달빛 halo.
- **아치:** 카드 프레임이나 이미지 마스크에 사용.
- **별가루:** 배경에 드문드문 배치하고 텍스트 주변은 비운다.
- **금박:** 카드 프레임과 작은 장식에 한정한다.

### 6.3 Motion

- 카드 뽑기: 3D flip 또는 rotateY 기반 뒤집기, 총 700–1000ms 이내.
- 카드 공개 직후 glow는 300–500ms 안에 자연스럽게 사라진다.
- 화면 전환: 180–260ms, ease-out.
- 선택 칩: 120–180ms.
- 애니메이션은 결과를 늦추지 않는다. `prefers-reduced-motion`에서는 회전·이동을 제거하고 짧은 opacity 전환만 사용한다.
- 사용자가 빠르게 연속 입력해도 카드 뽑기 동작은 한 번만 실행한다.

---

## 7. Screen Patterns & User Flow

기획 문서의 S-01~S-03, F-1~F-7 흐름을 기준으로 한다.

### 7.1 S-01 Start

**목표:** 서비스 정체성을 빠르게 전달하고 타로 시작 행동으로 연결한다.

구성 순서:
1. 서비스 심볼 또는 작은 별빛 아이콘.
2. “오늘의 타로” 서비스 타이틀.
3. 카드 뒷면 아트워크 — 화면의 시각적 중심.
4. “내 정보를 넣고 카드 한 장으로 나만의 해석을 받아 봐요” 설명.
5. Primary CTA: “타로 시작”.
6. “오락용 타로 · 입력 정보는 저장하지 않아요” 안내.

레이아웃은 중앙 정렬, 상단 광원, 넉넉한 여백을 사용한다. 시작 버튼은 화면에서 가장 명확한 액션이어야 한다.

### 7.2 S-02 Personal Info & Topic

**목표:** 필수 정보와 주제를 빠르게 입력하고 개인정보 사용 방식을 이해시킨다.

구성 순서:
1. 뒤로 가기 + “나에 대해 알려 주세요”.
2. 이름 입력 (최대 10자, 닉네임 가능).
3. 생년월일 입력 (실제 날짜 검증).
4. 전공 입력 (선택).
5. “어떤 주제가 궁금한가요?” + 6개 주제 선택.
6. 개인정보 안내문.
7. Primary CTA: “카드 한 장 뽑기”.

CTA는 이름·생년월일·주제가 모두 유효할 때만 활성화한다. 비활성 상태에서도 버튼의 위치와 문구는 유지해 다음 행동을 예측할 수 있게 한다.

개인정보 안내 문구는 다음을 그대로 사용한다.

> 입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.

### 7.3 Card Draw transition

- CTA를 누르면 버튼 중복 입력을 막는다.
- 22장 중 무작위 한 장을 정방향으로 뽑는다.
- 카드 뒤집기 효과는 1초 이내로 완료한다.
- 모션 중에도 화면이 멈춘 것처럼 보이지 않도록 간단한 진행 상태를 제공한다.
- 역방향·여러 장 스프레드는 MVP 범위에 포함하지 않는다.

### 7.4 S-03 Result

**목표:** 개인화된 결과를 읽고 이미지 저장 또는 공유를 선택하도록 한다.

결과 카드 구성:
1. “{이름}님의 타로 · {주제}”.
2. 타로 카드 그림.
3. 카드 이름 및 로마 숫자.
4. 별자리 표시.
5. 해석 3줄 — 총 90자 이내.
6. “※ 오락용 타로 해석입니다”.
7. 서비스 이름 또는 작은 워드마크.

결과 해석은 카드 × 주제 기본 문장 + 별자리 문장 + (전공 입력 시) 전공 계열 문장으로 구성한다. 전공을 분류하지 못하면 세 번째 줄은 생략한다.

- 건강·재물은 단정적인 예언이나 의학·재정 조언을 하지 않는다.
- 생년월일과 전공 원문은 결과 카드에 표시하지 않는다.
- 결과 아래 액션: [이미지 저장] [결과 공유].
- 보조 액션: [다시 뽑기] [처음으로].
- 개인정보 미저장 안내를 결과 화면에도 표시한다.

### 7.5 Save / Share

**Image Save**
- PNG 1080 × 1350px, 4:5 비율.
- 결과 카드의 이름·주제·카드 그림·카드명·별자리·해석·오락용 안내·서비스 이름을 포함한다.
- 생년월일과 전공 원문은 포함하지 않는다.
- 저장이 지원되지 않으면 화면에 이미지 미리보기를 띄우고 길게 눌러 저장하도록 안내한다.

**Share**
- 기기 공유 메뉴를 먼저 연다. 가능한 경우 이미지와 텍스트를 함께 전달한다.
- 공유 메뉴를 사용할 수 없으면 글을 자동 복사한다.
- 공유 문구에는 이름·주제·카드·별자리·해석·오락용 안내·시작 링크를 포함한다.
- 시작 링크에는 이름이나 결과를 넣지 않는다.
- 공유 메뉴를 취소해도 결과 화면을 유지한다.

**Retry / Reset**
- 다시 뽑기: 같은 입력 정보를 유지하고 주제 선택 단계부터 다시 시작한다.
- 처음으로: 확인 후 모든 입력 정보를 비우고 S-01로 이동한다.
- 브라우저 저장소, 쿠키, 서버, 분석 도구에 개인정보나 결과를 저장·전송하지 않는다.

---

## 8. Tailwind CSS v4 Implementation

### 8.1 CSS-first theme

Tailwind v4의 `@theme`와 CSS custom properties를 사용한다. 색상은 의미 기반 변수에 연결하고 컴포넌트에서 hex를 반복하지 않는다.

```css
@import "tailwindcss";

:root {
  color-scheme: dark;

  --background: #080a18;
  --foreground: #f4f0ff;
  --card: #171b35;
  --card-foreground: #f4f0ff;
  --popover: #171b35;
  --popover-foreground: #f4f0ff;
  --primary: #8b72e8;
  --primary-foreground: #ffffff;
  --secondary: #202544;
  --secondary-foreground: #e7e3ff;
  --muted: #202544;
  --muted-foreground: #9296b0;
  --accent: #2b2850;
  --accent-foreground: #f4f0ff;
  --destructive: #d96b7a;
  --destructive-foreground: #ffffff;
  --border: rgba(210, 216, 255, 0.14);
  --input: rgba(210, 216, 255, 0.18);
  --ring: #b7a8ff;

  --radius: 0.75rem;
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);

  --font-sans: "Pretendard", "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-serif: "Cormorant Garamond", "Noto Serif KR", serif;
}
```

### 8.2 Utility conventions

- 토큰이 존재하면 `bg-background`, `text-foreground`, `border-border`, `bg-card`처럼 semantic utility를 사용한다.
- 임의 색상은 반복하지 말고 토큰으로 승격한다.
- 반복되는 레이아웃은 컴포넌트로 추출하고 긴 조건부 class는 `cn()` 패턴으로 정리한다.
- 반응형은 mobile-first로 작성한다. 기본 클래스가 모바일, `sm:`·`md:`는 확장 화면을 뜻한다.
- spacing은 4px scale을 따른다. 의미 없는 임의 간격을 늘리지 않는다.
- hover만으로 기능을 전달하지 않는다. 터치·키보드 상태도 정의한다.
- 다크 테마가 기본이므로 색상 토큰에 light-theme 값을 혼합하지 않는다.

### 8.3 Example class recipes

```tsx
// Primary CTA
<Button className="h-13 w-full rounded-full bg-primary px-6 text-base font-semibold text-primary-foreground shadow-[0_8px_28px_rgba(139,114,232,0.24)] hover:bg-primary/90 focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 focus-visible:ring-offset-background">
  카드 한 장 뽑기
</Button>

// Glass panel
<Card className="rounded-2xl border border-border bg-[linear-gradient(145deg,rgba(210,216,255,0.08),rgba(139,114,232,0.035))] p-6 shadow-[inset_0_1px_0_rgba(255,255,255,0.08),0_16px_40px_rgba(0,0,0,0.24)]">
  ...
</Card>

// Text input
<Input className="h-12 rounded-[10px] border-input bg-white/[0.045] px-3.5 text-foreground placeholder:text-muted-foreground focus-visible:ring-2 focus-visible:ring-ring" />
```

예시는 시각적 레시피다. 실제 코드에서는 프로젝트의 shadcn/ui 컴포넌트 API와 설치된 Tailwind 버전에 맞춰 조정한다.

---

## 9. Accessibility & Content Rules

- 본문과 배경은 WCAG AA 대비를 목표로 한다. 일반 텍스트 4.5:1, 큰 텍스트 3:1을 기준으로 확인한다.
- 키보드 포커스는 항상 보이게 하고 ring을 제거하지 않는다.
- 모든 입력에는 연결된 Label과 명확한 오류 설명이 있어야 한다.
- 주제 선택은 단일 선택임을 스크린 리더에 전달한다.
- 아이콘 단독 버튼에는 accessible name을 제공한다.
- 색상만으로 선택·오류·성공을 구분하지 않는다.
- 최소 터치 타깃은 44 × 44px을 권장한다.
- reduced motion 환경에서는 카드 뒤집기 등 비필수 애니메이션을 축소한다.
- 결과 문구는 한국어 존댓말을 사용하고 따뜻하고 단정한 톤을 유지한다.
- 건강·재물 관련 문구는 판단이나 예언이 아니라 돌아볼 관점으로 작성한다.
- “반드시”, “확실히”, “무조건”, “치료된다”, “큰돈을 번다” 같은 단정 표현을 피한다.
- 결과·저장 이미지·공유 메시지에 오락용 안내를 항상 포함한다.

---

## 10. Design QA Checklist

### Foundations
- [ ] 페이지 배경과 본문 텍스트가 semantic token을 사용한다.
- [ ] 브랜드 보라색은 주요 액션과 선택 강조에 제한된다.
- [ ] Champagne Gold는 카드 장식에만 절제해 사용한다.
- [ ] spacing과 radius가 정의된 scale을 따른다.
- [ ] 제목·본문·캡션의 계층이 명확하다.

### Components
- [ ] 버튼에 default / hover / focus / active / disabled / loading 상태가 있다.
- [ ] 입력에 label / placeholder / focus / error 상태가 있다.
- [ ] 주제 선택은 단일 선택과 키보드 조작을 지원한다.
- [ ] 카드 프레임과 본문 텍스트의 대비가 충분하다.
- [ ] 다이얼로그와 토스트가 모바일 safe-area를 고려한다.

### Product flow
- [ ] S-01에서 타로 시작 CTA가 명확하다.
- [ ] S-02에서 이름·생년월일·주제 필수 검증이 동작한다.
- [ ] 전공은 선택 항목임이 분명하다.
- [ ] 개인정보 안내가 입력·결과 화면 모두에 표시된다.
- [ ] 카드 뽑기 애니메이션이 1초 이내다.
- [ ] 결과 해석이 3줄·90자 이내다.
- [ ] 저장 이미지가 PNG 1080 × 1350px이다.
- [ ] 저장·공유 결과에 생년월일과 전공 원문이 없다.
- [ ] 공유 링크에 이름이나 결과가 포함되지 않는다.
- [ ] 처음으로를 누르면 모든 입력 정보가 지워진다.
- [ ] 오락용 안내가 결과·이미지·공유 메시지에 표시된다.

---

## 11. Source of Truth

이 디자인 시스템은 아래 기획 문서를 기반으로 한다.

- `TARO_01_PRD.md`: 제품 목표, 사용자, MVP 범위, 개인정보·콘텐츠 원칙.
- `TARO_02_기능명세서.md`: F-1~F-7 기능 동작, 입력 검증, 해석 구성, 저장·공유 예외 상태.
- `TARO_03_유저플로우.md`: 시작부터 결과, 저장·공유 실패 분기, 재시작 흐름.
- `TARO_04_와이어프레임.md`: S-01 시작, S-02 입력, S-03 결과 화면 구조와 문구.

기획 문서와 이 디자인 가이드가 충돌하면 개인정보 보호·기능 완료 조건은 PRD와 기능명세서를 우선하고, 시각적 표현은 이 문서를 따른다. 이 문서는 MVP 범위를 확장하지 않으며, 역방향 카드·다중 스프레드·로그인·결과 이력 기능을 추가하지 않는다.
