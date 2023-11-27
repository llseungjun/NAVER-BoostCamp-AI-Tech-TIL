출처: https://gaussian37.github.io/ml-concept-ml-evaluation/ (Confusion Matrix)
https://process-mining.tistory.com/34 (Assosiation Rule)

# Recommendation System concept
### Search와 Recommendation의 차이
- pull : 사용자가 원하는 것을 직접 프로그램에 입력하는 방식(Search)
- pull : 프로그램이 사용자가 원할 것 같은 정보를 사용자에게 제공하는 방식(Recommendation)

### 추천시스템 왜 쓸까?
- 과거 : 컨텐츠가 제한적
- 현재 : 다양한 컨텐츠가 생산됨
- Long Tail Phenomenon : 아이템의 개수가 기하급수적으로 많아지며 현재의 상황에서 인기있는 소수의 아이템만 많이 소비되고 그 외 다른 아이템들은 적게 소비 되는 현상
- 컨텐츠가 너무 많아서 유저가 정보를 찾는데 시간이 오래걸림
- 결론 : Long Tail 부분의 컨텐츠에 대한 추천과 유저가 정보를 찾는 효율을 높여주기 위한 도구로써 쓰인다.
- **Long Tail에 존재하는 컨텐츠가 적절하게 추천이 될수록 사용자의 만족도는 높아지고 동시에 개인화 성능도 높아진다.**

#

# Recommendation System Data Structure
### 1. User data
- 유저 프로파일링을 통해 유저의 정보를 모으는데 모아진 데이터는 다음과 같다.
- **식별자** : 유저 ID, 디바이스 ID 등 유저를 구별할 수 있는 정보
- **데모그래픽 정보** : 성별, 연령 지역 등
    - 데모그래픽 정보는 다른 정보로부터 추정하여 구하기도 한다.
- **유저 행동 정보** : 페이지 방문 기록, 평점, 페이지 재방문율 등
    - 이전에는 유저의 행동 정보를 잘 활용하지 못하였지만 최근에는 많은 딥러닝 기술들이 추천시스템에 적용되어 비교적 활발히 사용 중

### 2. Item data
- 아이템 프로파일링을 통해 아이템의 정보를 모으는데 모아진 데이터는 다음과 같다.
- **Item meta data** : 추천 아이템의 종류(뉴스, 광고, 미디어 컨텐츠, 상품 등)에 따라서 아이템의 고유 정보(meta data)가 달라진다. 예를 들어 영화의 경우 장르와 러닝타임 출연 배우 등이 아이템 메타데이터에 해당한다.

### 3. User-Item interactive data
- 유저의 활동 기록을 바탕으로 추천 시스템 학습을 위한 데이터에 feedback 되는 데이터, Feedback의 종류는 아래 두 가지로 나뉜다.
- **Explicit Feedback**
    - 용어 그대로 사용자가 직접 해당 아이템에 대해 평가를 한 feedback을 의미한다.
- **Implicit Feedback**
    - 사용자가 아이템을 직접적으로 평가한 것이 아닌 단순 클릭이나 구매 혹은 해당 아이템 페이지 방문 시간 등에 대한 정보를 의미한다.
- **실제 추천 시스템 데이터를 구축할 때는 Explicit 보다 Implicit에 대한 데이터가 많다**

#

# Goal of Recommendation System
1. 랭킹 
2. 예측 
- 위의 두 가지 목표를 위해 유저와 아이템간의 상호 작용에 대한 평가가 필요함

### 랭킹
- 유저에게 적절한 아이템 Top K개를 추천하는 문제
- 정확하게 유저의 평점을 예측할 필요는 없기 때문에 아래와 같은 평가지표를 가진다.
- Precision@K, Recall@K, MAP@K, nDCG@K

### 예측
- 아이템에 대한 유저의 선호도를 예측하는 문제
- 유저-아이템 matrix의 빈칸을 채우는 문제라고도 바꾸어 말할 수 있다.
- Explicit Feedback : 특정 유저가 특정 아아템에 대해 매길 평점을 예측
- Implicit Feedback : 특정 유저가 특정 아이템을 구매할 확률 예측
- 예측 성능 지표는 MAE, RMSE, AUC등을 가진다.  

#

# 새롭게 구축된 추천 시스템의 모델에 대한 성능 평가 방법
- 2가지 관점에서 볼 수 있음
1. 비즈니스/서비스
    - 새롭게 구축된 추천 시스템으로 인한 매출 증가율
    - 유저의 CTR(노출당 클릭횟수)의 증가율
2. 품질
    - 연관성
        - 추천한 아이템과 유저와의 관련성
    - 다양성
        - 추천한 TopK 아이템이 얼마나 다양한가 
    - 새로움
        - 새로운 아이템이 추천되는가
    - 참신함
        - 유저가 생각지도 못한(아마도 Long Tail)부분의 아이템이 추천되는가


#

# Offline Test
- 추천 모델을 검증하기 위해 가장 먼저 수행되는 단계
- 추천 모델의 성능을 수학적인 지표로 검증한다.
- 성능지표
    - 랭킹 문제 : Precision@K, Recall@K ..
    - 예측 문제 : RMSE, AUC ..
- Serving bias : offline test와 online test간의 성능차이의 원인
    - 실제 모델을 serving하면 학습할 때의 데이터와 다른 데이터들이 새롭게 추가되기 때문에 여기서 오는 bias를 Serving bias라고 한다.
    - 따라서 실제 서비스 상황에서는 offline test와 online test간의 다양한 양상이 존재한다.

