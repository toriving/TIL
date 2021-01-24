# Inductive bias


## 1
very machine learning algorithm with any ability to generalize beyond the training data that it sees has some type of inductive bias, which are the assumptions made by the model to learn the target function and to generalize beyond training data.

For example, in linear regression, the model assumes that the output or dependent variable is related to independent variable linearly (in the weights). This is an inductive bias of the model.


## 2

Inductive bias can be thought of as the set of assumptions we make about a domain which we are trying to learn about.

Technically, when we are trying to learn Y from X and, initially, the hypothesis space (different functions for learning X->Y) for Y is infinite. To learn anything at all, we need to reduce the scope. This is done in the form of our beliefs/assumptions about the hypothesis space, also called inductive bias.

Through the introduction of these assumptions, we constrain our hypothesis space and also get the capability to incrementally test and improve on the data in the form of hyper-parameters.

Examples of inductive bias -

Linear Regression: Y varies linearly in X (in parameters of X).
Logistic Regression: There exists a hyperplane which separates negative / positive examples
Neural Networks: crudely speaking, Y is some non-linear function of X (the non linearity depends on the activation functions, topology etc.)


[Reference](https://stackoverflow.com/questions/35655267/what-is-inductive-bias-in-machine-learning)

## 3

기계학습에서의 inductive bias는, 학습 모델이 지금까지 만나보지 못했던 상황에서 정확한 예측을 하기 위해 사용하는 추가적인 가정을 의미합니다. (Wikipedia)  

기계학습에서는 특정 목표 출력(target output)을 예측하기 위해 학습 가능한 알고리즘 구축을 목표로 하고, 학습 모델에는 제한된 수의 입력과 출력에 대한 data가 주어집니다. 

학습이 성공적으로 끝난 후에, 학습 모델은 훈련동안에는 보이지 않았던 예들 까지도 정확한 출력에 가까워지도록 추측해야합니다. 이럴 때 추가적인 가정이 없이는 불가능한데, 이 Target function의 성질에 대해 필요한 가정과 같은 것이 Inductive bias라고 볼 수 있습니다.  

가장 고전적이고 대표적인 예가 Occam’s Razor, 오컴의 면도날입니다. 이는 target function에 대해 가장 단순한 무모순의 가설이 실제로 가장 좋을 것이라고 가정합니다. 

이 inductive bias의 개념은 Max Welling의 CoNLL 2018 keynote에서의 메인 테마였습니다. 2가지의 비결은 다음과 같습니다.  

[Reference](https://mino-park7.github.io/blog/)



## Inductive bias with permutation variant

- Inductive bias는 모델을 정의하는 뼈대가 되는 주요 가정
- 각 모델은 해당 가정을 바탕으로 모델을 구성함
---
e.g)
- Naive Bayes는 maximal conditional independence 가정
- SVM은 maximized margin 가정
- CNN은 인접한 픽셀끼리 높은 상관성을 같는 이미지를 처리함에 있어 커널을 바탕으로 feature 추출하도록 하는 CNN만의 inductive bias 존재 -> "이미지 처리에 특화되어 있다" 라고 말하는 이유
---
- 이러한 CNN은 픽셀의 순서가 바뀌면 feature가 달라짐. (커널에 의해서)
- 이것을 permutation variant 하다고 함. (입력 순서가 바뀌면 출력이 달라지는 것)
- 따라서 Inductive bias (모델의 특성을 결정하는 가정)에 따라서 permutation variant / invariant 여부가 결정됨

## Transformers with inductive bias

> In contrast to RNNs, Transformers, process the input in parallel. Although a weak notion of order is encoded by positional embeddings, no explicit assumption is made in the connectivity structure of the architecture. Moreover, they have a global receptive field and can access all tokens through self-attention. Finally, standard Transformers are not recursive, they apply the same set of weights on all input tokens, but they don’t do it recursively.

[Reference](https://samiraabnar.github.io/articles/2020-05/recurrence)  

> Transformer's inductive bias is more relaxed than either recurrent or convolutional architectures and reflects the fact that bag of words models are surprisingly competitive with the positionally aware NN models.
The positional embeddings of the transformer architecture allow the model to encode absolute position, relative position and positionally invariant relationships. Another inductive bias is true bi-directionality with being able to attend to all "future" and "past" tokens reflects the fact that sentences can be written in multiple ways with words appearing in different orders.
Another inductive bias that is part of BERT and other related models that is not necessarily strictly Transformer architecture related is to use Byte Pair Encoding for words. This reflects the inductive bias that words composed of similar subwords are related and allows the models to perform well without stemming and without having an enormous vocabulary size

위와 같은 이유로 RNN 및 CNN 보다 inductive bias가 약하다고 말할 수 있음

transformer의 transformer block 의 weight를 sharing 하면 recurrent bias를 얻을 수 있으며 성능향상도 얻을 수 있다고함 (Universal transformer)


[Reddit](https://www.reddit.com/r/MachineLearning/comments/d0gnyp/d_what_is_the_inductive_bias_in_transformer/)  
[Universal transformers](https://arxiv.org/pdf/1807.03819.pdf)  
[Relational inductive biases, deep learning, and graph networks](https://arxiv.org/pdf/1806.01261.pdf)  

## Transformers with permutation variant

> 일반적으로 transformer의 아웃풋 set을 하나의 vector로 permutation-invariant하게 reduce하는 함수 f를 정의할 수 있겠는데요. f의 예로는 BERT와 같이 0번째 vector를 가져오거나 set 전체를 summation하는 방법 등이 있겠습니다. 기본적으로 트랜스포머는 set을 인풋으로 받아서 set을 아웃풋으로 내뱉는 구조이고, f가 permutation invariant하면 인풋 set을 어떤 식으로 셔플하던지 간에 reduce된 vector는 같습니다.
말씀하신 position embedding을 더해서 사용하는 것은 순서가 있는 sequence를 다루기 위한 트랜스포머의 응용의 한 종류 인데요, position embedding을 붙이는 경우 두 개의 관점이 존재할 수 있는데: (1) 만약에 input vector set을 shuffle한 다음에 그 position에 따라서 position embedding을 붙이게 된다면 shuffle된 permutation에 따라서 f의 결과가 달라져서 permutation variant하다고 볼 수 있습니다. (2) 그러나 position embedding까지 더해진 전체 embedding 값 (token_embedding + position_embedding + token_type_embedding)을 set의 element로 본다면 이 경우 어떤 permutation이던지 f가 같은 vector를 출력할 수 있겠죠.
(1) 관점은 position embedding 자체를 transformer라는 함수의 구성 요소로 보는 경우입니다. 이 경우 transformer는 permutation variant 한게 맞습니다. 다만 현재 language modeling (더 나아가서 sequence modeling) 이외의 영역에서는 position embedding 없이 transformer를 사용하는 경우도 있습니다 (대표적으로 set transformer가 있습니다). 따라서 저는 (2) 관점, 즉 position embedding을 transformer의 구성 요소로 보지 않는 것이 더 타당하다고 생각합니다.

Reference : [본문 및 댓글](https://wonjae.kim/blog/2021/Exploiting_Contemporary_ML/?fbclid=IwAR3hTsYTNPJ93RbNTg5eJ3wbwcqDjN8Eqqp31tVJy3BurDl_Q5Kj6gpGal0)  

실제로 transformers를 통해 **position embedding을 0으로 모두 고정**시켜놓고 inference를 하면 cls 토큰은 permutation invariant 하다.  
각각의 input token은 vector로 변환되고 k, q, v 로 계산되어 사용이 되는데 모든 토큰에 대해 같은 weight를 통해 k, q, v로 변환하기 때문이다.    
또한 transformers 안의 linear projection이나 feed-forward layer의 경우 개별 토큰 (position wise)로 계산되기 때문에 입력 토큰의 순서에 따라서 다른 토큰들의 계산에 영향을 주지 않는다.  

```python
>>> from transformers import BertTokenizer, BertModel
>>> import torch

>>> tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
>>> model = BertModel.from_pretrained('bert-base-uncased')

>>> inputs = tokenizer("Hello, my dog is cute", return_tensors="pt")
>>> outputs = model(**inputs)

>>> last_hidden_states = outputs.last_hidden_state

t1 = {'position_ids': torch.tensor([0]*8), 'input_ids': torch.tensor([[  101,  7592,  1010,  2026,  3899,  2003, 10140,   102]]), 'token_type_ids': torch.tensor([[0, 0, 0, 0, 0, 0, 0, 0]]), 'attention_mask': torch.tensor([[1, 1, 1, 1, 1, 1, 1, 1]])}

t2 =  {'position_ids': torch.tensor([0]*8), 'input_ids': torch.tensor([[  101,    1010, 7592, 2026,  3899,  2003, 10140,   102]]), 'token_type_ids': torch.tensor([[0, 0, 0, 0, 0, 0, 0, 0]]), 'attention_mask': torch.tensor([[1, 1, 1, 1, 1, 1, 1, 1]])}

outputs = model(**t1)
outputs.last_hidden_state[0]

>>> tensor([[-0.3689,  0.2264, -0.7858,  ..., -0.0651,  0.4633,  0.3824],
        [-0.3558,  0.3680, -1.0172,  ..., -0.1852,  0.3436,  0.4455],
        [-0.4163,  0.3884, -0.5884,  ..., -0.0112,  0.2883,  0.2787],
        ...,
        [-0.3605,  0.4644, -1.0120,  ..., -0.2623,  0.1852,  0.6151],
        [-0.3672,  0.3302, -0.7691,  ..., -0.0583,  0.4470,  0.4243],
        [ 0.5736,  0.4118, -0.7354,  ...,  0.1107, -0.6458,  0.0465]],
       grad_fn=<SelectBackward>)

outputs = model(**t2)
outputs.last_hidden_state[0]

>>> tensor([[-0.3689,  0.2264, -0.7858,  ..., -0.0651,  0.4633,  0.3824],
        [-0.4163,  0.3884, -0.5884,  ..., -0.0112,  0.2883,  0.2787],
        [-0.3558,  0.3680, -1.0171,  ..., -0.1852,  0.3436,  0.4455],
        ...,
        [-0.3605,  0.4644, -1.0120,  ..., -0.2623,  0.1852,  0.6151],
        [-0.3672,  0.3302, -0.7691,  ..., -0.0583,  0.4470,  0.4243],
        [ 0.5736,  0.4118, -0.7354,  ...,  0.1107, -0.6458,  0.0465]],
       grad_fn=<SelectBackward>)
```

이해가 안되면 아래 레퍼런스를 보자  
https://github.com/cedrickchee/awesome-bert-nlp  
http://jalammar.github.io/illustrated-transformer/  


## etc
**Inductive bias가 약할수록 학습에 필요한 데이터는 많아야 충분히 학습이 가능**  
Inductive bias가 강할수록 모델 성능의 분산이 작아짐

![img](https://i.stack.imgur.com/QbD58.png)
