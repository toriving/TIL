# CNN과 이미지가 찰떡궁합인 이유
**본 글은 Reference 블로그에서 필요부분만 복붙했습니다.**

## 머신러닝의 가정
머신러닝(딥러닝) 모델들은 저마다 어떤 가정하에서 만들어진다. 

모델들마다 “나는 이런 특성을 가진 데이터를 주로 다루겠다.” 라고 선을 긋는 것이다. 

그래서 각 모델의 가정을 잘 아는것과 데이터 특성에 맞는 모델을 잘 선택하는 것이 중요하다.


## CNN의 가정
Alexnet 논문을 보면 이미지가 가진 특성에 대한 CNN의 가정이 짧게 언급된다.

“They also make strong and mostly correct assumptions about the nature of images (namely, stationarity of statistics and locality of pixel dependencies).”

바로 stationarity of statistics와 locality of pixel dependencies이다. 

짧게 stationarity, locality라고 하겠다. stationarity는 시계열 데이터의 통계적인 특성이 시간이 지나도 변하지 않는다는 뜻이고, locality는 이미지에서 한 점과 의미있게 연결된 점들은 주변에 있는 점들로만 국한된다는 뜻이다.

## Stationarity

이미지는 시간 대신 위치에 관계없이 동일한 패턴들이 반복되는 특징을 가지고 있다. 

그렇기 때문에 stationarity 가정하에 시계열과 비슷하게 이미지의 패턴을 파악할 수 있다.

즉 이미지의 특정 위치에서 학습한 파라미터를 이용해서 다른 위치에 있는 동일한 특징을 추출할 수 있다는 뜻이다.

이미 눈치채신 분들도 있겠지만 위에서 설명한 stationarity는 이미지 위치에 상관없이 동일한 특징들이 존재한다는 가정이기 때문에 파라미터를 공유(Parameter sharing)하는 Convolution 연산과 아주 잘 어울린다.

## locality of pixel dependencies

locality of pixel dependencies는 쉽게 이미지는 작은 특징들로 구성되어 있기 때문에 픽셀의 종속성은 특징이 있는 작은 지역으로 한정된다는 의미이다.

즉 이미지를 구성하는 특징들은 이미지 전체가 아닌 일부 지역에 근접한 픽셀들로만 구성되고 근접한 픽셀들끼리만 종속성을 가진다는 가정이다.

이러한 가정은 CNN이 Sparse interactions특성을 갖는 필터로 Convolution연산을 하는것과 아주 잘 어울린다.

Sparse interactions는 하나의 출력 유닛이 입력의 전체 유닛과 연결되어 있지않고 입력의 일부 유닛들과만 연결되어 있다는 의미로 주변 픽셀들과만 연관이 있다는 가정인 locality와 딱 들어 맞는다.

## translation equivariance

translation equivariance한 특성을 갖은 convolution 연산 (filter)과 translation invariance and downsampling 특성을 갖는 pooling 과정을 반복하다 맨 끝단까지 가면 CNN이라는 것이 큰 변화에도 translation invariance 하다고 말할수 있을까?

## 결론

결론
이미지의 특성인 stationarity of statistics와 locality of pixel dependencies를 가정하여 만들어진 CNN 모델이 이미지를 잘 다루는 건 당연한 일이다.

동일한 특징이 이미지내 여러 지역에 있을 수 있고, 작은 지역안에 픽셀 종속성이 있다는 가정 때문에 파라미터를 공유하고 sparse interaction을 가지는 필터와 Convolution연산을 하는것은 완벽하게 잘 들어맞는다.

그리고 Convolution 연산의 translation equivariance 특성에 파라미터 공유를 더해서 CNN 이 translation invariance를 가지게 된다는 것도 이해했다.

## Reference

아래 글은 너무 좋다.  
[CNN과 이미지가 찰떡궁합인 이유](https://medium.com/@seoilgun/cnn%EC%9D%98-stationarity%EC%99%80-locality-610166700979)  
[CNN은 왜 이미지영역에서 두각을 나타나게 된건가요?](https://89douner.tistory.com/58)
