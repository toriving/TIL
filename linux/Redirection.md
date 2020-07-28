# > and >>

`>` : 명령어 뒤에 나오는 파일에 쓸 때 사용(=write or overwrite)

`>>` : 명령어 뒤에 나오는 파일에 추가할 때 사용(=append)

예시
`>`의 경우
다음 아래 같이 사용하면 test.txt라는 파일이 없을 때는 생성하며 있다면 내용을 덮어쓰게 됩니다.
```
$ echo abcde > test.txt
```

To route the output and errors from Windows, you can use the following code outside of your Python file:
```
python a.py 1> a.out 2>&1
```

`>>`의 경우
다음 아래 같이 사용하면 test.txt라는 파일이 없을 때는 생성하며 있다면 test.txt 파일에 내용을 추가하게 됩니다.
```
$ echo abcde >> test.txt
```

grep과 함께 사용될 수 있음
```
$ grep -o '{"abc":[a-zA-Z0-9.,":_-]*}' test.txt | head -1 >> result.txt
```

[refer](https://twpower.github.io/114-difference-between-single-and-double-greater-than-sign)
