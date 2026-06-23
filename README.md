# Project-K_REITs
### REIT Valuation Case Study — Accounting Normalization · FFO Reconstruction · DCF/DDM

> REIT는 Net Income만으로 valuation할 수 없다.  
> 회계 왜곡을 제거해 Adjusted FFO를 재구성하고,  
> 국내 상장 리츠의 intrinsic value와 할인 구조를 분석한 valuation case study.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)

**기간:** 2025.10 – 2025.11 &nbsp;|&nbsp; **형태:** 팀 프로젝트 (데이터 분석 학회)

---

## The Problem

국내 상장 리츠는 오랜 기간 intrinsic value 대비 할인된 가격에 거래되어 왔다.  
그러나 "저평가"를 논하려면 먼저 신뢰할 수 있는 intrinsic value estimation이 있어야 한다.

문제는 **REIT의 재무제표를 일반 기업과 같은 방식으로 읽으면 안 된다**는 것이다.  
회계상 Net Income은 REIT의 실질 현금창출력을 왜곡하며, 이를 그대로 valuation에 투입하면 결과 자체가 틀린다.

DART 공시의 비정형 disclosure를 정규화하여 valuation-ready dataset을 구축하는 것이 분석의 출발점이었다.

---

## Why REIT Valuation Is Hard

| 회계·구조적 이슈 | 영향 |
|---|---|
| **감가상각 과대계상** | 부동산 자산의 실제 경제적 가치 하락 < 회계상 D&A → Net Income 만성적 과소계상 |
| **자산 처분이익** | 비반복적 매각익이 Net Income을 일시적으로 부풀림 → 지속 가능성 없는 CF |
| **배당 의무 (이익의 90% 이상)** | Retained earnings 거의 없음 → 내생적 성장(reinvestment) 구조적 제한 |
| **잦은 유상증자** | 성장 재원을 외부 조달에 의존 → dilution risk 상시 내재 |

> **핵심:** REIT valuation에서 accounting normalization은 선택이 아니라 전제 조건이다.

---

## Valuation Framework

### 1. Accounting Normalization — FFO Reconstruction

Net Income에서 회계 왜곡 항목을 제거하고 **Adjusted FFO**를 재구성했다.

```
  Reported Net Income
+ Depreciation & Amortization
− Asset Disposal Gain
± Non-recurring Adjustments
= Adjusted FFO
```

- DART 공시(사업·분기보고서)에서 D&A, 자산처분손익, 비반복 조정 항목을 리츠별·반기별로 직접 추출·정제
- 특별배당·처분이익 등 일회성 요인을 분리해 **지속 가능한 배당(sustainable dividend)** 시계열 재구성
- FFO와 독립적으로 배당 시계열도 병행 정제 → DDM 입력값의 독립적 검증 기반 확보

→ 상세 방법론: [`docs/valuation_framework.md`](docs/valuation_framework.md)

### 2. Discount Rate & Growth Rate

**할인율 (r):** 리츠별 CAPM 기반 자기자본비용 추정

- Beta: 한국공인회계사회 5년 반기 조정 베타 (2011–2025)
- ERP: Damodaran (2025) 국가별 Equity Risk Premium
- R_f: 한국은행 ECOS 국고채 금리

**성장률 (g):** 배당 의무 구조를 반영한 보수적 추정

- 이익의 90% 이상 배당 의무 → reinvestment 기반 내생적 성장 제한
- 기대 인플레이션(한국은행 ECOS)을 **성장률 상한**으로 설정

### 3. DCF vs. DDM — 왜 두 모델을 모두 적용했는가

두 모델을 병행한 이유는 투입값의 불확실성을 교차 검증하기 위해서다.

| | DCF | DDM |
|---|---|---|
| **현금흐름** | Adjusted FFO | 조정 배당 |
| **불확실성** | FFO 추정 오차 내재 (조정 방식에 민감) | 배당은 공시 수치에 근접, 상대적으로 안정 |
| **REIT 적합성** | 이론적으로 타당하나 실무 적용 어려움 | 배당 의무 구조상 실무적으로 더 robust |

**결론:** 국내 상장 리츠 현황에서는 **DDM intrinsic value가 실무적으로 더 해석 가능하다.**  
FFO는 감가상각·처분이익 조정 방식에 따라 추정값의 편차가 크고 신뢰구간이 넓어진다. 반면 배당은 공시 수치와의 차이가 작아 결과의 해석 가능성이 높다.

→ 모델 비교 상세: [`docs/ddm_vs_dcf.md`](docs/ddm_vs_dcf.md)

---

## Portfolio Diversification Analysis

리츠를 valuation 대상뿐 아니라 portfolio asset으로도 평가했다.

3개 투자 시나리오(S1–S3: 개인투자자형 주식 / ETF / KOSPI 100 최적화)에서 리츠·리츠지수·고배당주 편입 효과를 비교했으며, GARCH-M 기반 조건부 변동성을 통해 Sharpe Ratio와 volatility 변화를 분석했다.

---

## Key Findings

**Valuation**
- 시장 할인은 mispricing보다 uncertainty pricing에 가까웠다 — FFO opacity가 커질수록 required discount도 확대되었다
- 금리 급등·대규모 유상증자 시기에 괴리 최대화 → 거시 이벤트가 uncertainty를 증폭시키는 경로 확인
- FFO 기반 DCF보다 **배당 기반 DDM intrinsic value가 실무적으로 더 수용 가능** — 조정 방식 의존도가 낮고 해석 가능성이 높다

**Portfolio**
- 리츠 편입 시 변동성 감소 효과 확인; 단, 효과 크기는 기존 포트폴리오의 분산 정도에 크게 의존
- 일률적 편입 권고보다 **포트폴리오 특성에 따른 비중 조절**이 핵심

---

## My Contributions

- REIT valuation framework 설계 — DCF/DDM dual-track 구조 및 두 모델 병행 근거 수립
- Adjusted FFO reconstruction logic 정의 — 조정 항목 선정 기준 및 리츠별 처리 방식 설계
- DART 공시 기반 데이터 수집 및 normalization — 비정형 반기 공시에서 패널 데이터 구축
- Growth rate · discount rate assumption rationale 수립 — 배당 의무 구조와 거시 변수를 반영한 가정 체계화

---

## Limitations

- **FFO 추정 한계:** DART 공시 기반 재구성으로, 자산 단위(임대료·공실률·잔존만기) 정보 미반영
- **표본 제약:** 분석 기간 내 금리·인플레이션 급변 구간이 결과에 과도하게 반영될 가능성
- **모형 가정:** 성장률·ERP·베타 가정에 대한 체계적 민감도 분석 미수행
- **범위:** 국내 상장 리츠에 한정; 비상장·해외 리츠와의 비교 없음

## Next Steps

- 자산 단위 운영 지표(공실률·임대료·잔존만기) 반영으로 FFO 추정 정밀도 개선
- Sensitivity analysis 및 시나리오별 stress testing 체계화

---

## Related Documents

| 문서 | 내용 |
|---|---|
| [`docs/valuation_framework.md`](docs/valuation_framework.md) | FFO reconstruction 방법론 상세 |
| [`docs/ddm_vs_dcf.md`](docs/ddm_vs_dcf.md) | DCF vs DDM 모델 비교 및 sensitivity |
| [`docs/presentation/`](docs/presentation/) | 최종 발표자료 |
| [`docs/meeting_notes/`](docs/meeting_notes/) | 분석 과정 회의록 |
