# Exception - 예외처리

## try, except 문

```python
try:
    ...
except [발생 오류 [as 오류 메시지 변수]]:
    ...
```

try 블록 수행 중 오류가 발생하면 except 블록이 수행됨.  

오류가 발생하지 않으면 except는 수행하지 않음.  

### 1. try, except 만 쓰는 방법
```python
try:
    ...
except:
    ...
```

오류 종류 상관 없이 except 블록 수행

### 2. 발생 오류만 포함한 except 문
```python
try:
    ...
except 발생 오류:
    ...
```

발생한 오류가 except에서 정해놓은 오류와 일치할 때만 except 블록 수행

### 3. 발생 오류와 오류 메시지 변수까지 포함한 except문

```python
try:
    ...
except 발생 오류 as 오류 메시지 변수:
    ...
```
두번째의 경우에서 오류 메시지를 알고 싶을 때 사용하는 방법

```python
try:
    4/0
except ZeroDivisionError as e:
    print(e)

division by zero
```

## try .. finally

try 문에 finally 사용 가능

finally 는 try 문이 끝나면 예외 발생 여부에 상관없이 항상 수행됨

보통 사용한 리소스를 close 할 때 사용

```python
f = open('foo.txt', 'w')
try:
    ...
finally:
    f.close()
```

## 여러개 오류 처리하기
```python
try: 
    ...
except 발생 오류1:
    ...
except 발생 오류2:
    ...
```

```python
try:
    a = [1,2]
    print(a[3])
    4/0
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
except IndexError:
    print("인덱싱 할 수 없습니다.")
```

```python
try:
    a = [1,2]
    print(a[3])
    4/0
except (ZeroDivisionError, IndexError) as e:
    print(e)
```

## 오류 회피하기

```python
try:
    f = open("나없는파일", 'r')
except FileNotFoundError:
    pass
```

## 오류 일부러 발생시키기
**사실 이것 때문에 작성**
어떻게 하면 오류를 예쁘게 발생시킬 수 있을지...?

```python
class Bird:
    def fly(self):
        raise NotImplementedError
```

raise 문 이용

### 예외 만들기

예외를 만들어서 raise 문에 적절히 사용하면 예쁘게 만들 수 있지 않을까?

```python
class MyError(Exception):
    pass

def say_nick(nick):
    if nick == '바보':
        raise MyError()
    print(nick)

say_nick("천사")
say_nick("바보")

천사
Traceback (most recent call last):
  File "...", line 11, in <module>
    say_nick("바보")
  File "...", line 7, in say_nick
    raise MyError()
__main__.MyError
```

raise 말고도 try ... except 문을 이용할 수 있다

```python
try:
    say_nick("천사")
    say_nick("바보")
except MyError:
    print("허용되지 않는 별명입니다.")
```

오류 메시지를 사용하고 싶으면,

```python
try:
    say_nick("천사")
    say_nick("바보")
except MyError as e:
    print(e)
```

그러나, MyError에서 __str__ 메서드를 구현을 안했으므로 오류가 표시가 안됨

```python
class MyError(Exception):
    def __str__(self):
        return "허용되지 않는 별명입니다."
```

이렇게 해야함

예외를 직접 안만들고 이미 정의되어 있는걸 사용할 수 있음

정의된 예외는 많으므로 [여기](https://docs.python.org/ko/3/library/exceptions.html#base-classes)를 참조

사용자 정의 예외에서는 [Exception](https://docs.python.org/ko/3/library/exceptions.html#Exception) 을 상속해야함

```python
class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message

class TransitionError(Error):
    """Raised when an operation attempts a state transition that's not
    allowed.

    Attributes:
        previous -- state at beginning of transition
        next -- attempted new state
        message -- explanation of why the specific transition is not allowed
    """

    def __init__(self, previous, next, message):
        self.previous = previous
        self.next = next
        self.message = message
```

아래와 같이 다양한 방법으로 사용 가능

```python
try:
    ...
except InputError as e:
    print(e)
```

```python
try:
    ...
except:
    Exception("error")
```

```python
if ...:
    ...
else:
    raise Exception("error")
```

```python
if ...:
    ...
else:
    raise InputError()
```



### Reference
[점프투파이썬](https://wikidocs.net/30)  
[Python doc](https://docs.python.org/3/tutorial/errors.html)