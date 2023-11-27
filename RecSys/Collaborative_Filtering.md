추가 참고 자료 : https://tech.kakao.com/2021/10/18/collaborative-filtering/
# Collaborative Filtering 개념
- 많은 유저들로부터 얻은 정보를 통해 유저들의 관심사를 예측하는 방법
- 더 많은 유저들에 대한 정보가 축적될수록 성능이 좋아짐
- **CF의 목적**
    - 특정 유저에 대해 특정 아이템에 부여할 평점 예측
- **CF의 방법**
    1. 데이터를 바탕으로 user-item matrix를 생성한다.
        - 이때 모든 행렬의 항목이 채워져있지는 않다.
        - **이때 빈칸을 채워나가야하는 것이 목표**
    2. 유사도에 대한 기준을 정하고 user 혹은 item 사이의 유사도를 구한다.
    3. **주어진 평점과 유사도를 활용하여 행렬의 빈칸(평점)을 예측**
        - 평점이 높게 나온 상품들을 추천에 활용하게 된다.
        - 혹은 평점이 낮게 나온 상품들을 추천해주지 않는다.
- **CF의 특징**
    - 특정 유저 A와 비슷한 취향을 가진 유저들이 선호하는 아이템을 추천
        - ***아이템이 가진 속성을 사용하지 않음***

# 1. Memory-based Collaborative Filtering
## Neighborhood-based CF (NBCF)
- **목표**
    - 특정 유저가 아이템에 부여할 평점 예측
- **특징**
    - 장점
        - 구현이 간단하고 이해가 쉬움
    - 단점
        - 아이템과 유저가 늘어날 경우 확장성이 떨어짐(Scalability)
            - 모든 모델에서 가지는 문제이고 앞으로 해결해 나가야할 문제
            - Matrix Factorization으로 어느 정도 해결 가능
        - 데이터가 적을 경우 성능이 떨어짐(Sparsity)
            - **실제 데이터에서는 Sparsity가 큰 경우가 굉장히 많다**
                - 예를 들어 넷플릭스의 경우 영화가 엄청 많은데 한 사람이 모든 영화에 대한 평점, 혹은 전체 영화중 절반 이상의 평점을 매기는 경우가 있을까?
                - NBCF를 사용하기 위해서는 적어도 Sparsity ratio가 99.5%를 넘어야한다.
                - 이러한 경우에는 model based CF를 이용해야 한다.
                - **즉, 비어있는 데이터가 많은 경우 NBCF를 사용할 수 없다.**
            - 모든 모델에서 가지는 문제이고 앞으로 해결해 나가야할 문제
            - Matrix Factorization으로 어느 정도 해결 가능

- **구현 방법**        
    1. User-based CF
        - 유저간의 유사도를 사용한 방법
    2. Item-based CF    
        - 아이템간의 유사도를 사용한 방법
## K-Nearest Neighbors CF
- **NBCF의 한계**
    - 특정 아이템에 대한 평점을 예측하기 위해서는 해당 아이템을 평가한 모든 유저와의 유사도를 구해야한다.
    - ***유저가 많아질 경우 연산이 많아져 성능저하가 발생한다.***
    - 이것을 해결하기 위해 KNN CF를 이용한다.  

- **KNN CF의 개념**
    - 특정 아이템을 평가한 유저들 중 특정 아이템에 대한 평점 데이터가 없는 유저와 가장 유사한 k명의 유저를 KNN을 이용하여 예측
    - 특정 유저에 대해 유사한 k명 중 더 많은 클래스에 속하는 클러스터로 특정 유저가 분류된다.
    - 이때 k는 하이퍼파라미터이다.

- **그렇다면 특정 유저와 유사하다는 지표는 어떤 방법을 찾을 수 있을까?**
    - Mean Squared Difference Similarity 
        - User-Item에 해당하는 rating에 대해 서로 다른 두 유저의 rating값을 빼서 제곱한 값을 아이템의 수로 평균을 내면 구할 수 있다.
        - 해당 값은 유클리드 거리와 같은 값을 나타낸다.
        - 따라서 해당 값이 작을수록 두 유저는 유사도는 같음을 나타낸다.
        - 이미지 첨부예정
        - 최종 값이 따라서 MSD의 값이 0에 가까울수록 MSDS의 값은 커지는 관계식을 도출할 수 있다.
    - Cosine Silmilarity
        - 두 벡터의 방향이 같을 때 1 반대일 때 -1의 값을 갖는다.
        - 두 벡터의 크기가 달라도 가리키는 방향이 같으면 높은 값을 가진다.
    - Pearson Similarity (Pearson Correlation)
        - 두 벡터를 표본평균으로 정규화한 뒤 코사인 유사도를 구한 값이다.
        - 표본평균으로 정규화하기 때문에 두 벡터의 크기 차이도 고려할 수 있음
    - Jacard Similarity
        - 집합의 개념을 사용한 유사도
        - 두 집합이 얼마나 같은 아이템을 공유하고 있는지 나타낸다.
        - 두 벡터의 차원이 달라도 유사도 계산이 가능하다.  
    - ***위의 방법 중 모델에 따라 offline test를 거친 후 가장 좋은 성능을 낸 유사도를 선택하는 것이 일반적***

