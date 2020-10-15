# 함수, 확률분포에서의 세미콜론(;), 바(|), 컴마(,) 구분

공부하다 보면 가끔 함수와 확률분포에서 세미콜론, 바, 컴마가 헷갈릴때가 있다.

물론 **컴마(,)**는 대부분 **joint distribution**을 표기하는데 사용되므로 헷갈리지는 않는데 세미콜론과 바가 헷갈리는 경우가 있다.

=> 𝑓(𝑥,𝜃) is the joint density of 𝑋 and Θ at the point (𝑥,𝜃) and only makes sense if Θ is a random variable.

---

그렇다면 **세미콜론(;)**은 어떻게 사용될까?

function(variables;parameters)

처럼 **함수에서** 변수와 파라미터를 구분하는데 사용된다.

아래 그림을 참고하자.

![img](https://taewanmerepo.github.io/2019/01/semicolonInfunction/010.jpg)

---

그러면 **바(|)**는 어떻게 사용될까?

흔히 아는 것처럼 **확률에서** **conditional distribution**을 표기하는데 사용된다.

P(X|Y)

---

그렇다면 왜 헷갈릴까?

𝑝(𝑌|𝑥,𝛽) 는 conditional distribution 이다.

이때 beta를 추정하고 싶다면 likelihood를 최대화해야한다.

𝐿(𝛽;𝑦,𝑥)=𝑝(𝑌|𝑥,𝛽)

로 표현이 된다.

다른 예로는 아래와 같은 경우가 있다.

𝑝𝜃(𝑥|𝑧,𝑦)=𝑓(𝑥;𝑧,𝑦,𝜃)

`
My preference is to write 𝑋|𝑌,𝑍;𝜃,𝜙, to show conditional distributions, conditional on other random variables, and fixed, unknown parameters. 
`

이처럼 많이 혼용되기도 하고 변환과정에서 헷갈릴수가 있음

기본적인 사용법을 알고 그떄그떄 해석해야할듯하다.

## Reference  
[함수 표기법: 세미콜론으로 변수와 파라미터 구분](http://taewan.kim/post/function_in_semicolon/)  
[Do the vertical bar and semicolon denote the same thing in the context of conditional probability?](https://math.stackexchange.com/questions/3421665/do-the-vertical-bar-and-semicolon-denote-the-same-thing-in-the-context-of-condit)  
[Meaning of probability notations 𝑃(𝑧;𝑑,𝑤) and 𝑃(𝑧|𝑑,𝑤)](https://stats.stackexchange.com/questions/10234/meaning-of-probability-notations-pzd-w-and-pzd-w)  
[What does the semicolon ; mean in a function definition](https://math.stackexchange.com/questions/342268/what-does-the-semicolon-mean-in-a-function-definition/722256)  
