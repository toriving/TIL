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
