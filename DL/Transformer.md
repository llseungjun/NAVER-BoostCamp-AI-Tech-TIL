# Transformer
- attention이라는 구조를 처음 사용한 squential model
- language model뿐 아니라 image detection model이나 image classificaiton 문제에도 이용된다.

### 구조
- encoder와 decoder로 구성됨
- 재귀적으로 각 시퀀스 하나당 학습하지 않고 한번에 모든 시퀀스를 학습한다.
- RNN 구조가 아님
