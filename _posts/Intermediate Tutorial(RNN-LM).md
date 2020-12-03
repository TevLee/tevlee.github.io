---
layout: post
title: Intermediate Tutorial(RNN-LM)
subtitle: Recurrent Neural Network Language Model(RNN-LM)
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [books, test]
---


### 1. RNN-LM 이란 무엇인가?  
RNN-LM 은 딥러닝 모델 RNN을 이용한 언어모델（Language Model)이다. RNN-LM은 n-gram language model과 비교된다. n-gram LM은 

1.못 본 단어에 대한 일반화(generalization) 
2.기억력이 좋지 않다는 점(long-term dependency)

의 단점을 가진다. RNN을 통해 이를 극복할 수 있다. 또한, n-gram LM은 고정된 개수의 단어만을 입력만으로 받는 반면 RNN을 사용하여 시점 개념이 도입되어 입력의 길이가 고정될 필요가 없다. 

### 2. RNN의 작동 원리
RNN은 Hidden state 개념을 사용하여 메모리를 저장하는 네트워크이다. 따라서, 현재까지 들어왔던 인풋에 대한 정보를 저장할 수 있다. 그림에서 인풋 벡터인 word embedding이 하나씩 RNN으로 입력된다. 인풋 벡터는 N개의 실수로 구성된 N차원 벡터이다. 

![resnet1](https://github.com/TevLee/tevlee.github.io/blob/main/_img/RNNLM1.png?raw=true)  

인풋벡터 word embedding이 들어가면 아웃풋으로 output vector가 하나 생성된다. 이것이 hidden state이다. 이것 또한 word embedding과 비슷하게 M개의 실수로 구성된 M차원 벡터이다. 인풋의 N과 아웃풋의 M은 서로 같을수도 다를수도 있다. 여기까지는 RNN의 작동방식이다.
      
### 3. RNN-LM의 작동 예제
RNN을 사용한 LM을 이해하기 위해서 LM의 정의를 예제를 통해 살펴보도록 한다. LM은 어떤 문장이 주어졌을 때, 이 문장의 그럴듯함을 확률로 계산하는 모델로 다음과 같이 결합확률을 활용한 chain rule로 풀어서 쓸 수 있다.

![resnet1](https://github.com/TevLee/tevlee.github.io/blob/main/_img/RNNLM2.png?raw=true)     

위 그림은 “I love”가 이미 있을 때, “you”가 올 확률, “I”가 있을 때 “love”가 올 확률, “I”가 문장 처음에 쓰일 확률을 표현한 것이다. 여기서 n-gram LM은 직전의 N개 단어만 고려하는 반면 RNN은 문장 전체를 고려한다. 이것이 가능한 이유는 메모리인 hidden state에 지금까지 본 단어들의 정도가 모두 압축되어 들어가 있기 때문이다. 

### 4. RNN-LM의 학습 방법
출력층에서는 softmax함수를 활성화 함수로 사용하는데, softmax 함수를 지나면서 각 원소를 0에서 1 사이의 실수 값을 가지며 총 합은 1이되는 상태로 바뀐다. 이렇게 나온 벡터를 t시점에서 예측값이라는 의미에서 표현하면 아래와 같다.
yt^=softmax(Wyht+b)


![resnet1](https://github.com/TevLee/tevlee.github.io/blob/main/_img/RNNLM3.png?raw=true)            

벡터 yt^의 각 차원 안에서의 값이 의미하는 것은 yt^의 j번째 인덱스가 가진 0과 1사이의 값은 j번째 단어가 다음 단어일 확률을 나타낸다. 그리고 yt^는 실제값. 즉, 실제 정답에 해당되는 단어인 원-핫 벡터의 값에 가까워져야 한다. 실제값에 해당되는 다음 단어를 y라고 했을 때, 이 두 벡터가 가까워지게 하기위해서 RNN-LM은 손실 함수로 cross-entropy 함수를 사용한다. 


### 5. Implementation of Recurrent Neural Network Language Model

[Recurrent Neural Network Language Model](https://github.com/20-2-SKKU-OSS/2020-2-OSS-10/tree/main/tutorials/02-intermediate/language_model){:target="_blank"}  