## Prediction 
### Average
### Weighted Average
### Relative Rating

# 2. Model-based Collaborative Filtering
- NBCF의 경우 다음 두가지의 문제점이 존재한다
    1. Sparsity
        - 데이터가 충분하지 않으면 성능이 낮은 문제
        - Cold start problem
    2. Scalability
        - 유저 아이템 수가 많아야 예측 정확도가 높아지지만, 너무 많은 데이터는 학습시간이 오래걸리는 문제점이 있다.  

- 따라서 이를 해결하기 위한 방법으로 MBCF 기법이 있다.
- **MBCF는 항목 간 유사성을 단순 비교하는 것이 아닌 데이터에 내재한 유저-아이템 패턴을 이용해 추천하는 기법이다.**
    - 파라미터를 학습하는 machine learning을 사용(기존 NBCF는 파라미터를 학습하지 않음)
        1. 주어진 데이터를 이용해 모델 학습
        2. 학습된 데이터의 정보가 파라미터의 형태로 모델에 저장
        3. **모델의 파라미터는 데이터의 패턴을 나타내고 손실함수로 나타내어 최적화를 통해 업데이트 된다.**

- NBCF와 차이점을 정리하자면
    - NBCF는 ***유저-아이템 벡터를 계산된 형태로 저장(파라미터로 저장하지 않음)***
        - 데이터를 그대로 메모리에 올려놓고 이용한다고 해서 Memory-based CF라고 한다.
    - MBCF는 ***유저-아이템 벡터를 학습을 통해서 특정 파라미터로 저장한다.***

- 현업에서 MF의 기법이 많이 사용되는데, MF를 딥러닝 모델에 응용하는 기법이 좋은 성능을 낸다.

- **MBCF의 장점**
    1. 모델 학습과 서빙 속도가 빠름
        - 학습된 모델을 통해 추천을 제공하기 때문에 속도가 빠르다.
    2. Sparsity / Scalability 해결
        - sparse한 데이터에도 이용이 가능함
        - 유저-아이템 데이터의 개수가 많아도 성능이 좋음
    3. overfitting 방지
        - 특정 neighbor에 치우치지 않고 전체 데이터에 대한 패턴을 찾기 때문에 overfitting을 방지할 수 있다.
    4. Limmited Coverage 극복
        - NBCF의 경우 주변의 유저-아이템의 rating을 많이 공유해야만 유사도가 정확해지는 문제가 있음
        - 하지만 MBCF의 경우 전체 데이터의 패턴을 학슶하기 때문에 유저-아이템의 rating을 많이 공유하지 않아도 성능이 좋음

# Latent Factor Model
- 유사(?)혹은 동일한 개념으로 임베딩이 있다.
- MBCF의 경우 Latent factor(임베딩)으로 표현된 모델이다.
### latent factor model이 뭔가요?
- 유저와 아이템의 복잡한 특성을 몇개의 벡터로 단순하게 표현하여 나타내는 모델
### latent factor model은 어떻게 계산되나요?
- 유저-아이템 행렬을 저차원의 행렬로 분해
### latent factor model은 그래서 어떻게 유사한 정도를 알아내나요?
- 같은 벡터 공간에 유저와 아이템 벡터를 위치시켜서 두 벡터의 유사도를 알아내어 추천한다.

***실제 모델을 학습했을 때 벡터에서 각 차원의 의미를 인간이 알 수는 없다.***

# Singular Value Decomposition
- 2차원 matrix를 user-item의 latent factor로 분해하기 위해 쓰는 선형대수적 방법
- 총 3가지 matrix로 분해된다.
    - 유저 latent factor matrix
    - latent factor diagonal matrix
    - 아이템 latent factor matrix

