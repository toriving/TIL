# Constrative_Learning.md

Contrastive Learning을 간단히 설명하면, Contrastive Learning 기반 방법론들은 같은 image에 서로 다른 augmentation을 가한 뒤,  
두 positive pair의 feature representation은 거리가 가까워 지도록(유사해지도록) 학습을 하고,  
다른 image에 서로 다른 augmentation을 가한 뒤, 두 negative pair의 feature representation은 거리가 멀어지도록 학습을 시키는 게 핵심.  

![simCLR](https://hoya012.github.io/assets/img/byol/12.PNG)

[Refer](https://hoya012.github.io/blog/byol/)
