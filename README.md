# Fraud-Detection-Credit-Score-System
온라인 쇼핑몰에서 발생할 수 있는 결제 사기 및 오작동을 막는 FDS 시스템에 대해 연구하는 자료 입니다. 

### 참고자료
```
1. 캐글 데이터 : https://www.kaggle.com/mlg-ulb/creditcardfraud
2. FDS with ML : https://www.researchgate.net/project/Fraud-detection-with-machine-learning
```

### FDS란?
```
금융기업에서 다양한 금융사기에 대한 사전/사후대응을 지원하는 이상거래 탐지 시스템 - Fraud Detection System

이러한 FDS는 정보수집, 이상거래 분석, 대응으로 구성된다. 
1. 로그 수집 시스템 : 실시간 거래정보를 수집하고 대용량 데이터를 정제하여 이상거래 분석 시스템
2. 이상거래 분석 시스템 : 로그 수집에서 전달받은 데이터와 고객정보, 외부정보를 종합적으로 판단하여 거래이상 여부를 판단
3. 대응 시스템 : 이상거래 분석 시스템이 이상거래라고 판단한 거래에 대해 유형별 대응 시나리오에 따라 사용자 접속차단, 담당자에게 확인 알람 등의 자동화된 시스템 조치를 수행
- 인공지능 탐지 모델은 새로이 발견된 거래 패턴에 대한 내용을 학습하여 성능을 개선하고 이를 이상거래 분석 시스템에 수시로 반영함
```
<img src="https://www.2e.co.kr/news/photo/202012/301050_3752_120.jpg" />

### FDS 분석 방법
```
1. 오용탐지 기법 : 기존 이상거래 또는 사기거래에서 나타나는 주요 특징들을 조건화, 규칙화 하여 새로히 발생하는 금융거래에 다중 조건을 적용하여 필터링하는 방식으로 이상거래 여부를 식별 ex) 특정 고객이 거래하던 월 평균 금액보다 100배 이상 큰 금액이 새벽에 이체가 되고 구매가 속한 경우
2. 이상탐지 기법 : RDBMS에 저장된 고객 기번 정보, 거래 정보 등의 속성 정보를 바탕하여 모델링하여 특이점을 탐지하는 것이다. 또한, 고객이 가지고 있는 정적 변수(Static Variable)와 거래 정보에 따라 변화하는 동적 변수(Dynamic Variable)를 기본적으로 활용하여 분석함. ex) 손해보험사에서는 자동차 고의 사고 보험사기 사례에서 보험금 청구 고객의 고객기본정보(나이, 성별, 면허취득일), 상품정보(상품명, 가입특약, 가입일), 보험금 청구 거래정보(치료병원, 사고장소, 사고일, 청구일, 입원일수, 청구금 등), 외부기관 정보(통신사 정보, 신용평가기관, 의료보험 정보 등)를 종합적으로 분석하여 청구 거래 건이 사기일 가능성을 분석하여 경고를 줌.
```

### 주제선정 및 이유
    1. 실제 금융 비즈니스를 하고 있는데 기업이 가진 돈과 자원은 한정적이라 자금을 효율적으로 운용하기 위해서는 연체율을 줄여야 함
    2. 주 고객과 타겟층은 Thin Filer로 대체로 20대 대학생이 대다수를 차지하고 있음 
    3. 이들은 기존 금융거래 이력이 부족하여 신용카드 이용 및 발급 과정에서 어려움을 겪고 있음
    4. 결제 서비스 진행 과정에서 20대의 연체율을 예측하고 줄여나가고자 함

### 스토리 잡기
    1. 기존 신용평가 모델에서 제대로 평가하지 못하고 있는 Thin Filer들에게 금융 혜택을 주기 위한 여러가지 시도들이 있는데 이것이 바로 대안 신용평가 모델임
    2. 주요 변수/핵심 포인트 : 
    
### 과업 수행의 Outline 잡기
    1. 기존 신용평가 모형의 정의
       - 기존 신용평가 모형은 각 개인의 신용도를 평가하여, 신용평점 또는 신용등급을 산출하는 시스템을 의미함.
       - 즉, 신용이란 약속을 지킬 수 있는 능력을 말하며, 금융시장에서는 채무를 제때 갚을 수 있는 능력이나 직접 채무를 얻는 행위를 지칭함
    2. 신용평가의 구분
       - 신용평가는 크게 개인 신용평가와 기업 신용평가로 구분할 수 있음. 개인 신용평가는 소매 금융에서의 신용을 평가하고, 기업 신용평가는 기업 금융에서의 신용을 평가함
    3. 신용등급 종류
       - 개인 신용등급은 개인신용평가사에서 전국민을 대상으로 신용도를 평가한 신용평가사 신용등급(CB 등급: Credit Bureau 등급)과 개별 기관에서 자체적으로 고객 또는 관련인의 신용도를 평가한 내부 신용등급(CSS 등급: Credit Scoring System 등급) 두 종류가 존재하고 있음
       - 신용평가사 신용등급(CB등급): 개인신용평가사가 수집한 각 개인의 다양한 신용정보를 종합하여, 통계적 방법으로 신용 수준을 분석하여 산출한 신용도 지표, 점수가 높을 수록 1년 내 신용 부실 가능성이 낮음
       - 내부 신용등급(CSS등급): 대출심사, 신용카드발급, 한도/금리 산정 등의 업무 처리를 위해, 내부 정보와 신용평가사의 정보를 모두 종합하여, 각 기관별로 최적화된 맞춤 신용도를 평가한 지표

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcLkyZf%2Fbtqzb8DiomV%2FtSBxTm9u2iIHaJagRVIZK1%2Fimg.png" />

    4. 신용평가 활용정보
       - 신용정보는 예금, 대출, 신용카드 사용 등 금융회사와의 거래내용과 세금체납, 재산, 소송 등 공공기관의 정보를 모두 수집하여 판단

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FslPwy%2Fbtqzb8i0H3Q%2Fk9BA34sRtN2A7hhuLhv0G1%2Fimg.png" />
