# Graph Neural Network(GNN)의 개념
- **Graph**
    - node와 edge들로 이루어진 자료구조
    - 서로 연결되어 있는 데이터를 표현하기 적합
        - 유저-아이템의 관계를 모델링하기에 적합
    - non-euclidean space의 모델링이 가능
        - 그래프를 활용하여 데이터의 표현을 단순하게 만들 수 있다.  

- **Graph Neural Network를 표현하는 가장 기본적인 방법**
    - 인접행렬로 표현 -> 실제로 모델링에 사용하지는 않음
        - 문제점
            - 노드가 많아지면 feature가 증가(연산량 증가)
            - 노드가 입력되는 순서에 따라서 결과가 바뀔 수 있음  

- **Graph Convolution Network**
    - 2d convolution의 기법을 non-euclidean space의 graph에 적용하는 기법
        - filter의 파라미터를 통일하여 파라미터 수를 감소시킬 수 있다.
        - layer를 깊게 쌓으면 근접한 neighbor뿐 아니라 그 옆의 neighbor까지 관계 특성 파악 가능

# Neural Graph Collaborative Filtering의 개념
- GNN을 기반으로 ***user-item의 상호작용을 임베딩 과정***에서 추출하는 방법
- **왜 쓸까?**
    - Neural network를 적용한 기존 CF는 임베딩 단계에서 user-item의 상호작용을 추출하지 못함
        - MF 모델에서도 item latent matrix와 user latent matrix를 따로 구현 뒤, 내적을 통해서 상호작용을 추출한다.
- **어떤 구조로 만들까?**
    - 임베딩 시점부터 유저-아이템의 상호작용이 학습될 수 있도록 만듦
        - **GNN 구조 이용**
            - 경로가 1보다 큰 연결을 표현하여 임베딩할 수 있다.
    - **임베딩 레이어**
        - 유저와 아이템one-hot encoding을 k차원으로 임베딩해주는 레이어
    - **전파 레이어**
        - First-order propagation
            
        - High-order propagation
            - High-order connectivity(경로가 1보다 큰 연결)를 학습
    - **예측 레이어**
        - 전파레이어를 타고 넘어온 여러개의 출력값을 concat해서 최종 예측값 출력

# LightGCN의 개념





