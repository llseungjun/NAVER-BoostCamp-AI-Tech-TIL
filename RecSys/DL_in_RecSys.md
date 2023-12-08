# Recommendation System에 딥러닝을 쓰면 어떤 부분이 좋나요?
1. 비선형 모델링이 가능하다.
    - 데이터에 존재하는 비선형적인 패턴을 학습하는데 좋다.
2. feature를 효과적으로 줄이는 것이 가능하다.
3. sequence data를 처리하는데 좋다.
    - user와 item이 가지고 있는 sqeunce 정보를 활용할 수 있다.
# Neural Collaborative Filtering 
- 기존 MF가 가진 선형성의 한계를 극복하고자 Neural net 구조를 MF와 결합한 방법
- user-item vector space에 새로운 vector가 추가되었을 때 모순이 발생하는 경우가 있음
    - vector space에 모순되게 표현된 vector간에 내적을 구하게 된다면 결국 선형 연산이기 때문에 똑같이 모순이 발생하게 된다.
    - 위의 문제를 해결하기 위해 더 큰 차원으로 vector를 표현할 수 있다
        - 오버피팅 문제가 있음
    - **따라서 MF와 같은 기존 방법으로는 선형 모델의 한계가 있기 때문에 비선형 모델인 Neural net 구조를 이용**
- **모델은 어떻게 구성이 되나요?**
    - **MLP layer**
        - Input layer
            - user와 item 각각의 one-hot encoding vector
        - Embedding layer
            - input데이터가 dense vector로 임베딩
        - Neural CF layer
            - 임베딩된 user와 item vector를 concat하여 MLP layer를 통과 
        - Output layer
            - 최종 y_hat을 구함
    - **GMF layer**
        - input layer
            - user와 item 각각의 one-hot encoding vector
        - Embedding layer
            - input데이터가 dense vector로 임베딩
            - **이 때 MLP layer와 MF layer의 Embedding vector는 서로 다르다**
        - GMF layer
            - 임베딩된 user와 item vector를 concat
            - concat된 user와 item vector를 element wide product해서 GMF의 값 구함
    - **NeuMF layer**
        - MLP layer와 GMF layer를 통과한 output을 concat

-**GMF와 MLP layer를 따로 구성하는 이유는 뭘까?**
    - 앙상블 효과를 얻기 위함

# Deep Neural Network For YouTube Recommendation(DNN)
- **해결해야하는 문제 목표**
    1. user와 item 수가 압도적으로 많음
    2. 기존 컨텐츠와 실시간으로 업로드된 컨텐츠를 적절히 모델에 적용
    3. item을 예측하는데 기여하는 다양한 외부요인이 존재
- **그래서 어떻게 해결하는데**
- 2단계의 구조 사용
    - **1. Candidate Generation**
        - user에 대해 top N개의 추천 아이템 생성
            - 대략 수백개 정도로 추려짐
        - **Extreme Multicalss classification**
            - 특정 시간 t에서 특정 유저 u가 c라는 context를 가지고 있을 때 특정 영상 i를 볼 확률을 각각 계산
            - 영상의 개수가 수백만이기 때문에 Extreme이라는 명칭이 붙었다.
            - **watch vector & search vector**
                - 사용자의 watch data와 search data를 임베딩
                - 임베딩 된 vector에 대해 average를 바탕으로 예측 수행
                    - 평균을 내는 이유는 마지막에 있는 데이터가 큰 영향을 갖지 않게 하기 위함
            - **Demographic & Geographic Features**
                - 성별 및 인구통계학, 지리적 정보를 feature에 추가하여 적절히 임베딩 후 사용
            - **Example Age Feature**
                - 과거 데이터 위주로 편향되어 학습이 되는 문제가 있음
                - 따라서 watch log가 학습 시점으로부터 경과된 정도를 feature로 포함
            - **생성한 feature vector를 concat**
            - **dense layer를 통과한 후 user vector 생성**
            - **output layer는 classification을 위한 softmax function으로 구성**
        - **Candidate Generation Model Serving**
            - 앞의 Extreme Multicalss classification을 수행하기 위해서는 유저 1에 대해서 모든 비디오 vector와의 내적을 계산해야한다.
                - 따라서 ANN 라이브러리를 활용하여 serving 속도를 높인다.
    - **2. Ranking**
        - 추려진 item을 최종 ranking을 매겨 십여개 정도의 item 추천
        - **logistic regression**
            - Candidate Generation에서 추려진 아이템에서 최종적으로 클릭될 확률을 매겨서 순위를 생성
            - 따라서 logistic regression을 마지막 layer에 위치시킴
            - **이전 단에서는 neural net 구조로 되어 있기 때문에 다음에 나오는 많은 feature를 이용 가능**
            - 모델 그림을 보면 weighted logistic이라고 되어 있는데 이는 loss function에 시청 시간을 가중치로 적용하기 위함이다.
        - **user actions features**
            - 특정 유저가 특정 채널에서 영상을 본 개수
            - 특정 유저가 특정 토픽의 영상을 본 개수
            - 특정 영상에 대한 과거 시청 이력 등
        - **input feature concat**
        - **MLP layer**
            - 비디오가 실제로 시청될 확률로 매핑
            - 0,1의 값으로 시청 여부를 판단하는 CTR문제와 동일
        - **loss function**
            - weighted cross-entropy를 사용해서 비디오 시청시간에 대한 가중치 부여
            - abusing 영상에 대한 추천 감소            

# AutoEncoder
- 입력된 데이터를 출력으로 복원하는 비지도 학습
    - 이상치 탐지, representation learning, 노이즈 제거에 사용
### Denosing Autoencoder(DAE)
- 입력 데이터에 noise를 추가하여 모델을 학습하는 기법
    - noise input을 더 정확하게 복원할 수 있는 모델 생성 가능
    - noise input을 줌으로 인해 overfitting되는 현상을 방지하여 이러한 성능을 보임
# AutoRec
- AutoEncoder를 CF에 적용하여 user, item embedding에 대해 더 잘 표현하고 복잡도를 줄인 모델
- representation learning에 효과가 있기 때문에 이를 CF에 적용하면 효과적
    - **구현**
        - **input data**


# Collaborative Denoising Auto-Encoder 

