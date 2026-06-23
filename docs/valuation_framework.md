# REIT Valuation Framework — FFO Reconstruction

## Why Net Income Is Insufficient for REIT Valuation

일반 기업에서는 Net Income을 valuation의 출발점으로 사용한다.  
REIT에서는 이 접근이 구조적으로 왜곡을 만든다.

REIT가 보유한 부동산 자산은 회계 규칙에 따라 정기적으로 감가상각되지만,
실제 부동산의 경제적 가치는 오히려 시간이 지남에 따라 유지되거나 상승하는 경우가 많다.
이 괴리가 Net Income을 **현금창출력보다 만성적으로 낮게** 보이게 만든다.

추가로 자산 처분이익, 비반복적 손익 항목이 섞이면서 Net Income의 기간 간 비교 가능성이 낮아진다.

**FFO(Funds From Operations)** 는 이 왜곡을 제거한 REIT 고유의 수익성 지표다.

---

## FFO Reconstruction Methodology

### 기본 공식

```
  Reported Net Income
+ Depreciation & Amortization (D&A)
− Asset Disposal Gain (자산 처분이익)
± Non-recurring Adjustments (비반복 손익)
= Adjusted FFO
```

### 항목별 처리 기준

**① Depreciation & Amortization 가산**

- DART 사업·분기보고서 현금흐름표(영업활동 조정 항목)에서 직접 추출
- 리츠마다 계정과목명이 상이하므로("감가상각비", "투자부동산감가상각비" 등) 반기별로 수동 검증

**② 자산 처분이익 차감**

- 비반복적 자산 매각에서 발생한 처분이익·처분손실을 손익계산서에서 분리
- 처분손실은 더하고 처분이익은 빼는 방향으로 조정 → 반복 가능한 영업 현금흐름만 남김

**③ 비반복 항목 조정**

- 유상증자 비용, 파생상품평가손익, 일회성 소송 관련 손익 등
- 항목별로 지속 가능성을 판단해 조정 여부 결정

### 배당 시계열 병행 정제

FFO와 독립적으로 배당 데이터도 별도 정제했다.

- 특별배당(자산 처분 재원 배당 등) 분리 → 정규 배당(regular dividend)만 추출
- 리츠별 배당 지급 이력 검토 후 이상치 플래그 처리
- 정제된 배당 시계열은 DDM의 독립적 입력값으로 사용

---

## Discount Rate Construction

각 리츠에 대해 CAPM 기반 자기자본비용(Cost of Equity)을 추정했다.

```
r = R_f + β × ERP
```

| 구성요소 | 출처 | 비고 |
|---|---|---|
| **R_f** (무위험이자율) | 한국은행 ECOS 국고채 금리 | 분석 시점 기준 |
| **β** (베타) | 한국공인회계사회 5년 반기 조정 베타 | 2011–2025, 리츠별 |
| **ERP** (Equity Risk Premium) | Damodaran (2025) | 국가별 ERP 적용 |

**베타 데이터 처리:**  
한국공인회계사회에서 반기 단위로 공시하는 조정 베타를 수집·병합했다.
상장 시점에 따라 베타 추정 기간이 짧은 리츠는 별도 플래그를 부여했다.

---

## Growth Rate Assumptions

리츠의 법적 배당 의무를 반영해 성장률 가정을 설계했다.

**구조적 제약:**
- 상법 및 리츠 관련 법령상 이익의 90% 이상을 배당해야 함
- 이는 retained earnings가 거의 없음을 의미 → 내부 자금을 통한 유기적 성장 제한
- 성장은 주로 외부 자금(유상증자, 차입) 조달에 의존

**성장률 상한 설정:**
- 기대 인플레이션(한국은행 ECOS)을 **보수적 성장률 상한**으로 사용
- 이는 REIT가 장기적으로 인플레이션 이상의 내생적 성장을 기대하기 어렵다는 판단에 근거
- 성장률 하한은 0으로 설정 (배당 삭감 시나리오 배제)

---

## Data Sources

| 데이터 | 출처 |
|---|---|
| 사업·분기보고서 (D&A, 처분손익) | 금융감독원 DART |
| 배당 이력 | DART 배당 공시 |
| 5년 반기 조정 베타 | 한국공인회계사회 |
| 기준금리, 기대 인플레이션 | 한국은행 ECOS |
| Equity Risk Premium | Damodaran (2025) |
| 상장 리츠 가격·시가총액 | KRX marcap |
