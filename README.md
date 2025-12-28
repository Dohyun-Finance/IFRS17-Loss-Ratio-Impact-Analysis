# 📑 [IFRS17] 보험사 손해율 규제 가이드라인에 따른 재무 영향 분석

### 📌 프로젝트 한줄 요약
**금융당국의 무해지·저해지 보험 손해율 가이드라인(90%) 적용에 따른 보험사 미래 이익(CSM) 변동 및 자본 건전성(K-ICS) 민감도 시뮬레이션**

---

## 2-1. 프로젝트 개요 (Project Overview)
본 프로젝트는 2025년 금융당국이 제시한 **'신규 담보 손해율 가이드라인'** 이 보험사의 재무제표에 미치는 영향을 정량적으로 분석하기 위해 기획되었습니다. 기존의 낙관적인 가정(손해율 65% 내외)에서 당국 권고치(90%)로 가정을 변경했을 때 발생하는 **미래 서비스 마진(CSM)의 위축**과 **지급여력비율(K-ICS)의 하락폭**을 머신러닝 및 재무 모델링으로 구현했습니다.

**핵심 내용 및 주요 기능:**
* **시나리오 기반 데이터 생성**: 주요 보험 상품군(건강, 상해, 암, 종신)별 계약 및 재무 시뮬레이션 데이터 구축
* **수익성 분포 분석**: 규제 도입 전후의 CSM 분포 변화(Shift) 분석 및 손실부담계약 비중 산출
* **IFRS17 재무 시뮬레이션**: CSM 상각 로직 및 손실부담금(Loss Component) 즉시 비용 처리 로직 구현
* **건전성 스트레스 테스트**: 머신러닝 기반 손해율 예측 및 K-ICS 비율 민감도 시뮬레이션

---

## 2-2. 기술 스택 (Tech Stack)
### Language
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
### Libraries
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![Seaborn](https://img.shields.io/badge/Seaborn-blue?style=for-the-badge&logo=pandas&logoColor=white)
### Tools
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

---

## 2-3. 분석 방법론 및 재무 로직 (Methodology and Logic)

### 1) 데이터 컬렉팅 (Data Collecting)
* IFRS17 환경을 반영하여 보험료(Premium), 사업비율(Expense Ratio), 손해율(Loss Ratio) 변수를 포함한 1,000건의 합성 데이터 생성.
* 실제 금융권 규제 시나리오를 바탕으로 낙관적 시나리오(65%)와 규제 시나리오(90%) 대조군 설정.

### 2) 재무 로직 및 모델링 (Financial Logic & Modeling)
* **CSM 산출 모델링**: 
  $$CSM = \text{PV of Future Cash Inflow} - \text{PV of Future Cash Outflow} - \text{RA}$$
* **수익 인식 로직**: CSM 잔액에 상각률(10%)을 적용하여 연간 이익 인식.
* **K-ICS 민감도 로직**: 
  $$\text{K-ICS Ratio} = \frac{\text{Available Capital (Base + Profit)}}{\text{Required Capital}} \times 100$$
* **머신러닝 모델링**: Random Forest Regressor를 활용하여 기초 지표 기반의 미래 가이드라인 손해율 예측.

---

## 2-4. 주요 분석 결과 (Key Findings)

### [분석 1] 규제 전후 수익성 분포 변화
![수익성 분포 분석](./outputs/figures/loss_ratio_impact_analysis.png)
* **결과 요약**: 규제 가이드라인 적용 시, 포트폴리오의 이익 분포가 플러스(이익) 구간에서 마이너스(손실) 구간으로 급격히 이동함.
* **사진 설명**: KDE Plot을 통해 규제 도입 전후의 수익 분포 Shift를 시각화하였으며, 손실부담계약 비중이 유의미하게 증가함을 입증.

### [분석 2] 재무 제표 영향도 시뮬레이션
![재무 영향 분석](./outputs/figures/financial_impact_analysis_final.png)
* **결과 요약**: 손해율 90% 가정 시 전체 CSM 규모는 약 **28.0억 원에서 음수권으로 하락**함.
* **사진 설명**: CSM 총액과 연간 인식 이익의 변동을 '억 원' 단위로 비교하여 규제 도입에 따른 당기순이익 하락 폭을 정량화함.

### [분석 3] K-ICS 건전성 민감도 분석
![건전성 분석](./outputs/figures/kics_sensitivity_analysis.png)
* **결과 요약**: 당기순이익 하락으로 인해 **K-ICS 비율이 기존 대비 약 20%p 이상 하락**하는 충격 발생.
* **사진 설명**: 가용자본 감소에 따른 K-ICS 비율의 변화를 금융당국 권고치(150%) 및 법적 기준선(100%)과 비교 분석함.

---

## 2-5. 인사이트 (Insights)

1.  **보수적 회계 가정의 중요성**: 이번 시뮬레이션을 통해 낙관적 가정이 보험사의 재무 건전성을 왜곡할 수 있음을 확인했으며, 금융당국의 가이드라인 준수가 장기적 재무 투명성 확보의 핵심임을 도출함.
2.  **상품 포트폴리오 재편 필요성**: 손해율 90% 적용 시 수익성이 마이너스로 전환되는 상품군이 확인됨에 따라, 보장성 보험 중심의 고수익 상품 포트폴리오 믹스 개선 전략이 필수적임.
3.  **선제적 리스크 관리 및 자본 확충**: K-ICS 비율이 권고치 이하로 하락할 위험이 감지됨에 따라, 보험사는 후순위채 발행이나 자산-부채 관리(ALM) 고도화를 통해 가용자본을 선제적으로 확보해야 함.
4.  **데이터 기반 규제 대응 체계**: 머신러닝 예측 모델을 활용한 상시 스트레스 테스트 체계를 구축함으로써, 향후 추가적인 규제 변화나 시장 변동성에 유연하게 대응할 수 있는 의사결정 기반 마련.
