# function

```bash
function 함수명 () {
  variable=$1
  variable2=$2
  함수내용
  
  echo 결과값
  return 결과값
}

함수명 $1 $2
result=`함수명`  // echo 값을 받음
echo $? // (echo $결과값) return 값을 받음

```

ex)

```bash
function back_ground_process () {
    i=$1
    bash test.sh
    grep -o "test" >> test/result_$i.txt
}

back_ground_process 1 &
```

[Refer](https://net711.tistory.com/entry/%EB%B0%B0%EC%89%AC-%EC%89%98-%ED%95%A8%EC%88%98)
