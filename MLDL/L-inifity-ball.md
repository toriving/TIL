# L-inifity-ball

먼저 Ln norm / Ln loss / Ln ball에 대한 이해가 필요하다. (n=0,1,2...)   
[norm](https://rorasa.wordpress.com/2012/05/13/l0-norm-l1-norm-l2-norm-l-infinity-norm/)  
[Lp_space](https://en.wikipedia.org/wiki/Lp_space)  
[p-norm](https://en.wikipedia.org/wiki/Norm_(mathematics)#p-norm)  
[Ball](https://en.wikipedia.org/wiki/Ball_(mathematics))  

여기서 부터는 2차원으로 가정한다.

L1 / L2 - ball를 시각화 하는데는 쉽게 이해가 된다.

L1의 경우 |x1| + |x2| = 1 을 생각하면 된다.

L2의 경우 root(x1^2 + x2^2) = 1 을 생각하면 된다.

하지만 L inifity ball은 어떻게 될까?

직관적으로 정사각형이 되는것이 맞다 (L n이 커질수록 정사각형에 가까워진다)

L inifity norm의 정의가 max{|x1|, |x2|} 이 된다.

따라서 L inifity ball은 max{|x1|, |x2|} = 1이 되고, x1이 1이라고 가정하면 x2는 -1<=x2<=1 이 될 수 있다..

반대로도 동일하다.

그림으로 그리면 정사각형이 된다.

[L inifity ball](https://math.stackexchange.com/questions/520002/unit-ball-with-p-norm)
