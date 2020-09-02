# *args, **kwargs and asterisk

args = arguments (positional args)
-> N개 입력으로 받아서 tuple로 변환


kwargs = keyword arguments
-> {keyword: value} 딕셔너리 형태로 받아서 사용

함수 파라미터 순서 : 일반 -> *args -> **kwargs



## Asterisk

1. 곱셈 및 거듭제곱 연산으로 사용할 때
2. 리스트형 컨테이너 타입의 데이터를 반복 확장하고자 할 때
3. 가변인자 (Variadic Parameters)를 사용하고자 할 때 ( * -> positional args, ** -> keyword args )
4. 컨테이너 타입의 데이터를 Unpacking 할 때 (* -> list,tuple... 타입, ** -> dict 타입)

[Refer1](https://brunch.co.kr/@princox/180)
[Refer2](https://mingrammer.com/understanding-the-asterisk-of-python/)
