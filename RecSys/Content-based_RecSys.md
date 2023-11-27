# Content-based Recommendation 개념
- 유저 X에 대해 과거에 선호한 아이템과 유사한 아이템을 추천하는 방법
- 비슷한 아이템의 기준이란 아이템의 메타데이터가 유사한 아이템을 의미한다.
- 장점 
    - 유저에게 추천할 때 다른 유저의 데이터가 필요하지 않음
    - long tail에 위치하는 아이템을 추천할 수 있음
    - 추천한 아이템에 왜 추천이 되었는지에 대한 설명이 가능함
- 단점
    - 아이템에 맞는 적절한 피처(아이템 메타 데이터)를 조합하는 것이 어려움
    - overspecialization
        - 특정 하나의 피처에 대한 추천 결과가 반복해서 나타날 수 있음
    - 다른 유저의 데이터를 활용할 수 없음

# Item Profile
- 아이템이 가진 피처들을 어떻게 표현할까?
    - **Vector형태로 표현하자! => TF-IDF로 해보자!**

### TF-IDF
- text로 이루어진 문서에서 중요한 단어를 선정하는 방법
- text를 이루고 있는 단어들에 대해 중요도를 스코어로 나타냄
- **TF-IDF는 어떻게 단어에 점수를 매기나요?** 
    - 단어 a에 대해서 특정 문서 b에 많이 등장하는 정도(Term Frequency, TF)
    - 단어 a가 전체 문서 B에서는 적게 등장하지만 특정문서 b에서 나오는 정도(Inverse Document Frequency, IDF)
    - 따라서 TF-IDF가 높다는 말은 단어 a가 특정문서 b에서 중요한 feature라는 말이다.
- **TF-IDF formula**
    - TF-IDF이미지 첨부예정
    - TF이미지 첨부예정
        - TF의 경우 문서의 길이가 서로 제각각일 경우가 있다. 이때 각각의 문서에서 가장 많이 나온 단어의 개수로 나눠주는 normalization을 통해서 길이가 긴 특정 문서에서 TF의 값이 높아지는 것을 방지할 수 있다.
    - IDF이미지 첨부예정
        - IDF값은 단어마다 정의가 된다.
        - log를 이용하지 않으면 IDF의 변화가 크기 때문에 log scale을 사용

# User Profile
- item profile을 구축 후 user에게 item을 추천할 차례이다.
- user에게 item을 추천하기 위해서는 user profile의 구축이 필요하다.
- **User Profile 구축**
    - user가 과거에 선호했던 item 데이터가 존재하고, 개별 item은 TF-IDF를 통해 vectorization 시킨 상태이다.
    - 이때 user의 item 데이터들에 있는 vector들을 통합하면 User Profile이 된다.
    - 통합하는 방법
        - 유저가 선호한 item vector들의 평균 이용
        - 유저가 item에 매긴 평점을 기반으로 normalization한 평균 이용

- 이렇게 user에 대한 vector를 구했으면 item을 찾아서 추천을 하는 일만 남았다.
    -**Cosine Similarity 이용**

### Cosine Similarity 
- 같은 차원을 가진 두 벡터에 대해 적용할 수 있다.
- 두 벡터의 내적으로 표현할 수 있으며, 두 벡터의 방향이 얼마나 유사한지를 의미한다.
- 즉 두 벡터간의 사이 각도를 의미한다.
    - Cosine Similarity는 따라서 -1과 1사이 범위의 값을 가질 수 있다.

- **User가 선호하는 아이템 Vector를 활용하여 정확한 평점 예측하기**
    1. Cosine Similarty를 구하고
    2. user가 과거에 해당 item에 매겼던 평점을 Cosine Similarty를 가중치로 사용하여 user의 예측 평점을 추론할 수 있다.