### SVD의 원리
- 각 행렬의 의미
    - R : user-item matrix
    - U : 유저 latent factor matrix
    - V : 아이템 latent factor matrix
    - $\sum$ : latent factor diagonal matrix  
    - 이렇게 분해한 matrix들을 원래의 R로 복원하여 예측하는 기법이다.
 
- **Full SVD**
    - latent factor diagonal matrix 전체를 사용
- **Truncated SVD**
    - latent factor diagonal matrix에서 대표값으로 사용될 k개의 특이값만 사용
    - latent factor diagonal matrix가 압축된다고 볼 수 있음
    - 해당 방법을 사용하면 원래 행렬 R과 shape은 같게 나오지만 값은 약간 다르다.
    - **하지만 특정된 k개의 정보만 가지고도 원래 행렬 R과 유사한 값 R_hat을 가지도록 압축된 정보를 이용하는 것이 이 방법의 핵심 아이디어**  

- **따라서 원래 R과 R_hat을 비교하여 원래 값을 얼마나 잘 예측했는지 비교하는 것이다.**

***마찬가지로 실제 모델을 학습했을 때 압축된 latent factor가 정확하게 무엇을 의미하는지 인간이 알 수는 없다.***  

### SVD의 한계
- sparsity가 높은 데이터에 대해서는 수행되지 않는다.
    - 따라서 결측된 데이터를 모두 채워서 dense matrix로 만들어야 SVD를 수행할 수 있다.
    - 이때 결측된 데이터는 0 또는 유저-아이템 평점의 평균으로 채울 수 있다.
        - 하지만 이러한 방법은 데이터를 증가시키기 때문에 계산량이 많아진다.
        - 그리고 임의로 채워넣은 데이터이기 때문에 예측 정확도를 낮출 수 있다.

- **SVD 정말 좋은데.. 다른 접근 방법 없을까? => MF**

# Matrix Factorization
- user-item matrix를 저차원의 user와 item의 latent matrix의 곱으로 분해
- SVD와 유사하지만 rating이 존재하는 부분만 모델링에 활용
    - **rating이 존재하지 않는 부분을 예측하는 모델을 만드는 것이 목표**

### Matrix Factorization 어떻게 작동하나요?
- user-item matrix를 P와 Q로 분해하여 기존 user-item matrix와 유사한 값을 가지도록 목적함수를 최적화

- 목적함수는 실제 r과 r_hat의 차이를 제곱한 부분과 각 파라미터가 overfitting되지 않도록 regularization한 부분을 합한 값이다.
- $\lambda$ 가 적용되어 있는 부분은 학습되는 파라미터(P와 Q)에 L2-norm을 한 것인데 학습데이터에 overfitting 되는 것을 방지하기 위해 존재하는 term이다.
- 여기서 정규화(regularization)이란
    - loss function에서 학습되는 weight의 값이 너무 커지지 않도록 제한하는 방법이다.
    - 이때 이 부분에 곱해지는 $\lambda$ 의 크기에 따라서 weight의 학습에도 영향이 끼치기 때문에 적절한 $\lambda$ 를 설정하는 것이 중요하다.  

- **목적함수 최적화**
    - SGD
        - P와 Q에 대해서 목적함수를 편미분하여 각각 파라미터를 업데이트한다.

### Matrix Factorization 응용 버전
- MF를 기반으로 다양한 방법들을 추가하여 성능을 향상시킨 모델들이 많다고 한다.
- **Bias들을 추가한 모델**
    - 유저나 아이템 별로 평정에 대한 편향이 생길 수 있다.
        - bias 추가된 목적함수에 대한 이미지 첨부 예정
        - 따라서 유저나 아이템 별로 bias를 추가하여 예측 성능을 높인다.
        - 이때 뮤 값은 글로벌 평균이고 학습되는 파라미터는 아니다. 
        - SGD이미지 첨부예정
        - SGD를 통해서 P,Q와 각각의 bias들을 학습할 수 있다.
- **Confidence를 추가한 모델**
    - 모든 데이터가 동일한 신뢰도를 갖지 않는다.
    - ***또한 implicit feedback dataset의 경우에도 confidence를 추가한다.***
        - confidence가 추가된 이미지 첨부 예정
        - 따라서 신뢰도에 해당하는 confidence를 추가하여 예측 성능을 높인다.
- **Temporal한 feature를 추가한 모델**
    - 시간에 따라서 특정 아이템에 대한 rating이 감소하는 경우가 있다.
        - 이미지 첨부 예정
        - 따라서 학습파라미터가 시간을 반영하도록 temporal한 feature를 추가하여 예측 성능을 높인다.
        - 위와 같이 t라는 값을 추가하여 각각의 학습 파라미터들이 시간에 대한 정보를 반영하도록 설계한다.

