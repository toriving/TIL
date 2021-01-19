# Accuracy, Precision, Recall, F1 Score

## Summary
![img](https://github.com/toriving/TIL/blob/master/asset/diagnostic_testing.png?raw=true)
![img](https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Precisionrecall.svg/350px-Precisionrecall.svg.png)

![img](https://t1.daumcdn.net/cfile/tistory/99DC064C5BE056CE10)

**모델이 맞혔는지 - 모델의 예측**  

**True Positive** : 모델이 True라고 분류, 실제로 True 인 경우  
**True Negative** : 모델이 False라고 분류, 실제로 False 인 경우  
**False Positive** : 모델이 True라고 분류, 실제로 False 인 경우  
**False Negative** : 모델이 False라고 분류, 실제로 True 인 경우  

## Accuracy (정확도)

올바르게 예측된 데이터의 수를 전체 데이터 수로 나눈 값  

(True Positive + True Negative) / (True Positive + True Negative + False Positive + False Negative)

## Precision (정밀도) - Positive Predictive Value (PPV)

모델이 True (Positive)로 예측한 데이터 중 실제로 True 인 데이터의 수

True Positive / (True Positive + False Positive)

## Recall (재현율) - Sensitivity, hit rate, True Positive Rate (TPR)

실제로 True 인 데이터를 모델이 True (positive) 라고 예측한 데이터의 수  

True Positive / (True Positive + False Negative)

## F1 Score

Precision과 Recall의 조화평균

2 * (Precision * Recall) / (Precision + Recall)


## AUC
: Area Under the Curve  
임의의 curve에 대해 그 아래의 면적  

## Receiver-Operating Characteristic Curve (ROC Curve)
: TPR과 FPR 관계를 나타내는 커브  
ROC curve의 auc는 1에 가까울 수록 좋다  
x=y와 비교  

![img](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT1gATNhLOF5BAyYY64oRAbF5awQIwlgD09AQ&usqp=CAU)


## Precision-Recall Curve (PR Curve)

x축을 Recall, y축을 Precision으로 하는 curve  
base line을 두고 비교  


![img](https://mblogthumb-phinf.pstatic.net/MjAxOTEwMThfNDkg/MDAxNTcxNDAzOTM3ODE4.KODPnmJmMxigcWgNt6QeMaMqLMN8EF2yHZjOLYvTxv8g.rgKvQc1rsJlPqSSW37ACf5h5SRN9-6bl7bVx3Z_sjmIg.PNG.sw4r/image.png?type=w800)


## ROC curve vs PR curve
일반적으로 ROC curve가 더 robustness 하나, imbalanced dataset에 대해서는 PR curve 사용

## Reference
https://pacientes.github.io/posts/2021/01/ml_precision_recall/?fbclid=IwAR3tVpsJPtdKgD0BfjdyHI28VEXQmkayNre6DGvSpeB3NO1V4Tjeg0MeYoM