### Precion

### Recall

### Mean Average Precision(MAP)

### Normalized Discounted Cumulative Gain(NDCG)


# Online A/B Test
- 새롭게 개발된 모델과 기존 모델을 실제 서빙하면서 두 모델을 비교하는 방법

# Popularity Based Recommendation
- 가장 인기있는 아이템을 추천하는 방법
- 서비스 초반에 많이 사용하는 방법이다.
- "인기"에 대한 지표
    - 평점, 페이지 방문율 등
- 인기도를 기반으로 score를 만드는 방법
    1. 조회수가 높은 순
    2. 평균 평점이 높은 순
- **단순히 score를 계산하는 것이 아니라 날짜에 따른 중요도 감소 등과 같은 다양한 지표를 결합하여 score를 매기는 것이 중요하다. 따라서 아래와 같이 3가지의 방법이 고안되었다.**  

- **Hacker News Formula**
    - 뉴스를 추천해주는 서비스에 사용되는 formula
    - score는 pageview에 비례하고 age에 반비례하는 성질이 있다.
    - gravity라는 상수를 제곱해줌으로 인해서 pageview보다 age의 변화에 따라 score가 더 민감하게 변화하는 효과가 있다.
    - 따라서 아무리 많은 pageview가 있다고 하더라도 시간이 지나면 score값은 낮아진다.

- **Reddit Formula**
    - 시간이 지날수록 점수가 낮아지는 것이 아닌, 게시된 날짜가 최신일수록 높은 점수를 부여하도록 짜여진 formula
    - 첫번째 term
        - 인기도를 의미
        - 좋아요가 많을수록 첫번째 term이 상승한다.
        - log값으로 보정되어있는 이유는 시간이 지날 수록 평점의 방향성이 한쪽으로 무한히 커지는 경향이 있기 때문이다.
    - 두번째 term
        - 포스팅된 절대 시간
        - seconds값에 의해 좌우되며 seconds(게시된 절대시간)이 커질수록(최근 게시물일수록) 커진다
 
- **Steam Rating Formula**
    - 평점이 아무리 높더라도 평가자가 적으면 데이터의 신뢰도가 낮다
    - 따라서 평가자의 수도 수치에 반영한 formula
    - review의 개수가 너무 적을 경우에는 2번째 term을 통해서 score값을 평균보다 높게 혹은 낮게 보정해준다.
    - review의 개수가 많을 경우 평균 평점과 거의 유사해진다.

# 추천 시스템에서 사용되는 ML & DL
- 현업에서 추천 시스템은 DL보다는 ML 모델을 많이 사용한다.
- 이유는 크게 두 가지이다.
    - 다른 분야(CV, NLP)에 비해서 ML 대비 DL의 성능 향상 폭이 좋지 않다.
    - 많은 유저가 사용하는 큰 트래픽을 감당해야 하기 때문에 계산량이 많은 딥러닝 모델에는 적합하지 않음

# Association Analysis
- 이용자의 아이템 구매나 조회 데이터 사이의 규칙을 발견하기 위해 사용함
- **Support**
    - support count
        - 전체 transaction에서 itemset이 등장하는 횟수
    - support
        - itemset이 등장하는 횟수(support count) / 전체 transaction
        - 이 때 개별 itemset에 적용할 수도 있지만 itemset의 연관 규칙에도 사용가능하다.
    - frequent itemset
        - 유저가 지정한 minimum support 값 이상의 itemset
- **Confidence**
    - 특정 itemset X가 transaction에 존재할 때 itemset Y도 포함할 확률(조건부 확률)
- **lift**
    - 특정 itemset X가 transaction에 존재할 때 itemset Y도 포함할 확률 / Y가 등장할 확률
    - **lift == 1 : X,Y는 독립**
    - **lift > 1 : X,Y가 양의 상관관계를 가짐**
    - **lift < 1 : X,Y가 음의 상관관계를 가짐**

# Association Rule을 찾는 방법
- item이 많아지면, 가능한 itemset에 대한 rule이 무한정 많아짐
- 따라서 유의미한 rule만 찾아야할 필요가 있다.
- **유의미한 rule 찾는 방법**
    1. minimum support, minimum confidence를 사용자가 지정한 후 이를 바탕으로 rule을 필터링 함
        - transaction 중 빈도율이 낮거나 조건부 확률이 낮은 rule을 필터링
    2. 1차 필터링 후 lift값을 기준으로 내림차순 정렬하여 lift값이 높은 rule들을 찾아냄
        - lift값이 크면 상관관계가 높기 때문에 유의미함을 의미  

### 그렇다면 minimum support, minimum confidence 보다 큰 support와 confidence를 어떻게 찾을 수 있을까?

- **Brute-force**
    - 가능한 경우의 수를 모두 탐색
    - 탐색한 규칙들에 대한 support와 confidence 계산
    - minimum support, minimum confidence를 만족하는 값들만 필터링
    - **단점 : 어마무시한 계산량 => (transaction 개수) X (itemset 개수) X (itemset의 가능한 연관 규칙의 개수)**
    - **따라서 효율적인 minimum support 이상의 itemset의 support를 탐색하는 방법이 필요로 하고 아래의 3가지 방법이 존재한다**

- **Apriori**
    - 가능한 후보 itemset의 개수를 줄이는 방법
- **Direct Hashing & Pruning (DHP)**
    - 탐색하는 transection의 숫자를 줄이는 방법
- **FP-Growth**
    - 탐색하는 횟수를 줄이는 방법
