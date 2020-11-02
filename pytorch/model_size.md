# Model의 parameter 사이즈

논문에서 자주 보이는 (110M) 과 같은 모델 파라미터 사이즈를 얻는법

```python
pytorch_total_params = sum(p.numel() for p in model.parameters() if p.requires_grad)
print(pytorch_total_params)
```