**implicit feedback dataset일 경우에 confidence말고 다른 방법을 쓰고 싶어요! => ALS 쓰세요**

#### Alternative Least Square(ALS)
- MF 모델을 기반으로 implicit feedback 데이터를 다루기 위해 설계된 모델
- 파라미터를 업데이트 하는 방법론 중에 하나로 기존 방식(SGD)와 다른 방식이다.
- 기존 MF와 어떻게 다른가?
    - 유저 latent(P)와 아이템 latent(Q)를 번갈아가면서 학습
    - P와 Q 둘 중 하나를 상수로 고정하고 나머지 값에 대해서만 학습 후 least-square로 문제를 푼다.
    - sparse한 데이터에 대해 SGD보다 더 학습을 잘한다.
    - 병렬 처리가 가능해서 빠르게 학습이 가능하다.

#### MF에서 Implicit Feedback에 대해 고려해야할 부분
- 기존 MF는 user-item에 대한 rating만 고려
- 하지만 Implicit Feedback은 다음 두 가지를 고려
    1. Preference
        - 유저가 아이템을 선호하는지 여부를 1 또는 0으로 구분
        - 수식 이미지 첨부 예정
    2. Confidence
        - 유저가 아이템을 얼마나 선호하는지에 대한 정도를 나타냄
        - 수식 이미지 첨부 예정
#### Implicit Feedback을 고려한 목적 함수
- 위에서 얘기한 **Confidence를 추가한 모델**을 응용한 버전이다.
- 수식 이미지 첨부예정
- confidence가 높으면 해당 데이터에 대해 모델의 정확도가 올라가고 반대의 경우에는 모델의 정확도가 낮아진다.
- **목적함수가 Explicit Feedback과는 달라졌지만 파라미터를 업데이트하는 최적화 방식은 SGD나 ALS로 동일하게 적용가능하다.**

### Bayesian Personalized Ranking
- MF 모델을 기반으로 implicit feedback 데이터를 다루기 위해 설계된 모델
- *새로운 관점 제시*
    - 베이지안 추론에 기반하여 서로 다른 아이템에 대한 유저의 선호도를 반영할 수 있다.
- **Personalized Ranking이란**
    - 특정 사용자에게 순서가 있는 아이템 리스트를 제공하는 것 
- Personalized Ranking을 반영한 최적화
    - 특정 유저가 아이템 a보다 b를 좋아한다는 정보를 활용해서 MF의 파라미터를 학습한다.
    - 특정 유저가 아이템 a보다 b를 좋아한다는 정보는 특정 유저의 Personalized ranking이라고 할 수 있다.
    - a>b (user1) 어쩌고에 관한 이미지 첨부 예정

- **그렇다면 Personalized Ranking을 implicit feedback 데이터에 어떻게 적용해야할까?**
    - 사용자의 클릭이나 구매와 같은 사용자의 로그는 아이템에 대한 확실한 선호도가 나타나지 않지만 관측된 데이터로 남아있다.
    - 그렇다면 관측되지 않은 데이터는 도대체 뭘까?
        - 유저가 아이템에 관심이 없거나
        - 유저가 관심이 있지만 해당 아이템의 존재를 모르는 둘 중 하나다.
    - 따라서 관측되지 않은 데이터에 대해서 위의 두가지(관심이 없는것과 아이템의 존재를 모르는 것)에 대해 고려해서 학습데이터로 사용해야 한다.  
  
    - 구체적인 적용 방법
        - 조건
            - 관측된 item은 무조건 관측되지 않은 item보다 선호한다.
            - 관측된 item끼리는 선호도를 추론할 수 없다.
            - 관측되지 않은 item끼리도 서로의 선호도를 추론할 수 없다.
            - 이 부분은 강의를 참조할 것(예시 이미지를 바탕으로 설명해주시는데 그걸 참고해서 다시 작성 예정)
        - 특징
            1. 관측되지 않은 item들에 대해서도 학습 가능하며
            2. 동시에 ranking도 부여 가능하다.
        - 학습 데이터 생성 예시
            - 학습데이터 triples 집합에 관해 강의 참조 후 다시 작성 예정
            - 선호도 데이터 예시에 대해 강의 참조 후 다시 작성 예정
        - 목적 함수(MAP 사용)
            - MAP 유도하는 과정을 강의 참조 후 다시 작성 예정

        


# 3. Hybrid CF
    - content-based와 CF의 결합

