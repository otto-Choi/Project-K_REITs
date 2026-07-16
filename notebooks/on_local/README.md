# 로컬실행 노트북

> 로컬(Windows)에서 실행 가능한 노트북만 모아둔 폴더.
> 원본은 상위 `notebooks/`에 그대로 있고, 여기 있는 건 **복사본**입니다.

## 데이터

별도 복사 없이 기존 데이터를 그대로 참조합니다.
- 이 폴더가 `notebooks/로컬실행/`이라 데이터 경로는 **`../../data/raw/...`** (리츠/data) 또는 **`../colab/...`** (notebooks/colab)로 맞춰져 있습니다.
- 그래서 **반드시 이 폴더 기준으로 노트북을 열어 실행**해야 경로가 맞습니다 (VS Code·Jupyter는 노트북 위치를 자동으로 작업 폴더로 잡음).
- ※ `div`는 `data/raw/div.csv`(대문자 컬럼)가 아니라 스키마가 맞는 **`../colab/div.csv`**(소문자 `date`·`div_per_stock`)를 씁니다.

## 실행 환경

- 패키지 설치 완료: `arch`, `yfinance` (+ pandas·numpy·matplotlib·statsmodels·xlsxwriter)
- 한글 폰트: 맑은 고딕(`C:/Windows/Fonts/malgun.ttf`)으로 패치됨
- 코랩 전용 코드(`!apt`, `google.colab`, 나눔폰트 경로)는 주석/교체됨

## 노트북별 상태

| 노트북 | 상태 | 비고 |
|---|---|---|
| **GARCH_m모형_샘플_ (2)** | ✅ 전체 실행 검증됨 | 리츠/PF 22-24 사용 |
| **reits_pffo_g_user_schema** | ✅ 전체 실행 검증됨 | `../../data/raw/reit_panel_simple.csv` |
| **div** | ✅ 전체 실행 검증됨 | `../colab/div.csv` 사용 (스키마 일치) |

## 여기에 없는 노트북 (로컬 실행 불가 → 제외)

`notebooks/`에 원본이 있으나, repo에 없는 데이터가 필요해 제외:
- **포트폴리오 모델링 / 포트폴리오 모델링_시각화** — **팀원 작업**. 관련 데이터(`부동산_pf.csv`, `kospi100_list.csv`)가 repo에 없어 로컬 실행 불가 → 이 폴더에서 제외(삭제)
- **거시변수와 리츠의 상관관계 분석** — `base_rate.csv`, `cpi.csv` 없음
- **내재가치 분석** — 팀원(minju) PC 데이터 9개 없음

> 데이터를 구하면 이 폴더로 복사해 오고 경로를 `../../data/...`로 맞추면 됩니다.
> 상세: 상위 폴더 `notebooks/_실행가이드_로컬과Colab.md` 참고.
